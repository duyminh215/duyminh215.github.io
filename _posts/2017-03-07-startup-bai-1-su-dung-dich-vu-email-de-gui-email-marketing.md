---
layout: post
title: "[Startup] Bài 1: Sử dụng dịch vụ email để gửi email marketing"
category: startup
tags: [startup]
date: 2017-03-07
---

Xin chào các bạn,

Hôm nay mình sẽ bắt đầu một chuỗi bài chia sẻ kinh nghiệm của mình trong quá trình làm việc ở một startup.

Các bài chia sẻ này chỉ đứng dưới góc độ là người làm kĩ thuật và chủ yếu dành cho các bạn làm về kĩ thuật.

Đây đều là những vấn đề thực tế mình đã gặp trong quá trình phát triển sản phẩm cho một công ty startup công nghệ.

Mình muốn chia sẻ các kinh nghiệm này để giúp đỡ các bạn đang làm startup có thể không phải đối mặt với những vấn đề của mình và giải quyết các vấn đề được nhanh gọn hơn.

Mục đích chia sẻ không gì khác ngoài muốn giúp đỡ các bạn đang làm startup đi nhanh hơn, không cần mất quá nhiều thời gian để nghiên cứu và lựa chọn dịch vụ các bạn sử dụng.

Trong bài đầu tiên này mình sẽ chia sẻ kinh nghiệm chọn và sử dụng dịch vụ email mà các bạn muốn sử dụng để gửi email marketing.

Thông thường, khi làm startup, chúng ta sẽ thường yêu cầu người dùng đăng ký thông tin để sử dụng dịch vụ. Và một thông tin vô cùng quan trọng chính là email. Với thông tin email có được của người dùng, chúng ta có thể xác minh được người dùng đó là thật. Và quan trọng hơn là chúng ta sẽ gửi các email thông báo đến cho người dùng. Qua đó, giữ chân người dùng ở lại với dịch vụ của mình. Email là công cụ rất rẻ để có thể PING user.

Một vấn đề cho các bạn làm startup là lựa chọn dịch vụ gửi email trong hàng nghìn dịch vụ. Mình đã trải qua giai đoạn này nên mình biết. Đặc biệt là ở Việt Nam, các dịch vụ email của nước ngoài đều không support dẫn đến việc muốn sử dụng dịch vụ cũng rất khó khăn.

Qua thời gian tìm hiểu của mình thì ở Việt Nam, các bạn nên sử dụng dịch vụ email của Amazon SES (Amazon Simple Email Service ) và của Mandrill (một plugin của Mailchimp).

Amazon SES sẽ cho chúng ta gửi 62.000.000 email free một tháng nếu bạn sử dụng dịch vụ Amazon EC2 của họ.

Thực tế thì các bạn dùng Amazon SES sẽ dùng kiểu SMTP để gửi email. Tuy nhiên, có một điều là Amazon SES sẽ review việc gửi email ở Việt Nam rất chặt và thường sẽ bị block account.

Tóm lại, sử dụng Amazon SES ở Việt Nam cũng hơi khó khăn.

Mình suggest một service khác là Mandrill.

Mandrill trước đây là một startup ở trong Mailchimp và họ hoạt động độc lập. Tuy nhiên từ tháng 4-2016 họ đã tích hợp Mandrill thành một plugin của Mailchimp.

Một điều cũng gây khó khăn là Mandrill không cho phép đăng ký với IP ở Việt Nam. Nhưng mình đã thử proxy và dùng IP của Mỹ thì Mandrill đã cho phép đăng ký thông tin. Sau khi đăng ký được account, các bạn phải nhập thông tin thẻ tín dụng thì có thể sử dụng Mandrill bình thường mà không cần qua proxy nữa.

Mandrill cho phép chúng ta gửi 2000 email free hàng tháng. Còn sau đó chúng ta sẽ phải trả phí. Giá của Mandrill các bạn tìm hiểu ở đây <a href="https://www.mandrill.com/pricing/">https://www.mandrill.com/pricing/</a>. Ở thời điểm bài viết này thì Mandrill bán theo block 25.000 email với giá $20. Phí này không quá đắt cho các bạn làm startup.

Và đặc biệt, Mandrill hỗ trợ các bạn gửi email bằng cả 2 hình thức là dùng API hoặc dùng SMTP.

Với cách dùng SMTP thì các bạn chỉ cần cài đặt tham số về địa chỉ, cổng thì có thể gửi đi email.

Với cách dùng gửi qua API thì Mandrill hỗ trợ rất nhiều ngôn ngữ để gửi. Các bạn xem qua các ngôn ngữ hỗ trợ qua API bằng cách xem link sau: <a href="https://mandrillapp.com/api/docs/">https://mandrillapp.com/api/docs/</a>.

Công ty mình đang làm việc sử dụng Java nên mình suggest các bạn sử dụng API sau: <a href="https://github.com/rschreijer/lutung">https://github.com/rschreijer/lutung</a>.

Code để sử dụng rất đơn giản. Các bạn làm theo hướng dẫn trong link github là có thể gửi được. Mình sẽ làm một ví dụ cho các bạn:

```
MandrillApi mandrillApi = new MandrillApi("");
// create your message
MandrillMessage message = new MandrillMessage();
message.setSubject("Hello World!");
message.setHtml("Hi pal!Really, I'm just saying hi!");
message.setAutoText(true); 
message.setFromEmail("kitty@yourdomain.com"); 
message.setFromName("Kitty Katz"); 
// add recipients 
ArrayList recipients = new ArrayList(); 
Recipient recipient = new Recipient(); 
recipient.setEmail("claireannette@someotherdomain.com"); 
recipient.setName("Claire Annette"); 
recipients.add(recipient); 
recipient = new Recipient(); 
recipient.setEmail("terrybull@yetanotherdomain.com"); 
recipients.add(recipient); 
message.setTo(recipients); 
message.setPreserveRecipients(true); 
ArrayList tags = new ArrayList(); 
tags.add("test"); 
tags.add("helloworld"); 
message.setTags(tags); 
// ... add more message details if you want to! 
// then ... send 
MandrillMessageStatus[] messageStatusReports = mandrillApi.messages().send(message, false);

```

Trên đây là một đoạn code để sử dụng Java API gửi mail qua Mandrill.

Các bạn nên set tag cho một đợt email mà chúng ta gửi đi. Ví dụ bạn chạy một campain vào ngày 8-3 thì chúng ta đặt tên cái tag đó đơn giản là "campain_8_3" thì sau này, lúc mà muốn xem lại kết quả, các bạn chỉ cần chọn tag đó và nó sẽ hiển thị cho chúng ta.

<img class="alignnone  wp-image-141" src="http://hoctuduylaptrinh.com/wp-content/uploads/2017/03/mandrill-300x169.png" alt="" width="792" height="446" />

Một điều rất hay của Mandrill là báo cáo của nó rất chi tiết và bạn sẽ đánh giá được hiệu quả của việc gửi email hay không thông qua tỉ lệ mở, tỉ lệ click vào email và còn nhiều thông số khác nữa.

Các bạn có thể sử dụng dịch vụ này để làm nhiệm vụ gửi email cho startup của mình.

Trên đây là chia sẻ của mình về dịch vụ gửi mail.

Mình sẽ còn trở lại với các bài viết chia sẻ kinh nghiệm nữa.

Cảm ơn các bạn đã theo dõi.

Hẹn gặp lại các bạn ở bài viết tiếp theo.
