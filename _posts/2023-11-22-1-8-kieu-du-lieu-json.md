---
layout: post
title: "MySQL cho developer 1.9: Kiểu dữ liệu JSON"
category: MySQL
tags: [MySQL, MySQL for developer]
date: 2023-11-22
---

# Cột JSON trong MySQL: Khi nào, Tại sao và Cách sử dụng

MySQL đã hỗ trợ chính thức mạnh mẽ cho cột JSON (JavaScript Object Notation), cho phép các nhà phát triển tận dụng chúng giống như các kiểu dữ liệu khác trong MySQL, chẳng hạn như chuỗi, số và ngày giờ.

## Tạo và kiểm tra chuỗi JSON

Khi làm việc với JSON trong MySQL, kiểu dữ liệu chính là `JSON`. Để tạo một bảng có cột JSON, bạn có thể sử dụng code SQL sau:

```sql
CREATE TABLE has_json (
  id INT(11) NOT NULL AUTO_INCREMENT,
  json JSON NULL,
  PRIMARY KEY (id)
);
```

Lưu ý là MySQL rất chặt chẽ khi xử lý dữ liệu JSON so với các loại string khác. Dữ liệu JSON phải tuân theo quy định JSON; nếu không, MySQL sẽ từ chối insert. Ví dụ, nếu cố gắng insert một chuỗi JSON không hợp lệ, sẽ gây ra lỗi:

```sql
INSERT INTO has_json (json) VALUES ('{key:value}');
```

Đoạn code trên gây ra lỗi do thiếu dấu ngoặc kép xung quanh `key` và `value`.

```sql
> Error: Invalid JSON text: "Missing a name for object member." at position 1 in value for column 'has_json.json'.
```

Ngược lại, việc insert một chuỗi JSON hợp lệ có thể thực hiện như sau:
```sql
INSERT INTO has_json (json) VALUES ('{"key": "value"}');

SELECT json FROM has_json;
> {"key": "value"}

```
## Truy xuất Dữ liệu từ Cột JSON

Khi bạn có dữ liệu JSON hợp lệ trong cơ sở dữ liệu MySQL, bạn có thể sử dụng các hàm và toán tử khác nhau để truy xuất và thao tác nó. Để trích xuất một trường cụ thể từ một chuỗi JSON, bạn có thể sử dụng toán tử  `->>`:

```sql
SELECT json->>'$.key' AS key FROM has_json;
> key
> --------------
> value

```

Ở đây, toán tử  `->>` được gọi là "toán tử bỏ dấu ngoặc JSON."

## Index Cột JSON
Mặc dù cột JSON trong MySQL không thể được đánh index trực tiếp, nhưng có thể áp dụng đánh index trên một trường JSON cụ thể. Điều này có nghĩa là bạn có thể đánh index trên một số trường cụ thể của chuỗi JSON, nhưng không phải toàn bộ Object. Ví dụ:

```sql
ALTER TABLE has_json ADD INDEX my_index((json->>'$.key'));

```
Đoạn code trên tạo ra index trên trường `key` trong đối tượng JSON, cải thiện tốc độ của các truy vấn liên quan đến trường này.

## Khi nào và Tại sao sử dụng Cột JSON

Cột JSON mạnh mẽ nhưng không nên thay thế thiết kế schema truyền thống. Chúng hữu ích nhất trong những tình huống schema không có cấu trúc rõ ràng hoặc khi schema thay đổi thường xuyên. 

Ví dụ, JSON có thể hữu ích khi bạn lưu trữ dữ liệu từ các dịch vụ hoặc API của bên thứ ba, hoặc là các dữ liệu lồng nhau hoặc có cấu trúc phân cấp không phù hợp với thiết kế cơ sở dữ liệu quan hệ.

Một lưu ý là cột JSON có thể tốn nhiều tài nguyên, đặc biệt là với lượng lớn dữ liệu. Chỉ chọn dữ liệu cần thiết khi truy vấn và tránh lấy dữ liệu JSON một cách không cần thiết.

# Kết luận

Trong bài này, chúng ta đã đề cập đến việc tạo và kiểm tra chuỗi JSON, truy xuất dữ liệu bằng cách sử dụng toán tử, đánh index cột JSON. Cuối cùng, chúng ta hiểu hơn về các trường hợp sử dụng của chuỗi JSON và cung cấp một số hướng dẫn khi nào và tại sao lại sử dụng JSON trong MySQL.

Mặc dù mạnh mẽ, chúng ta cần sử dụng cột JSON một cách cẩn thận và phù hợp với các nguyên tắc thiết kế schema để đảm bảo ứng dụng hiệu quả và có thể mở rộng.


