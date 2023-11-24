---
layout: post
title: "MySQL cho developer 1.10: Các kiểu dữ liệu khác"
category: MySQL
tags: [MySQL, MySQL for developer]
date: 2023-11-24
---

# Các loại dữ liệu có thể bạn không ngờ đến

Là một lập trình viên, bạn có lẽ quen thuộc với nhiều loại dữ liệu khác nhau — chuỗi, số, ngày tháng và JSON, cùng những loại khác. Nhưng bạn có biết rằng có một số loại dữ liệu khá khác thường không? Trong bài này, chúng ta sẽ xem xét một số loại dữ liệu thú vị và kỳ lạ trong MySQL.

## MySQL Booleans

Bắt đầu với booleans. Mặc dù booleans là một loại dữ liệu phổ biến trong nhiều ngôn ngữ, nhưng MySQL thực sự không có một loại boolean native. Thay vào đó, MySQL sử dụng một cột `TINYINT` để mô phỏng giá trị boolean.

Tuy nhiên, bạn vẫn có thể sử dụng từ khóa `BOOLEAN` trong định nghĩa bảng của mình, nó sẽ được hiểu là một cột `TINYINT`. Từ khóa `BOOLEAN` chỉ là một cách viết tắt để tạo một cột int nhỏ, mặc định là null.

Bạn cũng có thể tạo một giá trị boolean bằng cách sử dụng một cột ký tự có độ dài bằng không, có thể là null. Tuy nhiên, phương pháp này ít được khuyến khích vì nó có thể làm cho dữ liệu của bạn trở nên rối bời và khó hiểu.

## Mã zip

Khi nói đến mã zip ở Hoa Kỳ, chúng luôn có 5 chữ số. Tuy nhiên, đôi khi những mã này cũng có thể bao gồm các số 0 đứng đầu. Nếu bạn lưu trữ những mã zip này dưới dạng số nguyên, bất kỳ số 0 đứng đầu nào cũng sẽ bị loại bỏ, dẫn đến mất dữ liệu.

Do đó, thường thì tốt hơn là lưu trữ mã zip dưới dạng chuỗi 5 ký tự. Tuy nhiên, nếu bạn cần lưu trữ một mã zip mở rộng (bao gồm một dấu gạch và 4 chữ số bổ sung), bạn sẽ cần tạo một cột chuỗi có độ dài 10 ký tự.

Quan trọng là phải hiểu rõ về dữ liệu khi nói đến mã zip, vì có ngoại lệ cho quy tắc. Ví dụ, có một cửa hàng Saks Fifth Avenue ở New York có mã zip riêng: "10022-SHOE." Luôn đảm bảo bạn hiểu rõ về dữ liệu trước khi quyết định cách lưu trữ nó.

### Địa chỉ IP

Cuối cùng, hãy xem xét địa chỉ IP. Mặc dù chúng thường xuất hiện dưới dạng chuỗi, bạn cũng có thể lưu trữ chúng dưới dạng số nguyên để tổ chức và phân tích tốt hơn.

MySQL có một hàm tích hợp sẵn là `INET_ATON()` chuyển đổi địa chỉ IPv4 thành số nguyên, và `INET_NTOA()` để chuyển đổi một số nguyên trở lại thành địa chỉ IP.

Nếu bạn cần hỗ trợ cả địa chỉ IPv4 và IPv6, bạn có thể cần sử dụng một cột nhị phân có độ dài 16 byte.

## Kết luận

Mặc dù những loại dữ liệu này có vẻ hơi lạ lẫm, chúng minh họa một điểm rằng bằng việc hiểu rõ về ý nghĩa của các loại dữ liệu và cách lưu trữ chúng hiệu quả, bạn có thể chuẩn bị cho mình thành công khi thực hiện truy vấn và phân tích dữ liệu sau này.

Vì vậy, hãy dành thời gian để khám phá dữ liệu của bạn, suy nghĩ về cách lưu trữ hiệu quả nhất và tận hưởng với những loại dữ liệu khác thường này. Bạn không bao giờ biết chúng có thể hữu ích như thế nào!
