---
layout: post
title: "[Startup] Bài 2: Kinh nghiệm đánh version cho ứng dụng"
category: startup
tags: [startup]
date: 2017-03-08
---

Xin chào các bạn,

Tiếp tục loạt bài về chia sẻ về kinh nghiệm làm startup của mình.

Trong bài này, mình sẽ chia sẻ kinh nghiệm để đánh version trên client và xử lý version đó trên phía server như thế nào.

Ngày nay, tốc độ phát triển ứng dụng diễn ra rất là nhanh. Qua đó việc quản lý ứng dụng bằng cách đánh version rất quan trọng. Đặc biệt hơn, chúng ta phải phát triển cho rất nhiều hệ điều hành khác nhau như iOS hay Android, ...

Trong bài viết này, mình xin chia sẻ kinh nghiệm đánh version của mình. Các bạn có thể tham khảo cách đánh version này và thay đổi một chút trong quá trình phát triển của các bạn.

<span style="color: #0000ff;">***1. Cách đánh version***</span>

Công ty mình hiện đang viết phần mềm cho mobile trên 2 hệ điều hành là iOS và Android.

Cách đánh version của mình như sau:

Mỗi version sẽ gồm 1 chuỗi 3 số cách nhau bởi dấu ".", ví dụ như: 1.1.12, 1.5.35, ...

Trong đó, số đầu tiên gọi là major version, số thứ hai là miner version và số thứ ba là prevesion.

Prevesion là các số thay đổi nhiều nhất, mỗi lần có bản release và sự thay đổi nhỏ hoặc sửa lỗi để up lên store thì số này thay đổi.

Số miner version thì sẽ thường thay đổi khi có một chức năng nào mới được release thì thay đổi số này.

Major version thường ít khi thay đổi, thường chỉ thay đổi khi có sự thay đổi lớn về mặt giao diện hoặc tính năng thay đổi rất nhiều.

Đó là cách đánh version.

<span style="color: #0000ff;">***2. Xử lý version khác nhau trên server:***</span>

Version không chỉ được đánh và giữ lại trên client mà còn phục vụ mục đích xử lý thông tin khác nhau trên phía server.

Một mẹo rất hay là các bạn nên gửi lên server thông tin của Hệ điều hành bằng cách đính vào header của http request. Ví dụ nếu Android thì chúng ta sẽ thêm 1 header vào http request là: "X-VERSION: Android-1.2.55", với iOS thì gửi lên "X-VERSION: iOS-1.2.60".

Và chú ý, chúng ta có thể phân biệt version ở 2 hệ điều hành bằng cách <span style="color: #0000ff;">đánh số prevesion của Android là số lẻ</span> - ví dụ như 55 ở trên, <span style="color: #0000ff;">prevesion của iOS là số chẵn</span> - ví dụ như 60 ở trên.

Lúc gửi thông tin lên server thì chúng ta sẽ đính kèm hệ điều hành và số version lên. Với các số version đó, phía server sẽ bóc tách thành 3 số. Từ 3 số version đó chúng ta sẽ xử lý thông tin khác nhau.

Ví dụ, ở bản Android-1.2.21 và iOS-1.2.30 chưa có chức năng đặt hàng. Version tiếp theo là Android-1.2.35 và iOS-1.2.40 thì sẽ có chức năng đặt hàng thì chúng ta chỉ cần check version lớn hơn 1.2.30 là sẽ có chức năng đặt hàng. Chúng ta chỉ cần đọc header version, phân tích số version và với một số dòng lệnh if else là ta đã có thể xử lý thông tin khác nhau cho các version client khác nhau rồi.

Đây cũng chính là lý do mình khuyên các bạn nên đánh version bằng số. Vì phía server, các bạn bóc tách số ra và so sánh sẽ nhanh hơn việc phải so sánh string.

Trên đây là kinh nghiệm đánh version và xử lý thông tin đối với version khác nhau trên phía server.

Các bạn có thể tham khảo cách đó hoặc tự các bạn thêm các thông tin vào version.

Hi vọng, các bạn sẽ có những ý tưởng khác để xử lý việc đánh version đơn giản và hiệu quả hơn.

Nếu có ý kiến nào hay các bạn hãy chia sẻ bằng cách comment vào bên dưới bài viết.

Cảm ơn các bạn đã theo dõi.

Hẹn gặp lại các bạn ở bài viết tiếp theo.
