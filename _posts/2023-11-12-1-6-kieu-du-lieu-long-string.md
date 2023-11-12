---
layout: post
title: "MySQL cho developer 1.6: Kiểu dữ liệu Long String"
category: MySQL
tags: [MySQL, MySQL for developer]
date: 2023-11-12
---
# Long String trong MySQL

Khi nói về quản lý dữ liệu trong MySQL, có một số loại cột có thể sử dụng để lưu các loại dữ liệu khác nhau. Trong bài viết này, chúng ta sẽ tập trung vào cột `TEXT` và `BLOB`, được sử dụng để lưu trữ văn bản lớn và dữ liệu nhị phân lớn. Chúng ta sẽ xem xét kỹ hơn lý do khiến những cột này tối ưu hơn so với các loại dữ liệu khác và xem xét kỹ hơn các loại dữ liệu này.

## Cột String

Cột `TEXT` được sử dụng để lưu trữ dữ liệu ký tự, chẳng hạn như chuỗi văn bản. Khác với các loại dữ liệu chuỗi khác mà chúng ta đã đề cập trước, cột `TEXT` cho phép bạn lưu trữ lượng dữ liệu lớn hơn nhiều, làm cho chúng trở thành một lựa chọn tuyệt vời để lưu trữ các đoạn văn bản dài. Tuy nhiên, lưu ý rằng các cột văn bản không thể được đánh index (trừ khi sử dụng full text index) và không thể sắp xếp theo giá trị đầy đủ của chúng. Một giải pháp tạm thời là chỉ đánh index một tiền tố của các cột hoặc sắp xếp chỉ theo một vài nghìn ký tự đầu tiên.

Có bốn loại cột văn bản trong MySQL: `TINYTEXT`, `TEXT`, `MEDIUMTEXT`, và `LONGTEXT`. Như tên gọi, mỗi loại có một giới hạn cho lượng dữ liệu nó có thể giữ. Cột `TINYTEXT` có thể giữ tối đa 255 ký tự, trong khi cột `LONGTEXT` có thể giữ lên đến 4 gigabyte dữ liệu.

## Cột BLOB

Các cột `BLOB`, ngược lại, được sử dụng để lưu trữ dữ liệu nhị phân. Chúng giống với các cột `TEXT` ở chỗ cho phép bạn lưu trữ lượng dữ liệu lớn hơn nhiều so với các loại dữ liệu khác. Tuy nhiên, các cột `BLOB` không có bảng ký tự hoặc collations như các cột `TEXT`.

Giống như cột `TEXT`, có bốn loại cột blob: `TINYBLOB`, `BLOB`, `MEDIUMBLOB`, và `LONGBLOB`. Chúng khác nhau về lượng dữ liệu chúng có thể lưu trữ, với cột `LONGBLOB` có thể lưu trữ lên đến 4 gigabyte dữ liệu.

## Lưu Trữ Tệp Trong Các Cột BLOB

Mặc dù các cột `BLOB` có thể giữ dữ liệu nhị phân như hình ảnh hoặc tệp âm thanh, nhưng không nên lưu trữ chúng trong cơ sở dữ liệu. Thông thường, tốt hơn là lưu trữ các loại tệp này ở nơi khác và lưu url trong `VARCHAR` đến file đó.

## Cách sử dụng

Khi sử dụng các cột văn bản hoặc blob, quan trọng là cân nhắc đến hai việc: bao nhiêu dữ liệu bạn cần lưu trữ và làm thế nào bạn sẽ truy cập dữ liệu đó. Dưới đây là một số cách sử dụng tốt nhất để cân nhắc:

- **Chỉ chọn các cột bạn cần:** Bởi vì cột `TEXT` và `BLOB` lưu trữ dữ liệu rất lớn trên ổ đĩa, do đó chỉ chọn chúng khi thực sự cần thiết. Tái cấu trúc dữ liệu của bạn để cột `BLOB` có thể được kết hợp khi cần.

- **Không đánh index hoặc sắp xếp toàn bộ cột:** Bởi vì kích thước của cột `TEXT` và `BLOB` lớn, việc đánh index hoặc sắp xếp trên toàn bộ cột không khả thi. Bạn chỉ nên đánh index hoặc sắp xếp trên một phần của cột.

- **Sử dụng cột `VARCHAR` cho lượng dữ liệu nhỏ:** Nếu bạn chỉ cần lưu trữ vài trăm ký tự, hãy xem xét việc sử dụng `VARCHAR` thay vì các cột văn bản. Điều này có thể giúp việc đánh index và sắp xếp tối ưu hơn.

## Kết Luận

Tóm lại, các cột `TEXT` và `BLOB` là các loại dữ liệu hữu ích trong MySQL để lưu trữ lượng lớn văn bản và dữ liệu nhị phân. Chúng có các biến thể khác nhau tùy thuộc vào lượng dữ liệu bạn cần lưu trữ. Mặc dù chúng có lợi ích về mặt lưu trữ, quan trọng là tuân thủ các cách sử dụng tối ưu để tránh các vấn đề tiềm ẩn liên quan đến việc đánh index, sắp xếp và tốc độ truy xuất.
