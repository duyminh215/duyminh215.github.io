---
layout: post
title: "MySQL cho developer 1.3: Kiểu dữ liệu Decimal"
category: MySQL
tags: [MySQL, MySQL for developer]
date: 2023-11-09
---
# Lưu trữ số thập phân trong MySQL

Nếu bạn đang làm việc trên một dự án yêu cầu lưu trữ giá trị số thập phân, bạn có thể tự hỏi phương pháp tốt nhất cho MySQL là gì. Bạn không muốn có dữ liệu không chính xác hoặc không chính xác, và sự chọn lựa của bạn về loại dữ liệu có thể tạo ra sự khác biệt lớn. Trong bài này, chúng ta sẽ khám phá những lựa chọn khác nhau cho việc lưu trữ số thập phân trong MySQL và khi nào nên sử dụng mỗi loại.

## Bốn loại dữ liệu số thập phân

Có bốn loại dữ liệu khác nhau trong MySQL có thể lưu trữ giá trị số thập phân:

1. **DECIMAL**: một loại dữ liệu số  thập phân cố định lưu trữ giá trị chính xác.
2. **NUMERIC**: một alias cho DECIMAL, cả hai đều giống nhau trong MySQL.
3. **FLOAT**: một loại dữ liệu dấu chấm động lưu trữ giá trị xấp xỉ.
4. **DOUBLE**: một loại dữ liệu dấu chấm động lưu trữ giá trị lớn và chính xác hơn so với FLOAT.

Mỗi loại dữ liệu này đều có ứng dụng riêng của nó, và lựa chọn của bạn phụ thuộc vào độ chính xác bạn yêu cầu.

## Khi nào sử dụng DECIMAL

Nếu bạn cần lưu trữ giá trị yêu cầu độ chính xác tuyệt đối, chẳng hạn như tiền tệ hoặc dữ liệu tài chính khác, bạn nên sử dụng loại dữ liệu `DECIMAL`. Với `DECIMAL`, bạn có thể chỉ định số lượng chữ số tối đa và số lượng chữ số phải xuất hiện sau dấu thập phân.

Ví dụ, giả sử bạn muốn lưu trữ tối đa 10 chữ số, với hai chữ số sau dấu thập phân, cú pháp sẽ là:

```plaintext
DECIMAL(10,2)
```

Tham số đầu tiên chỉ định số lượng chữ số tối đa, trong khi tham số thứ hai chỉ định số lượng chữ số nên xuất hiện sau dấu thập phân. Số lượng chữ số trước dấu thập phân được xác định bằng giá trị đầu tiên trừ đi giá trị thứ hai.

## Khi nào sử dụng float hoặc double

Nếu bạn không cần giá trị thập phân chính xác, bạn có thể sử dụng cả `FLOAT` hoặc `DOUBLE`. Cả hai loại dữ liệu này lưu trữ giá trị xấp xỉ, nhưng `DOUBLE` có thể lưu trữ giá trị lớn hơn và chính xác hơn so với `FLOAT`.

Nếu bạn đang sử dụng một loại dữ liệu cho các tính toán khoa học, nơi độ chính xác tương đối quan trọng hơn độ chính xác tuyệt đối, bạn cũng có thể xem xét việc sử dụng `FLOAT` hoặc `DOUBLE`.

## Ví dụ

Hãy xem cách các loại dữ liệu này hoạt động trong thực tế. Chúng ta sẽ tạo một bảng có tên `decimals` và chèn dữ liệu vào hai cột `D1` và `D2`. Cả hai cột sẽ được định nghĩa là loại dữ liệu `DOUBLE`.

```sql
CREATE TABLE decimals (
  id INT AUTO_INCREMENT PRIMARY KEY,
  D1 DOUBLE,
  D2 DOUBLE
);
```
Sau đó, chúng ta sẽ chèn một số dữ liệu vào bảng:
```sql
INSERT INTO decimals (D1, D2)
VALUES (100.4, 20.4), (-80.0, 0.0);
```

Nếu chúng ta chạy một truy vấn SELECT để lấy tất cả dữ liệu trong bảng:

```sql
SELECT * FROM decimals;
```

Chúng ta sẽ thấy đầu ra như sau:

```bash
| id | D1    | D2  |
|----|-------|-----|
| 1  | 100.4 | 20.4|
| 2  | -80.0 | 0.0 |
```
Bây giờ, nếu chúng ta cố gắng cộng các giá trị trong cột D1 và D2, chúng ta có thể mong đợi kết quả là 40.8, nhưng đó không phải là điều chúng ta nhận được:

```sql
SELECT SUM(D1), SUM(D2) FROM decimals;
```
```bash
| SUM(D1)           | SUM(D2)    |
|-------------------|------------|
| 20.4000000000006  | 20.4       |
```

Chúng ta có thể thấy rằng tổng gần giống với kết quả mong đợi, nhưng không chính xác giống nhau, và đó là do DOUBLE là giá trị xấp xỉ của một số, không phải giá trị chính xác.

## Kết luận
Khi làm việc với giá trị thập phân trong MySQL, quan trọng là chọn loại dữ liệu đúng cho nhu cầu của bạn. Nếu bạn yêu cầu độ chính xác tuyệt đối trong giá trị của mình, DECIMAL là lựa chọn tốt nhất. Nếu bạn không cần giá trị chính xác, FLOAT hoặc DOUBLE có thể phù hợp hơn. Lựa chọn giữa FLOAT và DOUBLE phụ thuộc vào phạm vi dữ liệu bạn đang lưu trữ và mức độ chính xác bạn cần.

Hãy nhớ rằng khi làm việc với FLOAT hoặc DOUBLE, kết quả sẽ không chính xác đúng, và giá trị có thể khác một chút so với những gì bạn mong đợi.