---
layout: post
title: "Bài 4: Điều kiện if else trong C"
category: C
tags: [C, C++]
date: 2016-12-01
---
Ở bài học trước chúng ta đã học cách sử dụng các phép toán trong ngôn ngữ C. Hôm nay, chúng ta sẽ tìm hiểu về các điều kiện rẽ nhánh.

***Sử dụng điều kiện if...else***

Hãy bắt đầu bằng ví dụ sau:

```
#include<stdio.h>
#include<stdlib.h> 
int main(int argc, char *argv[])
{
	int tuoi = 0;
	printf("Hay nhap vao tuoi cua ban: ");
	scanf("%d", &tuoi);
	if(tuoi > 18){
		printf("Ban 18+ roi do, hehe.\n");
	}else{
		printf("Ban la do tre con, khong duoc lam chuyen nguoi lon nha.\n");
	}
}
```

Như ở ví dụ trên, chúng ta đã có kiểm tra điều kiện tuoi có lớn hơn 18 hay không? Nếu tuổi lớn hơn 18 nghĩa là họ đã là người trưởng thành, có thể làm chuyện người lớn được(ý nói làm công dân của xã hội ấy, không phải chuyện bậy).

Còn không thì sao, thì chúng ta sẽ rẽ sang nhánh khác, nhánh khác ở đây là nhánh trong phần else. Nghĩa là phần else này xảy ra khi tuoi < 18. Do đó, ta hiểu rằng, cấu trúc if..else sẽ như sau:

if điều kiện muốn kiểm tra là đúng

thì làm việc gì đó

còn không (else):

làm việc khác

Nhìn vào ví dụ đó, chúng ta sẽ hiểu cấu trúc của if...else sẽ như sau:

