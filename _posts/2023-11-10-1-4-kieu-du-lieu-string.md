---
layout: post
title: "MySQL cho developer 1.4: Kiểu dữ liệu String"
category: MySQL
tags: [MySQL, MySQL for developer]
date: 2023-11-10
---
# Hiểu về các loại dữ liệu String, kích thước cột, bảng mã ký tự và collations trong MySQL

Khi nói đến việc lưu trữ String trong MySQL, có nhiều loại để sử dụng. Trên thực tế, MySQL có nhiều loại đến mức có thể cần nhiều video để cover tất cả. Trong video này, chúng ta sẽ xem xét một tổng quát về các loại String và sau đó đi sâu hơn vào hai loại cụ thể: String độ dài cố định và String độ dài thay đổi.

## Các loại String trong MySQL

Khi đến việc lưu trữ String trong MySQL, có nhiều loại để lựa chọn. Dưới đây là một danh sách các loại String:

- `CHAR`
- `VARCHAR`
- `TINYTEXT`
- `TEXT`
- `MEDIUMTEXT`
- `LONGTEXT`
- `BINARY`
- `VARBINARY`
- `TINYBLOB`
- `BLOB`
- `MEDIUMBLOB`
- `LONGBLOB`
- `ENUM`
- `SET`

Mặc dù có vẻ thừa thãi, điều quan trọng cần tập trung là hiểu sự khác biệt giữa String độ dài cố định và String độ dài thay đổi.

## String độ dài cố định

Các String độ dài cố định thường được sử dụng để lưu trữ dữ liệu có kích thước cố định. Điều này có thể là dữ liệu như tiền tố hai chữ số, băm MD5, hoặc số sê-ri có chữ số và chữ cái. Các String độ dài cố định được khai báo bằng kiểu dữ liệu `CHAR` và yêu cầu bạn khai báo kích thước cột.

```sql
CREATE TABLE strings (
  fixed_five CHAR(5),
  fixed_32 CHAR(32)
);
```
Trong ví dụ trên, chúng ta đã tạo hai String độ dài cố định. Cột fixed_five có thể lưu trữ tối đa năm ký tự, trong khi cột fixed_32 có thể lưu trữ tối đa 32 ký tự. Lưu ý rằng, bất kể số ký tự bạn lưu trữ trong một String độ dài cố định, nó sẽ luôn chiếm toàn bộ lượng dữ liệu được khai báo.
VD: Nếu bạn insert vào bảng strings trên với câu lệnh sau: 

```sql
INSERT INTO strings(`fixed_five`, `fixed_32`) VALUES("a", "B");
```

Thì khi bạn select bằng câu lệnh:

```sql
SELECT * FROM  strings;
```

Bạn sẽ nhận được kết quả như sau: 

```bash
| fixed_five    | fixed_32  |
|---------------|-----------|
| a             | B         |
```

## String độ dài thay đổi

String độ dài thay đổi, ngược lại, không có kích thước cố định. Số lượng dữ liệu yêu cầu phụ thuộc vào dữ liệu được lưu trữ trong cột. String độ dài thay đổi được khai báo bằng kiểu dữ liệu `VARCHAR`, và bạn phải chỉ định kích thước cột tối đa.

```sql
CREATE TABLE strings (
  variable_length VARCHAR(100)
);
```

Trong ví dụ trên, chúng ta đã tạo một String có độ dài thay đổi có thể lưu trữ tối đa 100 ký tự. Vì các String có độ dài thay đổi không chiếm toàn bộ không gian được chỉ định, chúng có thể hiệu quả hơn khi lưu trữ. Tuy nhiên, quan trọng là chúng ta phải chọn kiểu dữ liệu nhỏ nhất có thể để lưu trữ.

## Bảng mã ký tự và collations

Một bảng mã ký tự xác định những ký tự nào được phép lưu vào một cột. MySQL hỗ trợ một loạt các bảng mã ký tự, mà bạn có thể xem từ cơ sở dữ liệu `information_schema`. `utf8` và `utf8mb4` là những bảng mã ký tự bạn có thể sử dụng, với `utf8mb4` là bảng mã mặc định trong MySQL 8.

Ngược lại, collations quyết định cách hai hoặc nhiều chuỗi được so sánh hoặc sắp xếp. Một collations là một nhóm quy tắc quyết định liệu hai chuỗi có tương đương hay không. So sánh mặc định cho MySQL 8 là `utf8mb4_0900_ai_ci`, với `ai` (accent insensitive) không phân biệt không dấu và có dấu, và `ci` (case insensitive) có nghĩa là không phân biệt chữ hoa chữ thường.

```sql
CREATE TABLE strings (
  variable_length VARCHAR(100) CHARSET utf8mb4 COLLATE utf8mb4_general_ci
);
```

Trong ví dụ trên, chúng ta đã tạo một cột `VARCHAR` với bảng mã `utf8mb4` và collations `utf8mb4_general_ci`.

## Kết luận
Khi nói đến việc lưu trữ chuỗi trong MySQL, việc hiểu sự khác biệt giữa String độ dài cố định và String có độ dài thay đổi là quan trọng. Ngoài ra, bảng mã ký tự và collations đóng một vai trò quan trọng trong việc xác định ký tự có thể được lưu trong một cột và cách so sánh hoặc sắp xếp các chuỗi khác nhau. Hãy lưu ý rằng đối với một số thao tác nhất định, MySQL phân bổ bộ nhớ dựa trên kích thước tối đa của cột, nên quan trọng là chọn kiểu dữ liệu nhỏ nhất có thể cho dữ liệu bạn sẽ lưu trữ.