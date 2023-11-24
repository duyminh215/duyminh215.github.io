---
layout: post
title: "MySQL cho developer 1.11: Các cột dữ liệu tự sinh"
category: MySQL
tags: [MySQL, MySQL for developer]
date: 2023-11-24
---

# Cách sử dụng cột tự sinh trong MySQL

MySQL là một hệ thống quản lý cơ sở dữ liệu mạnh mẽ cung cấp nhiều tính năng để giúp nhà phát triển làm việc với dữ liệu một cách dễ dàng. Một trong những tính năng nhiều là cột tự sinh, giúp tự động hóa một số công việc và tính toán.

Trong bài viết này, chúng ta sẽ tìm hiểu về cột tự sinh là gì, cách sử dụng chúng và một số trường hợp sử dụng phổ biến.

## Cột tự sinh là gì?

Cột tự sinh là một cách để MySQL thực hiện nhiều công việc hơn thay bạn, bằng cách cho phép bạn tạo ra các cột dựa trên các cột khác trong bảng của bạn. Theo cách đơn giản, một cột tự sinh là một cột được tính toán bằng một biểu thức, thay vì được lưu trực tiếp trong bảng.

Ý tưởng là bạn có thể định nghĩa một cột bằng một công thức hoặc phép tính, và MySQL sẽ tự động tính toán các giá trị cho cột đó dựa trên dữ liệu trong các cột khác.

## Ví dụ: tạo một bảng với các cột tự sinh

Hãy xem một ví dụ về cách tạo một bảng với các cột tự sinh. Trong ví dụ này, chúng ta sẽ tạo một bảng có tên là `emails`, với hai cột - `email` và `domain`.

Cột `email` là một varchar(255), đại diện cho địa chỉ email. Cột `domain` sẽ tự sinh dựa trên nội dung của cột `email`.

Để tạo ra cột tự sinh, chúng ta sẽ sử dụng từ khóa `AS` và một hàm gọi là `substring index`. Hàm `substring index` cho phép chúng ta trích xuất domain từ địa chỉ email.

Dưới đây là mã SQL:

```sql
CREATE TABLE emails (
  email varchar(255),
  domain varchar(255) AS (substring_index(email, '@', -1))
);
```
Chú ý rằng cột `domain` được định nghĩa là `varchar(255) AS (substring_index(email, '@', -1))`. Điều này có nghĩa là giá trị của cột `domain` sẽ được tính toán dựa trên nội dung của cột `email`, sử dụng hàm `substring_index`.

## Cột tự sinh ảo và được lưu trữ

Lưu ý, cột tự sinh có thể là cột ảo hoặc cột được lưu trữ.

Cột ảo được tính toán khi chạy và không chiếm bất kỳ không gian nào trên đĩa. Điều này có nghĩa là việc tính toán có thể mất thời gian hơn, nhưng không ảnh hưởng đến kích thước tổng thể của bảng.

Một cột được lưu trữ, ngược lại, được tính toán trong quá trình chèn hoặc cập nhật dữ liệu và được lưu trên đĩa, giống như một cột thông thường. Điều này có nghĩa là có thể nhanh chóng truy xuất dữ liệu từ một cột được lưu trữ, nhưng nó sẽ chiếm nhiều không gian hơn trên đĩa.

Khi tạo một cột tự sinh, bạn có thể chỉ định liệu nó có phải là ảo hay được lưu trữ bằng cách sử dụng từ khóa `VIRTUAL` hoặc `STORED`. Nếu bạn không chỉ định gì cả, cột sẽ mặc định là ảo.

## Trường hợp sử dụng cho cột tự sinh

Có nhiều trường hợp sử dụng tiềm năng cho cột tự sinh. Dưới đây là một số ví dụ:

- **Trích xuất dữ liệu từ các chuỗi JSON**: Nếu bạn có một cột chứa một chuỗi JSON lớn, bạn có thể sử dụng một cột tự sinh để trích xuất một trường cụ thể từ chuỗi JSON và tạo một cột mới chỉ chứa dữ liệu đó. Điều này có thể làm cho việc truy vấn dữ liệu dễ dàng hơn và cải thiện hiệu suất.

- **Thực hiện các phép tính**: Bạn có thể sử dụng cột tự sinh để thực hiện các phép tính như chuyển đổi đơn vị, áp dụng thuế và nhiều hơn nữa. Điều này có thể hữu ích cho việc tạo báo cáo hoặc thực hiện các nhiệm vụ phân tích dữ liệu khác.

- **Chuẩn hóa dữ liệu**: Nếu bạn có một cột chứa dữ liệu lặp lại, bạn có thể sử dụng một cột tự sinh để trích xuất dữ liệu đó và tạo một bảng mới chỉ chứa các giá trị duy nhất. Điều này có thể giúp dễ dàng quản lý dữ liệu của bạn và loại bỏ sự lặp lại.

# Kết luận

Cột tự sinh là một tính năng mạnh mẽ của MySQL có thể giúp bạn tự động hóa một số công việc và tính toán. Bằng cách định nghĩa một cột bằng một công thức hoặc phép tính, bạn có thể tiết kiệm thời gian và công sức của mình, đồng thời đảm bảo rằng dữ liệu của bạn luôn cập nhật.

Trong bài viết này, chúng ta covered cơ bản về cột tự sinh, bao gồm cách tạo chúng, sự khác biệt giữa cột ảo và cột được lưu trữ, và một số trường hợp sử dụng phổ biến. Hy vọng bạn thấy bài viết này thông tin và hữu ích, và bạn sẽ xem xét việc sử dụng cột tự sinh trong cơ sở dữ liệu MySQL của bạn.