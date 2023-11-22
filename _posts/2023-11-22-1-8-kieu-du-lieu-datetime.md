---
layout: post
title: "MySQL cho developer 1.8: Kiểu dữ liệu Dates"
category: MySQL
tags: [MySQL, MySQL for developer]
date: 2023-11-22
---
# Hiểu về Các Kiểu Dữ Liệu Thời Gian trong MySQL: Lưu Trữ Dữ Liệu Thời Gian

Khi cơ sở dữ liệu MySQL của bạn phức tạp hơn, việc hiểu rõ về các kiểu dữ liệu khác nhau được sử dụng để lưu trữ các loại thông tin khác nhau trở nên ngày càng quan trọng. Trong bài này, chúng ta sẽ xem xét cụ thể về việc lưu trữ dữ liệu liên quan đến thời gian trong MySQL và khám phá năm kiểu dữ liệu khác nhau mà bạn có thể sử dụng cho mục đích này.

## Sự Quan Trọng của Dữ Liệu Thời Gian

Trước khi chúng ta nghiên cứu về các kiểu dữ liệu khác nhau được sử dụng để lưu trữ dữ liệu thời gian, điều quan trọng là phải hiểu liệu bạn có cần phải lưu trữ dữ liệu thời gian không. Tùy thuộc vào ứng dụng của bạn, bạn có thể cần lưu trữ các ngày, giờ, timestamps, năm hoặc dữ liệu thời gian khác.

Vì vậy, câu hỏi đầu tiên bạn cần đặt ra cho chính mình là, "Liệu tôi có cần phải lưu trữ **thời gian** không?" Nếu bạn chỉ cần lưu trữ ngày, thì bạn sẽ cần nhìn vào các kiểu dữ liệu khác nhau so với khi bạn cần lưu trữ cả ngày và giờ.

## Năm Kiểu Dữ Liệu Khác Nhau để Lưu Trữ Dữ Liệu Thời Gian

Hãy xem xét cẩn thận năm kiểu dữ liệu khác nhau mà bạn có thể sử dụng để lưu trữ dữ liệu thời gian trong MySQL.

### DATE

Nếu bạn chỉ cần lưu trữ ngày, thì cột kiểu `DATE` là sự lựa chọn tốt nhất của bạn. Đây là một kiểu dữ liệu có kích thước ba byte có thể lưu trữ một loạt dữ liệu rộng từ năm 1,000 đến 9,999.

### DATETIME

Nếu bạn cần lưu trữ cả ngày và giờ, thì `DATETIME` và `TIMESTAMP` là hai lựa chọn bạn có. `DATETIME` là một kiểu dữ liệu tám byte có thể lưu trữ một dải dữ liệu lớn. Do đó, nếu bạn cần lưu trữ dữ liệu thời gian đến năm 9,999, `DATETIME` là lựa chọn phù hợp.

### TIMESTAMP

`TIMESTAMP`, ngược lại, là một kiểu dữ liệu bốn byte có thể lưu trữ một dải dữ liệu hạn chế, từ năm 1970 đến 2038-01-19. Hạn chế này được gọi là "vấn đề 2038". Nếu bạn chỉ cần lưu trữ dữ liệu thời gian trong khoảng này, `TIMESTAMP` là lựa chọn hiệu quả và gọn nhẹ hơn.

### YEAR

Nếu bạn cần lưu trữ một năm từ 1901 đến 2155, `YEAR` sẽ là cách gọn nhẹ nhất để thực hiện điều này. Kiểu này không được sử dụng phổ biến.

### TIME

Kiểu dữ liệu `TIME` được sử dụng để lưu trữ giờ, phút và giây. Nó có thể lưu trữ nhiều hơn 24 giờ, điều này hữu ích để lưu trữ các khoảng thời gian. Kiểu này hữu ích cho một khoảng thời gian 10 ngày được đặt bằng giờ, phút và giây, nhưng không phổ biến.

## Lựa Chọn Giữa DATETIME và TIMESTAMP

Nếu bạn cần lưu trữ cả ngày và giờ, bạn sẽ cần lựa chọn giữa `DATETIME` và `TIMESTAMP`. Cả hai kiểu dữ liệu đều có ưu điểm và nhược điểm của mình, vì vậy quan trọng là phải hiểu rõ sự khác biệt giữa chúng.

### Kích thước lưu trữ

Sự khác biệt đầu tiên giữa `DATETIME` và `TIMESTAMP` là kích thước lưu trữ. `DATETIME` là một kiểu dữ liệu tám byte, trong khi `TIMESTAMP` là một kiểu dữ liệu bốn byte. Điều này làm cho `TIMESTAMP` gọn nhẹ và hiệu quả hơn về mặt không gian lưu trữ.

### Phạm vi của Dữ Liệu

Sự khác biệt thứ hai giữa hai kiểu dữ liệu này là phạm vi của dữ liệu mà chúng có thể lưu trữ. Như đã đề cập trước đó, `DATETIME` có thể lưu trữ dữ liệu thời gian đến năm 9,999. Ngược lại, `TIMESTAMP` chỉ có thể lưu trữ dữ liệu từ năm 1970 đến 2038.

Do hạn chế này, bạn có thể phải sử dụng `DATETIME` trong các trường hợp bạn cần lưu trữ dữ liệu vượt quá năm 2038.

### Múi giờ

Một khác biệt cuối cùng giữa `DATETIME` và `TIMESTAMP` là cách chúng xử lý múi giờ. Với `DATETIME`, MySQL không xử lý múi giờ. Bất cứ điều gì bạn insert vào, bạn sẽ nhận lại đúng như vậy. Với `TIMESTAMP`, MySQL cố gắng giúp bạn bằng cách chuyển đổi giá trị sang giờ UTC khi thêm vào cơ sở dữ liệu và quay lại múi giờ của bạn khi lấy ra.

Sự khác biệt này quan trọng để xem xét khi lựa chọn giữa hai kiểu dữ liệu này, đặc biệt là nếu ứng dụng của bạn yêu cầu xử lý các múi giờ khác nhau.

## Kết Luận

Khi nói đến việc lưu trữ dữ liệu liên quan đến thời gian trong MySQL, quan trọng là phải chọn đúng kiểu dữ liệu dựa trên nhu cầu của bạn. Các kiểu dữ liệu `DATE`, `DATETIME`, và `TIMESTAMP` là những kiểu dữ liệu phổ biến nhất, với `TIMESTAMP` là cách hiệu quả và gọn nhẹ nhất để lưu trữ dữ liệu thời gian cả ngày lẫn giờ.

Khi lựa chọn giữa `DATETIME` và `TIMESTAMP`, hãy xem xét kích thước lưu trữ, phạm vi dữ liệu cần thiết và cách xử lý múi giờ. Cuối cùng, sử dụng MySQL một cách hiệu quả để lưu trữ và xử lý dữ liệu thời gian có thể giúp ứng dụng của bạn hoạt động một cách hiệu quả và chính xác.
