---
layout: post
title: "MySQL cho developer 1.12: Schema migrations Thay đổi cấu trúc bảng"
category: MySQL
tags: [MySQL, MySQL for developer]
date: 2023-12-05
---

# Tầm quan trọng của migrations trong quản lý cấu trúc bảng cơ sở dữ liệu

Là những lập trình viên, chúng ta biết rằng khi yêu cầu kinh doanh thay đổi, chúng ta cần phải thay đổi cấu trúc bảng cơ sở dữ liệu tương ứng. Nhưng làm thế nào chúng ta có thể theo dõi những thay đổi này? Làm thế nào chúng ta có thể đảm bảo đội ngũ phát triển của chúng ta đồng thuận với những thay đổi này? Đó là lúc khái niệm migrations xuất hiện.

## Migrations là gì?

Về cơ bản, migrations là một thư mục chứa đầy các câu lệnh SQL giúp theo dõi các thay đổi trong cấu trúc bảng (schema) cơ sở dữ liệu của bạn. Hầu hết các framework full-stack đều có khái niệm migrations, cho phép lập trình viên thực hiện các thay đổi vào schema của mình một cách dễ dàng và hiệu quả. Migrations giúp lập trình viên thực hiện các thay đổi dễ  theo dõi, có kiểm soát phiên bản và dễ bảo trì.

Bất kỳ framework web nào bạn đang sử dụng, khái niệm migrations vẫn giữ nguyên: chúng giúp lập trình viên thực hiện các thay đổi vào schema của họ dễ theo dõi và dễ bảo trì.

## Best practices cho migrations

Khi viết migrations, việc quan trọng là thống nhất với đội ngũ của bạn về các best practices phù hợp. Dưới đây là một số điều bạn có thể xem xét:

- Luôn có các câu lệnh SQL rõ ràng để thể hiện cách cơ sở dữ liệu sẽ chuyển từ một trạng thái này sang trạng thái khác.
- Tránh sử dụng down migrations, có thể dẫn đến vấn đề nếu phương thức down không hoàn toàn revert được những gì phương thức up làm.
- Sử dụng version control (kiểm soát phiên bản) để theo dõi các thay đổi trong schema của bạn theo thời gian.

Ngoài ra, lập trình viên cũng nên xem xét khi nào chạy migrations, vì chúng có thể tốn kém và chiếm nhiều tài nguyên đáng kể. Các lựa chọn cho việc chạy migrations bao gồm bật màn hình bảo trì được lên lịch hoặc sử dụng các công cụ như `pt-online-schema-change` hoặc `gh-ost` (GitHub online schema change).

Migrations là một phần quan trọng của quản lý schema cơ sở dữ liệu giúp lập trình viên thực hiện các thay đổi vào schema của họ một cách dễ theo dõi và dễ bảo trì. Bằng cách tuân theo các best practices và hiểu rõ khi nào chạy migrations, lập trình viên có thể quản lý và điều chỉnh schema cơ sở dữ liệu của mình một cách hiệu quả khi yêu cầu kinh doanh thay đổi theo thời gian.
