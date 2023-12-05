---
layout: post
title: "MySQL cho developer 2.1: Giới thiệu về index"
category: MySQL
tags: [MySQL, MySQL for developer]
date: 2023-12-05
---

# Đánh index: cơ sở của tối ưu cơ sở dữ liệu

Đến thời điểm này của khóa học, bạn đã rất quen thuộc với việc thiết kế  cấu trúc bảng (schema)! Việc thiết lập schema cơ sở dữ liệu của bạn là về việc xây dựng nền tảng cho cơ sở dữ liệu của bạn. Nhưng khi điều đó đã được thực hiện, bước tiếp theo là tập trung vào việc đánh index. Index là cách tốt nhất để đảm bảo rằng các truy vấn của bạn hoạt động tốt, nó rất quan trọng cho một ứng dụng hoạt động mượt mà. Trong thực tế, index quan trọng gấp mười lần so với thiết kế schema về mặt tối ưu! Có thể là quan trọng gấp trăm lần.

Trong video này, chúng tôi sẽ cung cấp cho bạn một cái nhìn tổng quan về Index, các đặc điểm của Index và một số quy tắc để đánh index.

## Đặc điểm của Index

Index là một cấu trúc dữ liệu hoàn toàn riêng biệt với dữ liệu của bạn. Khi bạn tạo một index, nó tạo ra một cấu trúc dữ liệu thứ hai, khác với cấu trúc dữ liệu chính của bạn (bảng). Lưu ý, mỗi Index giữ một bản sao của một phần dữ liệu của bạn, điều này có nghĩa là nếu bạn có nhiều Index, sẽ có nhiều bản sao của các phần khác nhau của dữ liệu của bạn.

Hơn nữa, Index có một con trỏ để trỏ đến một row trong dữ liệu. Nó rất cần thiết để Index biết cách lấy lại data của row trong bảng.

## Quy tắc để đánh index

Đối với quy tắc đánh index, bạn nên cố gắng tạo nhiều Index nhất có thể. Index là công cụ tốt nhất để tạo truy vấn nhanh, có nghĩa là ứng dụng sẽ rất nhanh và mượt. Tuy nhiên, bạn cũng nên tạo ít Index nhất có thể vì việc tạo quá nhiều Index có thể ảnh hưởng đến hiệu suất dữ liệu.

Quan trọng là phải thiết lập một sự cân bằng giữa số lượng Index bạn cần và số ít mà bạn sử dụng để vẫn tối ưu được. Việc thiết lập sự cân bằng này phụ thuộc vào kích thước của cơ sở dữ liệu, tần suất cập nhật và các yếu tố khác có thể ảnh hưởng đến hiệu suất của ứng dụng. Với hiểu biết này, bạn phải xem xét các pattern để quyết định đánh index nào.

## Tạo Index tối ưu

Khác với thiết kế schema, bạn không thể nhìn vào dữ liệu của mình và quyết định đánh index gì cho bảng của mình. Thay vào đó, bạn phải xem xét các truy vấn (query) của mình để xác định Index nào sẽ hoạt động tốt nhất. Nói cách khác, việc đánh index nên phụ thuộc vào các access pattern của ứng dụng.

Nếu bạn là một lập trình viên đang viết các access pattern cho ứng dụng, bạn là ứng viên tốt nhất để thiết kế Index. Bạn hiểu rõ về những access pattern là gì và có thể đánh index phù hợp.

## Kết luận

Index là yếu tố quan trọng cho tối ưu cơ sở dữ liệu. Sau khi bạn đã thiết kế schema của mình, Index là bước tiếp theo. Hiểu rõ các đặc điểm và quy tắc để đánh index là chìa khóa để xây dựng một cơ sở dữ liệu tối ưu cao. Hãy nhớ rằng việc đánh index nên được phụ thuộc các mô hình truy cập và các lập trình viên thường là người có vị trí tốt nhất để thiết kế Index.

Hãy tiếp tục theo dõi những bài viết sâu hơn về Index, nơi chúng tôi sẽ giải thích cách Index hoạt động bên trong, cách tạo chúng, điều gì tạo nên một Index tốt, và điều gì tạo nên một Index kém.