Viết if đầu dòng, sau đó mở ngoặc đơn. Trong dấu ngoặc đơn sẽ là mệnh đề điều kiện, đóng ngoặc đơn. Sau dấu ngoặc đơn sẽ là có một cặp dấu { và }. Trong cặp dấu { và } sẽ là một số các câu lệnh. Lưu ý là có thể nhiều câu lệnh trong 2 dấu { và }. Một điều cần chú ý nữa là khi mà có dấu { bắt đầu thì các câu lệnh cần phải thụt vào một tab. Chúng ta có thể không tab nhưng chương trình nhìn sẽ rất rối mắt và khó hiểu.

Lưu ý ở đây là mệnh đề kiểm tra "tuoi > 18". Chúng ta dùng dấu > để kiểm tra xem một biến có lớn hơn một giá trị hay không. Chúng ta sẽ có các điều kiện khác như sau:

<img class="alignnone size-medium wp-image-34" src="http://hoctuduylaptrinh.com/wp-content/uploads/2016/12/condition_syntax-300x190.png" alt="condition_syntax" width="300" height="190" />

Nhìn vào bảng ký hiệu trên, ta có thể có các ví dụ khác như sau:

```
if(tuoi == 18){
    printf("Ban vua tron 18 tuoi\n");
}

```

Ở đây, chúng ta kiểm tra xem tuổi có bằng 18 hay không. Nếu bằng thì in ra "Ban vua tron 18 tuoi". Lưu ý ở đây là phải hai dấu == thì nó mới thành mệnh đề kiểm tra điều kiện. Nếu chúng ta viết  if (tuoi = 18) thì lúc đó chúng ta đã gán giá trị của biến tuoi cho 18.

Theo như kinh nghiệm dạy học của mình thì các bạn sẽ gặp rắc rối với các ký hiệu mệnh đề điều kiện và phần đóng mở dấu { và } cũng như thụt vào các câu lệnh vào một tab. Do đó, các bạn nên tập luyện code nhiều để thành thạo về phần này.

Ví dụ trên chúng ta đã kiểm tra 2 khả năng là lớn hơn 18 hoặc không. Tuy nhiên trong thực tế, chúng ta sẽ có thể phải kiểm tra nhiều điều kiện hơn. Ví dụ kiểm tra có bé hơn 6 tuổi không, có lớn hơn 18 tuổi không, và điều kiện khác nữa. Để có thể xử lý được các tình huống đó, ngôn ngữ C cung cấp cho ta nhiều điều kiện để xử lý tình huống đó.

Hãy bắt đầu luôn bằng ví dụ:

```
#include<stdio.h> 
#include<stdlib.h>
int main(int argc, char *argv[])
{
	int tuoi = 0;
	printf("Hay nhap vao tuoi cua ban: ");
	scanf("%d", &tuoi);
	if(tuoi >= 18){
		printf("Ban 18+ roi do, hehe.\n");
	}else if(tuoi > 6){
		printf("Ban la do tre con!\n");
	}else{
		printf("Oe oe!\n");
	}
}

```

Ở ví dụ trên, ta đã kiểm tra xem tuổi có lớn hơn 18 hay không, nếu không thì kiểm tra tiếp xem có lớn hơn 6 không. Còn nếu không xảy ra cả hai điều kiện đó thì sẽ in ra "Oe oe".

Chúng ta có thể đặt nhiều else if nếu ta muốn. Ví dụ chúng ta có thể viết như sau:
<table class="NormalTable" style="height: 262px;" width="466">
<tbody>
<tr>
<td width="200"><span class="fontstyle0">NẾU biến số thỏa điều kiện 1
THÌ thực hiện việc 1
NẾU KHÔNG NẾU biến số thỏa điều kiện 2
THÌ thực hiện việc 2
NẾU KHÔNG NẾU biến số thỏa điều kiện 3
THÌ thực hiện việc 3
NẾU KHÔNG NẾU biến số thỏa điều kiện 4
THÌ thực hiện việc 4
NẾU KHÔNG thực hiện việc 5</span></td>
</tr>
</tbody>
</table>
&nbsp;

***Thiết lập nhiều điều kiện cùng lúc***

Ta có thể kiểm tra nhiều điều kiện cùng lúc với if. Ví dụ bạn muốn kiểm tra tuổi lớn hơn 18 và bé hơn 25. Chúng ta sẽ sử dụng các ký hiệu sau:

<img class="alignnone size-full wp-image-35" src="http://hoctuduylaptrinh.com/wp-content/uploads/2016/12/multi_conditon.png" alt="multi_conditon" width="182" height="213" />

Và để kiểm tra điều kiện trên chúng ta sẽ viết như sau:

```
if(18 <= tuoi && tuoi <= 25)
```

***Test HOẶC:***

Ví dụ ta muốn kiểm tra một người có nằm ngoài độ tuổi lao động không thì sẽ như sau:

```
if(tuoi < 18 || tuoi > 60){
    printf("Ban ngoai do tuoi lao dong\n");
}

```

Ở đây chúng ta sẽ kiểm tra một trong hai điều kiện tuoi < 18 hoặc tuoi > 60 thỏa mãn thì sẽ in ra màn hình dòng "Ban ngoai do tuoi lao dong".

***Test KHÔNG***

```
if(!(tuoi > 18)){
    printf("Ban la con nit\n");
}
```

Ở đây ta đang kiểm tra điều kiện ngược lại của tuoi > 18.
<h3>***Các lỗi hay gặp***</h3>
Có vẻ sau khi học xong thì chúng ta thấy rắc rối rồi đúng không? Bao nhiêu là ký tự.

***Lỗi thường gặp dấu ==***

Lưu ý để so sánh bằng thì chúng ta dùng dấu == chứ không phải dấu =. Dấu = là phép gán, còn dấu == là so sánh xem một biến có bằng một giá trị hay không.

***Lỗi dấu chấm phẩy sau điều kiện if***

Ví dụ đoạn code sau sẽ không chạy:

```
if (tuoi == 18); // dau cham phay nay KHONG duoc phep o day
{
    printf ("Ban chi vua moi truong thanh");
}

```

Chú ý tiếp theo là chúng ta cần phân biệt ký hiệu của các phép so sánh với ký hiệu của việc thiết lập nhiều điều kiện cùng lúc. Các bạn sẽ thấy khó hiểu giữa != và ký hiệu !. Ký hiệu tuoi != 18 là để so sánh xem tuổi có khác 18 hay không. Còn ký hiệu ! là lấy ngược lại điều kiện.

<span style="color: #ff0000;">Bài tập cho các bạn:</span>

<span style="color: #ff0000;">Giải phương trình bậc 1: a * x  + b = 0 với a, b là các biến nhập từ bàn phím.</span>

<span style="color: #ff0000;">Giải phương trình bậc 2:  a * x^2 + b * x + c = 0 với a, b, c là các biến nhập từ bàn phím.</span>
