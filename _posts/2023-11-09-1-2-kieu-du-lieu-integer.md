---
layout: post
title: "MySQL cho developer 1.2: Kiểu dữ liệu Integers"
category: MySQL
tags: [MySQL, MySQL for developer]
date: 2023-11-09
---
# Hiểu về số nguyên: loại và phạm vi

Khi nói đến cơ sở dữ liệu, một trong những điều quan trọng nhất là hiểu về các loại dữ liệu khác nhau có thể được sử dụng để lưu trữ thông tin. Trong bài viết này, chúng ta sẽ tập trung đặc biệt vào số nguyên (integer), các loại cột khác nhau có thể giữ giá trị số nguyên và phạm vi của mỗi loại.

## Bắt đầu

Để thể hiện các loại cột khác nhau có thể giữ giá trị số nguyên, chúng ta sẽ sử dụng một ví dụ đơn giản: một bảng lưu trữ thông tin cuốn sách. Bảng có một ID và một tiêu đề, và chúng ta sẽ xác định cột dữ liệu lưu số trang. Trước khi làm điều đó, chúng ta cần xác định loại dữ liệu và bất kỳ thuộc tính nào khác cần thiết.

## Loại cột có thể giữ giá trị số nguyên

Có năm loại dữ liệu có thể được sử dụng để lưu trữ số nguyên:

- TINYINT
- SMALLINT
- MEDIUMNINT
- INT
- BIGINT

Đáng chú ý rằng bất kỳ loại số nguyên nào bạn gặp phải có thể là các alias, có nghĩa là chúng chỉ là các từ khác nhau chỉ đến cùng một loại dữ liệu. Ví dụ, "integer" chỉ là một từ khác cho "int".

## Phạm vi cho mỗi loại dữ liệu

Mỗi loại dữ liệu số nguyên có yêu cầu lưu trữ khác nhau, điều này có nghĩa là chúng có thể lưu trữ lượng dữ liệu khác nhau. Dưới đây là phạm vi cho mỗi loại dữ liệu:

- TINYINT: Chiếm một byte và có thể lưu trữ giá trị từ 0 đến 255 (hoặc từ -128 đến 127 nếu hỗ trợ số âm).
- SMALLINT: Chiếm hai byte và có thể lưu trữ giá trị từ 0 đến 65,535 (nếu không hỗ trợ số âm).
- MEDIUMNINT: Chiếm ba byte và có thể lưu trữ giá trị từ 0 đến 16,777,215 (nếu không hỗ trợ số âm).
- INT: Chiếm bốn byte và có thể lưu trữ giá trị từ 0 đến 4,294,967,295 (nếu không hỗ trợ số âm).
- BIGINT: Chiếm tám byte và có thể lưu trữ giá trị từ 0 đến 18,446,744,073,709,551,615 (nếu không hỗ trợ số âm).

## Hiểu về số âm

Trong cơ sở dữ liệu, số âm được hỗ trợ bằng cách dành một trong các bit cho dấu (dương hoặc âm), với các bit còn lại dành cho giá trị. Ví dụ, một TINYINT với hỗ trợ số âm có một bit dành cho dấu và bảy bit cho giá trị, có nghĩa là nó có thể lưu trữ giá trị từ -128 đến 127.

## Xác định cột số trang

Đối với bảng lưu trữ thông tin cuốn sách của chúng ta, chúng ta sẽ xác định cột số trang, mà chúng ta kỳ vọng sẽ không bao giờ vượt quá 65,000 trang. Với điều này, chúng ta không cần sử dụng loại dữ liệu INT, có thể chứa đến 4.2 tỷ giá trị. Thay vào đó, chúng ta có thể sử dụng loại dữ liệu SMALLINT, chiếm hai byte và có thể lưu trữ giá trị từ 0 đến 65,535.

Tuy nhiên, chúng ta cũng cần chỉ định rằng không hỗ trợ số âm cho cột này. Chúng ta có thể làm điều này bằng cách thêm từ khóa unsigned, cho biết MySQL rằng chúng ta không quan tâm đến số âm.

## Các hiểu nhầm thông thường: INT(11)

Chúng ta thường thấy kiểu dữ liệu như INT(11) và cho rằng số 11 kiểm soát phạm vi dữ liệu có thể lưu trữ. Tuy nhiên, số trong dấu ngoặc đơn không ảnh hưởng đến lưu trữ cơ bản hoặc phạm vi của cột. Notation này chỉ được dự định để xác định chiều rộng hiển thị. Nó đã lỗi thời và sẽ sớm bị loại bỏ.

## Kết luận

Hiểu về các loại cột khác nhau có thể giữ giá trị số nguyên và phạm vi tương ứng của chúng là quan trọng để thiết kế một lược đồ cơ sở dữ liệu hiệu quả và có thể mở rộng. Bằng cách chọn loại dữ liệu phù hợp cho mỗi cột, chúng ta có thể tránh yêu cầu lưu trữ không cần thiết và đảm bảo truy vấn hiệu quả.
