---
layout: post
title: "Phương pháp để lập trình hiệu quả"
category: Programing
tags: [Programing]
date: 2017-01-04
---

Cá nhân mình chưa phải là một người lập trình quá xuất sắc hoặc có quá nhiều tip hay để có thể giới thiệu với mọi người. Tuy nhiên, mình cũng lập trình khá lâu (tính từ lúc đi học đại học thì cũng hơn 5 năm lập trình). Những phương pháp mà mình chia sẻ dưới đây là ở góc độ cá nhân. Và mình muốn chia sẻ để có thể giúp đỡ được các bạn nào chưa biết cách học. Các bạn có thể có nhiều phương pháp khác thì hãy chia sẻ và bàn luận bằng cách comment vào bên dưới bài viết.

Cá nhân mình thấy phương pháp để học lập trình hiệu quả cần những kỹ năng sau.

***1.Kỹ năng phân tích, thiết kế***

Kỹ năng phân tích, thiết kế là như thế nào? Khi chúng ta nhận một yêu cầu từ người ra yêu cầu, các bạn cần phân tách nhỏ yêu cầu thành các bài toán nhỏ hơn. Từ các bài toán nhỏ hơn chúng ta sẽ chi tiết thành các hàm, các cấu trúc dữ liệu.

Một bài toán lập trình sẽ gồm hai thành phần quan trọng là giải thuật và dữ liệu. Do đó, khi chúng ta nhận yêu cầu từ người ra yêu cầu chúng ta cần phải phân tích và từ đó đi đến thiết kế dữ liệu cho bài toán, sau đó là thiết kế giải thuật. Trong thiết kế giải thuật chúng ta sẽ tách nhỏ thành các hàm lập trình. Trong mỗi hàm thì tùy vào mục đích của hàm, ta sẽ chi tiết hóa đến từng dòng code.

Tóm lại, kỹ năng phân tích thiết kế là cách chia nhỏ dần yêu cầu thành các bài toán nhỏ, từ các bài toán nhỏ thành các hàm.

***2. Kỹ năng tìm kiếm và nghiên cứu***

Khi lập trình, chúng ta không cần phải biết tất cả mọi hàm, API mà ngôn ngữ cung cấp vì thực tế số lượng hàm và API sẽ rất rất lớn. Nhưng mà những nhà lập trình họ đã có những tài liệu rất chi tiết cho chúng ta và chúng được chia sẻ rộng rãi trên Internet.

Do đó, chúng ta hoàn toàn có thể tìm được câu trả lời của bài toán của mình trên Internet. Công cụ hữu hiệu nhất ở đây là Google. Lưu ý một điều là chúng ta không được lấy hoàn toàn code của người khác để đưa ra lời giải cho bài toán của mình. Chúng ta chỉ tìm kiếm những cái mà mình chưa biết (chủ yếu là các API hoặc các hàm đơn giản như convert unixtime to Date time), sau đó tự cá nhân chúng ta cần giải quyết bài toán của chính mình.

Trong thực tế, mỗi người sẽ nhận được những yêu cầu khác nhau và sẽ không có bài code nào hoàn thiện để giải quyết bài toán của bạn. Cái chúng ta cần là tìm những điều mình còn thiếu để giải quyết bài toán của mình. Hầu hết cái mà người lập trình hay tìm kiếm chính là các API. Một số ví dụ mà mình thường tìm kiếm trên Internet:

1. Cách chuyển unixtime thành date time

2. Cách push notification cho IOS hoặc Android

3. Cách lấy dữ liệu từ một url bằng python, java, ...

 ...
Tất cả những ví dụ trên đều là các hàm, API mà ngôn ngữ cung cấp nhưng chúng ta chưa biết. Cách tốt nhất là cứ google.

***3. Kỹ năng test và debug (xử lý lỗi)***

Hầu như không lập trình viên nào có thể viết code và chạy ngon ngay từ đầu. Thông thường, chúng ta sẽ mắc lỗi khi thử chạy chương trình. Điều đó là bình thường. Mắc lỗi và biết sửa lỗi, đó mới là điều quan trọng.

Một kỹ năng quan trọng không kém khi lập trình là test và debug. Chính các lập trình viên là những người hiểu rõ nhất chương trình của mình và biết được khả năng lỗi ở đâu là cao nhất. Do đó, các bạn cần phải test chương trình của chính bản thân mình trước khi đưa cho tester. Một cách test hay nhất là unit test. Đó là chúng ta phải test được tất cả các trường hợp xảy ra. Có rất nhiều kỹ thuật unit test, các bạn có thể search trên mạng. Cách mà mình hay áp dụng là test từng hàm của mình với các đầu vào khác nhau.

Cái quan trọng của test và debug là kỹ năng phân tích từng dòng lệnh. Chúng ta có rất nhiều công cụ để chạy qua từng dòng lệnh và kiểm tra chương trình. Hoặc chính các bạn sẽ phải phân tích được từng dòng code của mình.

Khi mà đã biết cách test và debug chương trình, bạn sẽ sửa chương trình để nó chạy đúng với thiết kế mà bạn mong muốn.

Trên đây là một số kỹ năng mà mình thấy quan trọng trong quá trình lập trình. Có thể với các bạn là chưa đủ hoặc không chính xác. Các bạn có thể góp ý với mình bằng cách comment vào bên dưới bài viết. Mình rất mong nhận được góp ý từ các bạn.
