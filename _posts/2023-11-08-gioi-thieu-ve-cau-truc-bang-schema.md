---
layout: post
title: "MySQL cho developer 1: Giới thiệu về cấu trúc bảng (Schema)"
category: MySQL
tags: [MySQL, MySQL for developer]
date: 2023-11-08
---
# Tầm quan trọng của thiết kế cấu trúc dữ liệu trong tối ưu cơ sở dữ liệu

Trước khi chúng ta đào sâu vào tối ưu hóa truy vấn, index (index) và những điều thú vị khác, hãy dừng lại một chút và nói về một khía cạnh thường bị bỏ qua trong tối ưu cơ sở dữ liệu: thiết kế cấu trúc bảng. Cấu trúc bảng đề cập đến cấu trúc của các bảng dữ liệu trong cơ sở dữ liệu của bạn, bao gồm các loại cột, kích thước và thuộc tính. Cấu trúc bảng của bạn có thể đặt bạn lên con đường thành công hoặc gây ra vấn đề sau này, vì vậy quan trọng phải bắt đầu đúng cách.

## Viết một cấu trúc bảng

Khi bạn tạo cấu trúc bảng của mình, bạn có hai lựa chọn: viết bằng tay hoặc để framework tạo ra. Mặc dù cả hai phương pháp đều hợp lệ, để framework tạo cấu trúc bảng có thể tiết kiệm thời gian và công sức. Tuy nhiên, quan trọng phải nhớ rằng dù bằng cách nào tạo cấu trúc bảng, bạn vẫn chịu trách nhiệm cuối cùng về nó.

MySQL cung cấp nhiều loại dữ liệu, và chúng ta sẽ bàn về hầu hết chúng chi tiết sau này. Nhưng trước khi điều đó, quan trọng phải nhớ ba nguyên tắc hướng dẫn sau, khi chọn loại dữ liệu:
1. Chọn loại dữ liệu nhỏ nhất có thể chứa tất cả dữ liệu của bạn.
2. Chọn loại cột đơn giản nhất mà phản ánh chính xác dữ liệu của bạn (ví dụ: sử dụng loại số cho số, không phải là string).
3. Đảm bảo rằng cấu trúc bảng của bạn phản ánh chính xác thực tế của dữ liệu của bạn (ví dụ: không biến một cột bắt buộc thành cột có thể để trống).

Bằng cách tuân thủ ba nguyên tắc này, bạn có thể tạo một cấu trúc bảng gọn nhẹ và tối ưu phản ánh chính xác dữ liệu của bạn.

## Tại sao thiết kế cấu trúc bảng quan trọng

Bạn có thể nghĩ, "ổ cứng rẻ, tại sao tính gọn lại quan trọng?" Mặc dù đúng rằng ổ cứng có giá rẻ, tính gọn có thể cải thiện tối ưu cơ sở dữ liệu một số cách:

- Truy cập dữ liệu nhanh hơn: Cấu trúc bảng càng gọn, cơ sở dữ liệu càng truy cập dữ liệu nhanh hơn. Điều này là do cơ sở dữ liệu không cần dành thời gian thêm để tìm kiếm dữ liệu trong các loại cột lớn hơn.
- Index hiệu quả: Khi đến lúc tạo index, một cấu trúc bảng gọn có thể cải thiện tốc độ và tối ưu index. Điều này là do index được lưu trữ trong bộ nhớ, và một cấu trúc bảng nhỏ hơn có nghĩa là sử dụng bộ nhớ ít hơn.

Nói cách khác, tối ưu hóa cấu trúc bảng không phải là về việc giảm thiểu sử dụng không gian đĩa, mà là về việc cho phép cơ sở dữ liệu truy cập và index dữ liệu của bạn một cách hiệu quả hơn.

## Các loại dữ liệu thông thường

Bây giờ khi chúng ta biết tại sao thiết kế cấu trúc bảng quan trọng, hãy xem xét cận cảnh một số loại dữ liệu thông thường trong MySQL:

- **INT**: Sử dụng cho giá trị số nguyên.
- **FLOAT** và **DOUBLE**: Sử dụng cho giá trị thập phân hoặc dấu phẩy động.
- **VARCHAR**: Sử dụng cho chuỗi (string) ký tự độ dài biến đổi.
- **DATE**, **DATETIME** và **TIMESTAMP**: Sử dụng cho giá trị ngày và thời gian.

Khi chọn loại dữ liệu, quan trọng phải xem xét dữ liệu của bạn và chọn loại đơn giản và nhỏ nhất mà phản ánh chính xác nó. Ví dụ, nếu bạn lưu trữ tuổi, bạn có thể chọn loại **INT** thay vì loại **VARCHAR**, vì giá trị số đơn giản và nhỏ gọn hơn.

## Kết luận

Mặc dù thiết kế cấu trúc bảng dữ liệu có thể không phải là việc nghe hay nhất của tối ưu cơ sở dữ liệu, nhưng nó là một phần quan trọng có thể ảnh hưởng đáng kể đến hiệu suất cơ sở dữ liệu của bạn. Bằng cách tuân theo ba nguyên tắc hướng dẫn về tính gọn, đơn giản và chính xác, bạn có thể tạo một cấu trúc bảng dữ liệu hiệu quả phản ánh chính xác dữ liệu của bạn và cho phép truy cập và index dữ liệu nhanh chóng.