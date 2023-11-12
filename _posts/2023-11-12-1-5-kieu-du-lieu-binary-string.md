---
layout: post
title: "MySQL cho developer 1.5: Kiểu dữ liệu Binary String"
category: MySQL
tags: [MySQL, MySQL for developer]
date: 2023-11-12
---
# Sức mạnh của cột binary và varbinary trong MySQL

Khi nói về MySQL, các cột CHAR và VARCHAR là những kiểu phổ biến nhất để lưu trữ giá trị String. Tuy nhiên, có các cột khác trong MySQL có thể lưu trữ giá trị kiểu như String, như cột BINARY và VARBINARY. Những cột này lưu trữ dữ liệu theo dạng byte thay vì ký tự, cho phép người dùng lưu trữ dữ liệu nhị phân, các đoạn bit dữ liệu nhị phân không thể được thể hiện dưới dạng String, hoặc không cần phải được lưu trữ theo kiểu dữ liệu đó.

## Hiểu về cột binary và varbinary

Các cột BINARY và VARBINARY khá giống với các cột CHAR và VARCHAR, với một số khác biệt chính. Trong khi các cột CHAR và VARCHAR lưu trữ các ký tự và phải khai báo kèm bảng mã ký tự và collations, còn các cột binary và VARBINARY chỉ lưu trữ byte. Nói cách khác, không có bảng mã ký tự hoặc collations nào phải quan tâm; nó chỉ là dữ liệu nhị phân thôi.

Cột BINARY là một cột có độ dài cố định, trong khi cột VARBINARY là một cột có độ dài thay đổi. Với các cột VARBINARY, bạn có thể lưu trữ đến một số byte đã khai báo, thay vì loại dữ liệu cố định. Mặc dù không được sử dụng rộng rãi, các loại dữ liệu BINARY và VARBINARY cung cấp một cách hiệu quả để lưu trữ dữ liệu nhị phân, chẳng hạn như các giá trị hash (băm) hoặc UUID.

## Cách sử dụng cột binary trong MySQL

Để minh họa cách sử dụng các cột binary trong MySQL, chúng ta sẽ sử dụng một ví dụ đơn giản: lưu trữ các giá trị hash. Để bắt đầu, chúng ta sẽ tạo một bảng với hai cột: một cột BINARY và một cột VARBINARY.

```sql
CREATE TABLE bins (
  bin BINARY(16),
  varbin VARBINARY(100)
);
```
Tiếp theo, chúng ta sẽ tạo một số dữ liệu nhị phân bằng cách sử dụng hàm MD5. Hàm này trả về giá trị băm MD5 của một chuỗi cụ thể. Ví dụ, băm MD5 của "hello" là "5d41402abc4b2a76b9719d911017c592". Chúng ta có thể chuyển đổi giá trị băm này thành dữ liệu nhị phân bằng hàm UNHEX.

```sql
SELECT UNHEX(MD5('hello'));
```

Đầu ra sẽ là biểu diễn giá trị nhị phân của giá trị hash, nhưng vẫn được hiển thị dưới dạng chuỗi HEX trong app client MySQL. Để xem dữ liệu nhị phân thực tế, chúng ta cần kết nối vào máy chủ MySQL bằng cách sử dụng CLI với cờ "skip binary as hex".


```sql
mysql --skip-column-names --skip-binary-as-hex -e "SELECT UNHEX(MD5('hello'))"
```
Đầu ra sẽ hiển thị dạng: "\x5d\x41\x40\x2a\xbc\x4b\x2a\x76\xb9\x71\x9d\x91\x10\x17\xc5\x92". Điều này cho thấy hàm đã tạo dữ liệu nhị phân đúng.

Bây giờ chúng ta đã có dữ liệu nhị phân, chúng ta có thể insert nó vào bảng đã tạo trước đó.

```sql
INSERT INTO bins (bin, varbin)
VALUES (UNHEX(MD5('hello')), UNHEX(MD5('hello')));
```
Để lấy dữ liệu, chúng ta có thể sử dụng truy vấn sau:

```sql
SELECT * FROM bins;
```
Dữ liệu sẽ hiển thị dưới định dạng nhị phân. Để đọc được dữ liệu, chúng ta có thể sử dụng hàm HEX.

```sql
SELECT HEX(bin), HEX(varbin) FROM bins;
```

Dữ liệu hiển thị dưới dạng chuỗi các ký tự HEX.

## Kết luận
Tóm lại, các cột BINARY và VARBINARY trong MySQL cung cấp một cách hiệu quả để lưu trữ dữ liệu nhị phân mà không phải String có thể đọc được. Bằng cách sử dụng các cột nhị phân, bạn có thể lưu trữ dữ liệu hash và UUID một cách gọn gàng hơn trên ổ cứng, mà không quan tâm đến bảng mã ký tự và collations. Mặc dù những cột này có thể không được dùng rộng rãi, nhưng chúng có thể quan trọng cho việc lưu trữ dữ liệu trong một số trường hợp cụ thể.
