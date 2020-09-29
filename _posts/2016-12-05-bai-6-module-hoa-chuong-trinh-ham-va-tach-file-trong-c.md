---
layout: post
title: "Bài 6: Module hóa chương trình: hàm và tách file trong C"
category: C
tags: [C++]
date: 2016-12-05
---
Trong các phần trước, chúng ta đã học các kĩ thuật lập trình trong ngôn ngữ C. Tuy nhiên, hầu như các bài code mà chúng ta đã sử dụng đều nằm trong một file và chỉ có một hàm main duy nhất. Trong thực tế, một dự án không thể chỉ code trong một file mà gồm rất nhiều file và nhiều hàm khác nhau. Hôm nay chúng ta sẽ tìm hiểu cách sử dụng hàm và tách file trong ngôn ngữ C.

***Cách sử dụng hàm***

Chúng ta sẽ bắt đầu bằng một ví dụ:

```
#include<stdio.h>

int tinh_chu_vi_hinh_chu_nhat(int chieu_dai, int chieu_rong);
int tinh_dien_tich(int chieu_dai, int chieu_rong);

int tinh_chu_vi_hinh_chu_nhat(int chieu_dai, int chieu_rong){
	int chu_vi_hinh_chu_nhat = 0;
	chu_vi_hinh_chu_nhat = (chieu_dai + chieu_rong) * 2;

	return chu_vi_hinh_chu_nhat;
}

int tinh_dien_tich(int chieu_dai, int chieu_rong){
	int dien_tich_hinh_chu_nhat = 0;
	dien_tich_hinh_chu_nhat = chieu_dai * chieu_rong;
	return dien_tich_hinh_chu_nhat;
}

int main(){
	int dai = 0;
	int rong = 0;
	int chu_vi = 0;
	int dien_tich;

	printf("\nNhap chieu dai ");
	scanf("%d", &dai);
	printf("\nNhap chieu rong");
	scanf("%d", &rong);

	chu_vi = tinh_chu_vi_hinh_chu_nhat(dai, rong);
	dien_tich = tinh_dien_tich(dai, rong);

	printf("chu vi hinh chu nhat la %d\n", chu_vi);
	printf("dien tich hinh chu nhat la %d\n", dien_tich);
}

```

Như ở ví dụ trên, chúng ta có hai hàm là tinh_dien_tich(int chieu_dai, int chieu_rong) và hàm tinh_chu_vi_hinh_chu_nhat(int chieu_dai, int chieu_rong). Nhưng mà hình như có gì đó sai sai. Chúng ta thấy tên hàm được khai báo lại hai lần thì phải? Chú ý kĩ hơn, các bạn sẽ thấy ở dòng khai báo hàm phía trên, chúng ta chỉ có tên hàm rồi đến dấu ;. Nhưng ở phía dưới, sau tên hàm sẽ là các đoạn code để thực hiện hàm đó. Vậy thì khác nhau ở đây là gì?

```
int tinh_dien_tich(int chieu_dai, int chieu_rong);

```

Đây là một khai báo hàm hay là prototype của hàm. Prototye để báo trước một hàm. Prototype thường được đặt ở đầu source code. Một prototye là một lời chỉ dẫn cho máy tính. Nó sẽ thông báo cho máy tính sự tồn tại của các hàm với các tham số cần đưa vào hàm.

Còn đoạn code:

```
int tinh_dien_tich(int chieu_dai, int chieu_rong){
	int dien_tich_hinh_chu_nhat = 0;
	dien_tich_hinh_chu_nhat = chieu_dai * chieu_rong;
	return dien_tich_hinh_chu_nhat;
}
```

là để thể hiện rõ công việc của hàm này.

Như đã hứa ở bài viết trước, chúng ta sẽ tìm hiểu về return. Như ở ví dụ trên, hàm tính diện tích sẽ có từ khóa return. Các bạn chú ý, lúc khai báo hàm, chúng ta thấy có kiểu int ở đầu hàm

```
int tinh_dien_tich(int chieu_dai, int chieu_rong)
```

có nghĩa là hàm này lúc kết thúc phải trả ra một kết quả có kiểu dữ liệu là int. Do đó, trong hàm, chúng ta sẽ thấy có dòng chữ return dien_tich_hinh_chu_nhat. Giá trị của kết quả trả về là một tích của chiều dài nhân với chiều rộng. Do vậy, ta cần chú ý, với những hàm nào khai báo có kiểu dữ liệu ở đầu hàm thì chúng ta cần phải return một kết quả.

Ví dụ khác về hàm mà không cần trả ra một kết quả:

```
void in_ra_chao_the_gioi(){
	printf("Hello world\n");
}

```

