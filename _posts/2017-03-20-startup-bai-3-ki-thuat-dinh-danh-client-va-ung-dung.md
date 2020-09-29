---
layout: post
title: "[Startup] Bài 3: Kĩ thuật định danh client (unique device) và ứng dụng"
category: startup
tags: [startup]
date: 2017-03-20
---

Xin chào các bạn,

Tiếp tục chuỗi bài về chia sẻ kinh nghiệm khi làm startup cho các bạn.

Hôm nay mình sẽ đi vào phần định danh client và ứng dụng của việc định danh client trong ứng dụng client - server.

<span style="color: #0000ff;">***1.Định danh client là gì?***</span>

Định danh client nghĩa là chúng ta sẽ dùng một kĩ thuật nào đó để xác định một client (điện thoại, máy tính, ...) là duy nhất. Qua đó chúng ta sẽ phân biệt được các device khác nhau khi có nhiều client gửi thông tin lên server.

<span style="color: #0000ff;">***2.Kĩ thuật định danh client:***</span>

Chúng ta sẽ có rất nhiều cách để định danh một client (máy tính, điện thoại).

Chúng ta có thể áp dụng một số cách như sau:

***a. Lấy thông tin về số seri của sản phẩm:***

Thông thường nhà sản xuất khi xuất xưởng một sản phẩm ra thị trường họ sẽ có một số seri để định danh sản phẩm đó. Số seri là số emei của sản phẩm. Trên Android thì việc này chúng ta có thể lấy được dễ dàng. Tuy nhiên trên iOS thì Apple đã chặn API để lấy emei sản phẩm. Trên windows thì kĩ thuật cũng phức tạp hơn.

***b. Lấy thông tin về địa chỉ MAC của sản phẩm:***

Một device khi xuất xưởng cũng có một địa chỉ MAC duy nhất. Địa chỉ MAC được sử dụng cho các client sử dụng kết nối mạng. Và chúng ta cũng đang nói đến các app đang sử dụng kết nối client-server.

Trên Android thì việc lấy địa chỉ MAC dễ hơn, trên iOS thì khó hơn.

***c. Lấy thông tin account của client:***

Ngày nay, mỗi thiết bị bán ra thường có một chợ ứng dụng đi kèm. Và người dùng muốn cài đặt app đều sử dụng một account để đăng nhập. Chúng ta có thể dựa vào thông tin này để định danh được client. Cách này có thể áp dụng cho cả Android và iOS.

***d. Dùng fingerprint của browser:***

Mỗi browser sẽ các fingerprint riêng. Các bạn có thể search trên mạng finger print for browser. Tuy nhiên, giải pháp này cũng chưa triệt để vì nếu một máy cài nhiều browser thì không chính xác lắm. Đối với iOS thì Apple bắt buộc các bên thứ 3 đều sử dụng web view của họ nên có thể dùng cách này. Tuy nhiên, trên iOS hay Windows thì vẫn chưa triệt để.

Từ các phương pháp trên, chúng ta sẽ tìm một phương pháp và áp dụng trên Client khác nhau. Hiện nay, ở cty mình thì iOS xác định qua account Apple vì cách này vẫn sử dụng được. Trên Android thì các bạn có thể theo phương pháp sau: <a href="https://android-developers.googleblog.com/2011/03/identifying-app-installations.html">https://android-developers.googleblog.com/2011/03/identifying-app-installations.html</a>.

<span style="color: #0000ff;">***3. Kĩ thuật để tracking device:***</span>

Để biết được client nào gọi request đến server của chúng ta thì lúc client gửi thông tin lên server, các bạn thêm vào header và gửi request đó lên server.

Ví dụ, chúng ta sẽ có một header là: X-UNIQUE-DEVICE: md5(identify_string).

Trong đó X-UNIQUE-DEVICE là header nhúng trong request. md5(identify_string) là chuỗi định danh của client. Tại sao chúng ta sử dụng md5 vì md5 cho ra một chuỗi có độ dài giống nhau, và input khác nhau thì output khác nhau. identify_string là định danh mà chúng ta đã tìm được ở phần 2.

Sau khi gửi request lên server, trên server, chúng ta cần ghi lại log request của client với thông tin header đi kèm.

Sau khi có file log, chúng ta sẽ phân tích ra được một dữ liệu thô để tiếp tục xử lý.

<span style="color: #0000ff;">***4.Ứng dụng của việc định danh Client:***</span>

Việc định danh client sẽ giúp rất nhiều cho chúng ta. Trong đó, ta thấy được một số ứng dụng chính sau:

***a. Đếm được chính xác số download hoặc active user (device):***

Bằng cách định danh được client, chúng ta sẽ biết được chính xác hệ thống của chúng ta có bao nhiêu device (user) đang active.

Qua việc đếm được chính xác số này, chúng ta sẽ đánh giá được sức khỏe của hệ thống server, hoặc đánh giá được hiệu quả của một đợt marketing về app install.

***b. Phân tích hành vi người dùng:***

Vì chúng ta định danh được client, chúng ta sẽ có được các action của user. Qua việc thấy được action của user, chúng ta sẽ thấy được hành vi của người dùng là gì.

***c. Cá nhân hóa thông tin cho user:***

Từ việc lấy được hành vi của user, chúng ta sẽ đưa ra các thông tin hữu ích đến từng user một.

***d. Chống user gian lận***

Đối với các hệ thống liên quan đến việc thương mại hoặc thưởng điểm dựa trên thông tin user hoặc device, chúng ta sẽ biết được user nào có hành vi tạo nhiều account hoặc dùng nhiều account trên cùng một máy để gian lận điểm thường. Vì chúng ta đã tracking được thông tin device nên chúng ta sẽ biết được user nào tạo nhiều account trên một máy và gian lận.

Còn nhiều ứng dụng nữa trong việc định danh client. Nhưng trên đây là những ứng dụng rõ nét nhất mà mình thấy ở cty mình và nó thực sự hiệu quả.

<span style="color: #0000ff;">***5. Nhược điểm của việc này:***</span>

Việc định danh client cũng chưa hoàn toàn chính xác hoàn toàn. Vì các công ty cung cấp hệ điều hành các ngày càng siết chặt việc lấy định danh client nên kĩ thuật này cần nghiên cứu khá là phức tạp.

Ngoài ra, các máy Android bị root hoặc máy iOS bị jaibreak có thể bị fake các thông tin kể trên. Cho nên việc định danh client vẫn chưa thực sự triệt để.

Vẫn còn những kẻ hở để những cá nhân có hiểu biết về kĩ thuật có thể lách qua.

<span style="color: #ff6600;">***Kết luận:***</span>

Ứng dụng của kĩ thuật định danh client là thấy rõ được và nó hữu ích trong việc phân tích hành vi người dùng. Qua đó chúng ta có thể có hệ thống recommandation tốt để đưa thông tin hiệu quả đến user.

Tuy nhiên, kĩ thuật này vẫn còn có một số hạn chế và chưa thực sự triệt để.

Do đó, chúng ta sẽ cần nghiên cứu nhiều cách khác nữa để định danh client và xử lý triệt để các hạn chế.

