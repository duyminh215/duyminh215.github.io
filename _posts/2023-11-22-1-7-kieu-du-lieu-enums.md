---
layout: post
title: "MySQL cho developer 1.7: Kiểu dữ liệu Enums"
category: MySQL
tags: [MySQL, MySQL for developer]
date: 2023-11-22
---
# Sức mạnh của Enums trong MySQL

Khi làm việc với dữ liệu String trong MySQL, điều quan trọng là bạn phải lưu trữ dữ liệu hợp lệ trong bảng. Có một cách để làm điều này là sử dụng enums, một loại dữ liệu đặc biệt cho phép bạn chỉ được insert vào cột danh sách các giá trị đã định nghĩa trước. Trong bài này, chúng ta sẽ khám phá sức mạnh của enums trong MySQL và cách bạn có thể sử dụng chúng để lưu trữ và quản lý dữ liệu một cách hiệu quả hơn.

## Enums là gì?

Enums giống như String, nhưng về bản chất, chúng được lưu trữ dưới dạng số nguyên. Enums mang lại khả năng đọc được của một String với kiểu dữ liệu bản chất lại là một số nguyên. Một cột enum có một danh sách các giá trị đã định nghĩa trước, và khi nhập giá trị nằm ngoài danh sách này đều sẽ gây ra lỗi. Tính năng này giúp đơn giản hóa việc (validate) kiểm tra dữ liệu trong cơ sở dữ liệu của bạn.

Để thấy cách enums hoạt động, hãy tạo một bảng orders với một cột `size` được khai báo là `ENUM`. Chúng ta sẽ truyền vào năm tùy chọn khác nhau đại diện cho các giá trị được phép cho cột:

```sql
CREATE TABLE orders (
  id INT AUTO_INCREMENT PRIMARY KEY,
  size ENUM('extra small', 'small', 'medium', 'large', 'extra large')
);

INSERT INTO orders (size) VALUES ('small'), ('medium'), ('large');
```
Như bạn có thể thấy, chúng ta đã chèn dữ liệu vào cột size bằng String. Tuy nhiên, nếu chúng ta thực hiện một truy vấn đơn giản yêu cầu giá trị phải là số nguyên, chúng ta sẽ thấy rằng những chuỗi này thực sự được lưu trữ dưới dạng số nguyên:

```sql
SELECT size, size+0 FROM orders;
```
Truy vấn này trả về:

```sql
+--------+--------+
| size   | size+0 |
+--------+--------+
| small  |      2 |
| medium |      3 |
| large  |      4 |
+--------+--------+
```
## Lợi ích của Enums

Sử dụng enums trong MySQL mang lại nhiều lợi ích, bao gồm:

### Kiểm tra (validate) dữ liệu

Như đã đề cập trước đó, enums cung cấp hỗ trợ việc valiate dữ liệu, giúp đảm bảo chỉ có dữ liệu hợp lệ được insert vào một cột. Khi cố gắng nhập một giá trị không hợp lệ, sẽ có lỗi xảy ra, ngăn chặn dữ liệu rác được insert vào cơ sở dữ liệu.

### Dễ dàng hiểu

Vì enums cho phép bạn lưu trữ các giá trị String có thể hiểu được trong cơ sở dữ liệu của bạn, nên việc đọc dữ liệu đã lưu trữ nhanh chóng hơn. Bạn không cần phải nhớ các số nguyên để hiểu dữ liệu; các giá trị là các từ có ý nghĩa trong tiếng Anh thông thường.

### Kiểu dữ liệu ngắn gọn

Enums là các kiểu dữ liệu ngắn gọn, có nghĩa là chúng chiếm ít không gian lưu trữ hơn so với các kiểu dữ liệu khác như chuỗi. Tính năng này làm cho chúng trở nên lý tưởng cho các cơ sở dữ liệu lớn.

## Nhược điểm của Enums

Mặc dù enums mang lại nhiều lợi ích, nhưng cũng có một số nhược điểm khi sử dụng chúng, bao gồm:

### Thay đổi phải vào schema

Nếu yêu cầu kinh doanh thay đổi và bạn cần thêm một tùy chọn khác vào các giá trị được phép, bạn sẽ phải thay đổi schema của bảng để thêm một enum mới. Mặc dù quá trình này không khó khăn, nhưng có thể làm phiền toái.

### Sắp xếp

Khi sắp xếp dữ liệu bằng cách sử dụng enums, MySQL sắp xếp theo giá trị số nguyên thay vì so sánh String. Mặc dù điều này có thể hữu ích trong một số trường hợp, nhưng cũng có thể gây nhầm lẫn, đặc biệt là nếu bạn không để ý điều này.

### Sử dụng enums số nguyên

Lưu ý rằng enums số nguyên có thể gây nhầm lẫn và nên tránh nếu có thể. Nếu bạn phải sử dụng enums số nguyên, nên sử dụng một cột TINYINT.

# Kết luận
Enums trong MySQL là một tính năng mạnh mẽ có thể giúp đơn giản hóa thiết kế cơ sở dữ liệu, tăng cường bảo mật và cải thiện khả năng đọc hiểu dữ liệu. Với một danh sách các giá trị được định nghĩa trước, ưu điểm của enums trở nên rõ ràng. Tuy nhiên, quan trọng nhất là phải nhớ đến các hạn chế và nhược điểm tiềm ẩn của việc sử dụng enums, như cần phải điều chỉnh cấu trúc nếu các giá trị cho phép thay đổi. Do đó，nếu sử dụng đúng cách, enums có thể là một công cụ có giá trị khi làm việc với dữ liệu chuỗi trong MySQL.