Như ở ví dụ trên, đơn giản hàm chỉ là thực hiện một lệnh in ra màn hình dòng chữ "Hello world". Như chúng ta thấy, khai báo hàm bắt đầu bằng void. Bây giờ, chúng ta hiểu rằng, hàm có kiểu khai báo void thì sẽ không cần return một kết quả trả ra.

Theo như cách hiểu của cá nhân mình, hàm với kiểu dữ liệu trả ra thì thường dùng khi người ta quan tâm đến kết quả của dữ liệu trả về chứ không quan tâm cách hàm thực hiện như thế nào. Nhưng hàm với kiểu void thì người ta thường sẽ quan tâm cách hàm thực hiện như thế nào.

Nhìn vào hai ví dụ trên, ta có thể hiểu hàm là một đoạn code để thực hiện môt chức năng gì đó. Và hàm sẽ được sử dụng lại nhiều lần.

***Cách dùng nhiều file trong ngôn ngữ C***

Chúng ta đã tìm hiểu cách viết các hàm trong ngôn ngữ C. Tiếp theo chúng ta sẽ học cách tách thành các file và cách gọi các file để code có thể chạy.

Ví dụ, chúng ta có 3 file như sau:

file main.cpp

```
#include<stdio.h>
#include "functions.h"

int main(){
	int a = 0, b = 0;

	printf("\nNhap a = ");
	scanf("%d", &a);

	printf("\nNhap b = ");
	scanf("%d", &b);

	int max = tim_max(a,b);

	printf("Gia tri lon nhat giua 2 so la %d\n", max);

	return 0;
}

```

File "functions.h"

```
int tim_max(int a, int b);

```

File functions.cpp

```
#include<stdio.h>

int tim_max(int a, int b){
	if(a > b){
		return a;
	}
	if(b > a){
		return b;
	}

	if(a == b){
		return a;
	}
}

```

Chúng ta thấy trong hàm main có một cách khai báo lạ ngay ở đầu file. Đó là dòng

```
#include "functions.h"
```

Đây là cách gọi một file header trong ngôn ngữ C. Nội dung của file header này chính là cái file "functions.h". File "functions.h" chỉ đơn giản là một số khai báo hàm (prototye) như cách khai báo hàm mà chúng ta vừa học xong. Vấn đề bây giờ là cái khai báo hàm này dùng để khai báo hàm ở đâu. Đó là là các hàm ở trong file "functions.cpp". Các bạn cẩn thận ở đây nha, "functions.cpp" là file chứa các hàm, "functions.h" là file header chứa các prototye của hàm. Tên 2 file này có vẻ giống nhau nhưng về mặt nội dung là khác nhau. Các bạn phải hiểu là file header .h như là một phần link giữa file "main.cpp" và file "functions.cpp". Chính file header "functions.h" là cầu nối để file "main.cpp" có thể gọi được các hàm ở trong file "functions.cpp".

Do đó, các bạn phải nhớ như sau, sẽ có một hàm main trong một file "main.cpp" là file để chạy chương trình chính. Chúng ta có file để thực hiện hàm nào đó thì cần phải có file header tương ứng để link giữa file hàm main và file khác. Ví dụ, bạn có thêm một file "tinh_toan.cpp" để thực hiện một số phép toán nào đó thì cần có một file "tinh_toan.h" nữa để link các hàm trong file "tinh_toan.cpp". Và để file main có thể dùng được thì ta lại có thêm dòng

```
#include "tinh_toan.h"
```

Mỗi file .cpp tương ứng với một file .h trong đó chứa những prototype của những functions.

Nhưng mà ở trong hàm main có 2 cách #include, thông thường ta sử dụng:

- Ngoặc nhọn < > để thêm vào một file thư viện tìm thấy trong folder của IDE
- Ngoặc kép " " để thêm vào một file tìm thấy trong folder project của bạn ( bên cạnh những file .c)

Khi code source bạn viết yêu cầu gọi một function, máy tính của bạn bắt buộc phải biết trước function đó là gì, nó cần bao nhiêu tham số (parameter),... Vì thế ta cần đến prototype: giống như một bảng hướng dẫn sử dụng trước khi dùng function cho máy tính.
Câu hỏi trên tương ứng với câu hỏi về thứ tự chạy chương trình: nếu bạn đặt các prototypes trong những file .h (headers) #include ở phần đầu những file .c , máy tính của bạn sẽ hiểu được cách sử dụng tất cả các function kể từ giai đoạn bắt đầu chạy chương trình.
Và điều đó giúp bạn ít bận tâm hơn về thứ tự đặt các function trong các files .c. Hiện giờ, bạn chỉ viết một số chương trình chứa khoảng hai hoặc ba functions, bạn vẫn chưa thấy rõ ích lợi của những prototypes nhưng về sau, khi bạn đã có thể viết nhiều functions hơn rồi, nếu bạn không đặt các prototypes trong những file .h, bạn sẽ thường xuyên gặp lỗi trong việc dịch chương trình.
