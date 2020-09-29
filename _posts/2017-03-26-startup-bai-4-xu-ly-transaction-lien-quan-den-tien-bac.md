---
layout: post
title: "[Startup] Bài 4: Xử lý transaction liên quan đến tiền bạc"
category: startup
tags: [startup]
date: 2017-03-26
---

Tiếp tục về chuỗi bài kinh nghiệm làm startup cho các bạn.

Với công nghệ ngày càng phát triển ở Việt Nam, thì các ứng dụng liên quan đến tài chính ngày càng nhiều.

Tuy nhiên, ứng dụng liên quan đến tài chính, tiền bạc cần phải phân tích, thiết kế và chạy phải chuẩn xác.

Vì nếu sai lệch thì dẫn đến hậu quả rất nghiêm trọng cho hệ thống, có thể gây ra mất rất nhiều tiền.

Một trong những bài toán kinh điển của ứng dụng liên quan đến tài chính là xử lý transaction để đảm bảo data được sync một cách chuẩn xác.

Hôm nay, mình sẽ nêu ra một số kinh nghiệm khi làm việc với ứng dụng liên quan đến tài chính.

***1. Bạn phải hiểu rõ nghiệp vụ trước khi làm***

Một điều vô cùng quan trọng của ứng dụng liên quan đến tài chính là bạn cần phải nắm rất rõ nghiệp vụ của nó.

Và điều quan trọng là nghiệp vụ liên quan đến ngân hàng.

Ví dụ như sau, khi user rút tiền, bạn cần phải trừ ngay số tiền user rút trong tài khoản của họ. Sau đó, chúng ta mới tiến hành chuyển tiền cho user. Đồng thời ghi nhận 1 bản ghi ghi rõ lý do thay đổi tài khoản, ghi lại số tiền trước lúc thay đổi, sau khi thay đổi và số tiền thay đổi. Việc này sẽ tránh việc user có thể rút nhiều lần nếu chúng ta không trừ ngay tài khoản của họ. Nếu giả sử chúng ta không gửi tiền đến được cho user thì cần làm một bản ghi để trả lại tiền cho user trong tài khoản của họ.

***2. Đảm bảo tính toàn vẹn dữ liệu khi thực hiện transaction:***

Một điều vô cùng quan trọng khi làm việc với các ứng dụng liên quan đến tiền bạc là bạn cần phải thực hiện synchronize data. Tức là khi user thực hiện một transaction, chúng ta phải làm rất nhiều việc như trừ tiền của user, tạo bản ghi lý do trừ tiền, ...Tất cả những việc trên chúng ta phải đặt nó trong một transaction của cơ sở dữ liệu.

Nghĩa là, chỉ cần một trong các action đó bị lỗi thì transaction bị lỗi tất, còn nếu tất cả đều ổn thì mới cho lưu vào dữ liệu.

Với cơ sở dữ liệu MySQL và code dùng Java thì bạn có kĩ thuật transaction trên multi database hoặc multi table.

Tại sao chúng ta cần phải để tất cả các action đó vào một transaction?

Vì chúng ta cần phải đảm bảo toàn vẹn dữ liệu. Không thể có chuyện trừ tiền của user mà không ghi rõ lý do trừ là gì, hoặc có một bản ghi trừ tiền nhưng tài khoản của user vẫn chưa bị trừ. Nếu không để tất cả vào trong 1 transaction thì sẽ xảy ra lệch dữ liệu, khiến cho hệ thống hoạt động sai.

Một câu mình hay nói với bản thân khi làm việc liên quan đến transaction tiền bạc là "Được thì được cả, lỗi một thì lỗi tất". Tức là, tất cả các action liên quan đến dữ liệu thành công thì mới commit, sai một cái thì rollback lại cơ sở dữ liệu. Các bạn hãy search từ khóa "MySQL transaction" để hiểu rõ thêm về cái này. Đối với Java thì các bạn search "transaction in multi table mysql java" hoặc "transaction in multi database mysql java".

***3. Lưu ý khi sử dụng load balancer với transaction:***

Một kĩ thuật kinh điển trong việc scale hệ thống của các bạn là instance multi application servers.

Tuy nhiên, liên quan đến xử lý tiền bạc trên nhiều application server là phải rất chú ý.

Ví dụ, một user họ rút tiền thì họ sẽ gửi một request rút tiền lên server.

Lúc này server loadbalancer sẽ đón request đó và phân phối đến các instance application servers khác nhau. Tuy nhiên, load balancer có rất nhiều kĩ thuật. Nếu có một application server bị chậm là server 1, load balancer gửi request rút tiền đó đến server 1 nhưng nó phản hồi chậm, load balancer sẽ gửi tiếp request đó đến server 2. Xảy ra tình trạng cả 2 server sẽ đều xử lý việc rút tiền cho user. Điều này rất nguy hiểm gây ra sai lệch hệ thống.

Do đó, với các transaction liên quan đến tiền bạc, chúng ta áp dụng load balancer chỉ gửi đến server một lần, chứ không nên retry lại request đó.

***4. Chống duplicate request liên quan đến tiền bạc:***

Một điều rất dễ xảy ra khi xử lý transaction là gọi request liên tục.

Ví dụ, một user sẽ gửi yêu cầu rút tiền đến cho server, nếu chúng ta không có phương pháp chống duplicate request thì user rất dễ vô tình ấn nút rút tiền nhiều lần liên tục. Việc này gây ra hậu quả là nếu cơ sở dữ liệu không cập nhật kịp thời thì có thể sẽ xử lý nhiều lần mà data thì chưa thay đổi.

Để chống duplicate request thì cần phải xử lý cả trên client và server.

Đối với client, khi thực hiện các request liên quan đến tiền bạc thì khi user ấn nút xong thì phải disable cái nút đó luôn.

Đối với server, cần phải lock lại các request sau, chờ request đầu thực hiện xong thì mới thực hiện tiếp. Chúng ta có thể sử dụng cache in memory hoặc dùng transaction mysql để lock bảng liên quan đến tài khoản user.

Tương tự như ở phần 3, chúng ta cũng cần chống duplicate request với nhiều server đối với load balancer.
