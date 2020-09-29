---
layout: post
title: "Sử dụng Nginx làm load balancer"
category: nginx
tags: [nginx, scale]
date: 2017-01-05
---

Một điều rất quan trọng khi hệ thống ngày càng lớn là bạn biết cách scale nó lên để đáp ứng được nhiều user request lên server của bạn. Một cách rất kinh điển đó là scale theo bề ngang. Có nghĩa là hệ thống của bạn thay vì chạy trên 1 server thì sẽ được nhân lên thành nhiều nhiều server. Do đó, khi có nhiều request của nhiều người dùng thì sẽ phân phối các request đó đến với các server khác nhau. Một ví dụ đơn giản là nếu 1 server có thể phục vụ được khoảng 100 người cùng lúc thì nếu ta có 2 servers thì ta sẽ phục vụ được 200 người dùng cùng lúc.

Vấn đề đặt ra là làm thế nào để phân phối các requests đó đến với các servers khác nhau? Lúc đó người ta cần dùng đến loadblancer.

###Vậy Cân Bằng Tải (hay Load Balancing) là gì?

Cân Bằng Tải là việc phân bố đồng đều lưu lượng truy cập giữa hai hay nhiều các máy chủ có cùng chức năng trong cùng một hệ thống. Bằng cách đó, sẽ giúp cho hệ thống giảm thiểu tối đa tình trạng một máy chủ bị quá tải và ngưng hoạt động. Hoặc khi một máy chủ gặp sự cố, Cân Bằng Tải sẽ chỉ đạo phân phối công việc của máy chủ đó cho các máy chủ còn lại, đẩy thời gian uptime của hệ thống lên cao nhất và cải thiện năng suất hoạt động tổng thể.

Có rất nhiều phần mềm hỗ trợ để làm load balancer như HAProxy, nginx, lighttp,...

Hiện nay, với dự án cho công ty mình thì mình đang dùng Nginx để làm load balancer. Nginx là một web server rất nổi tiếng và đang ngày càng được nhiều developer sử dụng. Ngoài việc nó hoạt động như web server thì nginx cũng hỗ trợ rất tốt cho việc làm load balancer. Nginx được viết bằng C nên performance của nó rất tốt, tiêu tốn ít tài nguyên hệ thống (so với Apache Web Server).

Sau đây mình sẽ chỉ cho bạn cách config để có thể sử dụng được nginx như một load blancer.

Giả sử bạn muốn đón connection từ client ở máy 10.10.10.1 với cổng là 9000 và phân tải đến 2 servers là 10.10.10.9 và 10.10.10.10. Trước hết, bạn phải chạy service ở 2 máy 10.10.10.9 và 10.10.10.10 với cổng dịch vụ là 9002.

Để sử dụng nginx làm load blancer thì bạn config trên máy 10.10.10.1 như sau:

```
upstream proserver {
    server 10.10.10.9:9002;
    server 10.10.10.10:9002;
}

```

Trong đó 10.10.10.9 và 10.10.10.10 là 2 servers đang chạy dịch vụ ở cổng 9002.
Chúng ta sẽ config để máy 10.10.10.1 này đón ở cổng 9000 như sau:

```
server {
        proxy_buffering off;
        client_max_body_size 5M;
        listen 9000;

        location / {
            proxy_pass http://proserver;
        }
    }

```

Sau khi config xong thì chúng ta sẽ start nginx lên để nó làm load blancer cho 2 máy kia.

```
sudo service nginx restart

```

Nginx hỗ trợ việc chúng ta ưu tiên lưu lượng đến một server nào nhiều hơn server còn lại bằng tham số weight.
Chúng ta sẽ sửa lại config như sau:

```
upstream proserver {
    server 10.10.10.9:9002 weight=1;
    server 10.10.10.10:9002 weight=2;
}

```

Có nghĩa là lúc này, server 10.10.10.10 sẽ nhận requests nhiều gấp 2 lần server 10.10.10.9.
Ngoài ra, chúng ta còn có thể log lại dữ liệu request từ client bằng nginx.
Sau khi configure đầy đủ chúng ta sẽ được file load blancer như sau:

```
worker_processes  4;
user apache;
events {
    worker_connections  2048;
}

http {
    #limit_conn_zone $binary_remote_addr zone=addr:10m;
   log_format upstream_time \'$remote_addr - $remote_user [$time_local] \'
                             \'\"$request\" $status $body_bytes_sent \'
                             \'\"$http_referer\" \"$http_user_agent\"\'
                             \'rt=$request_time urt=\"$upstream_response_time\"\';

    upstream proserver {
        server 10.10.10.9:9002 weight=1;
        server 10.10.10.10:9002 weight=2;
    }

    server {
        if ($time_iso8601 ~ \"^(\\d{4})-(\\d{2})-(\\d{2})\") {
                set $year $1;
                set $month $2;
                set $day $3;
        }
        access_log /home/log/nginx/nginx-access-$year-$month-$day.log upstream_time;
        proxy_buffering off;
        client_max_body_size 5M;
        listen 9000;

        location / {

            proxy_set_header  Host  $host;
            proxy_set_header  X-Real-IP $remote_addr;
            proxy_set_header  X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_pass http://proserver;
        }
    }
}


```
