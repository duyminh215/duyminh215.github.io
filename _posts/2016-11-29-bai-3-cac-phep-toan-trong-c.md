---
layout: post
title: "Bài 3: Các phép toán trong C"
category: C
tags: [C, C++]
date: 2016-11-29
---
Xin chào các bạn, trong bài trước chúng ta đã tìm hiểu qua về cách khai báo biến trong ngôn ngữ C. Trong bài tiếp theo chúng ta sẽ học cách sử dụng các công cụ tính toán trong C để đưa ra các kết quả mà mình mong muốn.

Ngôn ngữ C cung cấp cho chúng ta một số công cụ để chúng ta có thể tính toán. Ngôn ngữ C có thể thực hiện được các phép toán sau:

1. Phép cộng
2. Phép trừ
3. Phép nhân
4. Phép chia

Chúng ta sẽ lần lượt tìm hiểu các phép toán cơ bản trước, sau đó sẽ có các hàm để thực hiện các phép toán phức tạp hơn như căn bậc 2, lũy thừa, ...

Chúng ta bắt đầu với phép cộng. Để thực hiện phép cộng chúng ta sẽ sử dụng dấu +.

Vd:

```
#include<stdio.h>
int main(int argc, char *argv[])
{
    int sum = 0;
    sum = 3 + 5;
    printf("Tong cua hai so la %d\n", sum);
    return 0;
}
```
Nếu như theo suy nghĩ của chúng ta phép toán kia sẽ ra kết quả là 3.5. Nhưng lúc mà chạy chương trình trên chúng ta sẽ được kết quả là 3. Vậy là máy tính sai à? Vậy thì máy tính kém quá nhỉ?

Tuy nhiên, các bạn hãy nhớ lại kiến thức của bài trước về các dạng biến số. Như chúng ta biết kiểu int để biểu diễn các số nguyên. Do vậy, biến thuong ở bài ví dụ trên nó cũng chỉ trả ra kết quả là một số nguyên thôi.

Vậy thì làm sao để bài trên trả ra được kết quả đúng là 3.5? Chúng ta hãy nhớ lại kiến thức của bài trước. Để khai báo một biến số thực, chúng sử dụng kiểu float hoặc double. Do đó, chúng ta sẽ thử lại như sau:

```
double thuong = 0;
thuong = 7/2;
```
Chúng ta thử thay xem có vấn đề gì không? Sau khi chạy, máy tính vẫn trả ra kết quả bằng 3. Mặc dù thương đã khai báo kiểu double rồi. Có vấn đề gì thế nhỉ? Máy tính này ngu quá!!!

Không phải đâu các bạn ạ, máy tính không ngu đâu, nó chỉ thực hiện lệnh rất chính xác thôi. Lưu ý rằng 7 với 2 máy tính vẫn hiểu là 2 số nguyên nên kết quả nó vẫn trả ra bằng 3. Để thực hiện đúng phép toán trên chúng ta cần tiếp tục sửa chương trình thành như sau:

```
double thuong = 0;
thuong = 7.0/2.0;
```
Bây giờ thì các bạn hãy thử lại chương trình và chạy lại xem sao nào. Kết quả sẽ được là 3.50000 đúng không? Vậy là máy tính đã trả ra kết quả đúng rồi. Do vậy các bạn lưu ý trong lập trình C, chúng ta cần phải khai báo chính xác loại kiểu số mà chúng ta sử dụng để tính toán trong chương trình. Kiểu int và long thì dùng để thực hiện các phép toán với các kết quả là số nguyên. Kiểu float và double sử dụng để thực hiện các phép toán với kết quả là các số thực.

Ở ví dụ trên chúng ta chia 7 cho 2 sẽ được ra 3.5 đối với số thực. Nhưng với số nguyên chúng ta sẽ được thương là 3 và dư 1. Vậy muốn lấy số dư 1 ra thì làm như thế nào? Ngôn ngữ C có cung cấp phép toán lấy số dư. Đó là phép module.

***Phép module:***

Module là phép toán cho ta số dư của một phép chia. Để sử dụng phép module chúng ta sử dụng dấu %.

Ví dụ:
```
5 % 2 = 1
14 % 3 = 2
4 % 2 = 0
```

***Sử dụng phép toán với các biến số:***

Ở bài trước, chúng ta đã học được cách khai báo các biến số, chúng ta sẽ học cách sử dụng các biến số đó để thực hiện các phép toán. Chúng ta hãy xem ví dụ sau:

```
#include<stdio.h>
#include<stdlib.h>
int main(int argc, char *argv[])
{
    int a = 0, b = 0;
    int sum = 0, dif = 0;
    printf("Nhap vao so thu nhat: ");
    scanf("%d", &a);
    printf("Nhap vao so thu hai: ");
    scanf("%d", &b);
    sum = a + b;
    dif = a - b;
    printf("Tong cua hai so la %d\n", sum);
    printf("Hieu cua hai so la %d\n", dif);
    return 0;
}
```

Với bài trên, chúng ta đã học cách sử dụng kiến thức của bài trước và bài này. Đó là cách khai báo biến và sử dụng phép toán với các biến số đó.

<span style="color: #ff0000;">Bài tập cho các bạn:</span>

<span style="color: #ff0000;">Làm bài tập tính tổng 2 số, 3 sốvới các biến số nhập từ bàn phím như ví dụ trên.</span>

<span style="color: #ff0000;">Làm bài tập tính hiệu, tích, thương và phép module cho 2 số với các biến số nhập từ bàn phím.</span>

***Các phương pháp rút gọn:***

Đó là các phép toán cơ bản mà ngôn ngữ C cung cấp cho chúng ta. Chúng ta không cần thêm các phép toán khác vì chúng ta có thể tạo ra chúng. Ngoài ra, ngôn ngữ C cung cấp cho chúng ta một số phương pháp viết rút gọn. Tại sao lại viết rút gọn? Tại vì chúng ta sẽ thường xuyên phải lặp lại các phép toán.

***Phép tăng giá trị:***

Bạn sẽ thấy rằng bạn sẽ thường xuyên tăng giá trị của biến lên 1. Và ta sẽ làm như sau:

sohang = sohang + 1;

Chúng ta sẽ lấy số hạng cộng với chính nó thêm 1. Nghĩa là nếu số hạng mà bằng 3 thì sau phép trên sẽ được là 4.

Thao tác này sau này bạn sẽ thấy là sử dụng thường xuyên. Do đó các nhà viết ngôn ngữ lập trình C đã nghĩ ra cách rút gọn. Cách viết đó như sau:
```
sohang++;
```

***Phép giảm giá trị:***

Tương tự như trên, để giảm sohang một giá trị, chúng ta có thể viết như sau:

sohang = sohang - 1;

Và cách rút gọn sẽ là:

sohang--;

***Các dạng viết rút gọn khác:***

Trong C còn nhiều cách viết rút gọn khác cũng hoạt động tương tự. Tất cả các phép toán cơ bản +, -, *, / đều có phương pháp rút gọn.

Ví dụ bạn muốn tăng 3 lần giá trị của 1 biến số:

sohang = sohang * 3;

Bạn có thể rút gọn lại là:

sohang *= 3;

Tương tự cho các phép toán khác:

```
int sohang = 5;

sohang += 4; // sohang tro thanh 9...

sohang -= 3; // ... sohang tro thanh 2

sohang *= 5; // ... sohang tro thanh 25

sohang /= 3; // ... sohang tro thanh 1

sohang %= 3; // ... sohang tro thanh 2 (vi 5 = 1 * 3 + 2)
```
***Thư viện toán học***

Trong ngôn ngữ C tồn tại cái gọi là những thư viện chuẩn mà các lập trình viên đã viết để chúng ta sử dụng. Trong đó, thư viện "math.h" chứa lượng lớn các function toán học đã được viết trước.

Ví dụ bạn muốn tính phép lũy thừa trong C thì phải làm như thế nào? Bạn có thể viết  <span class="fontstyle0">5²</span>  nhưng mà máy tính sẽ không hiểu phép toán này. Để sử dụng được thư viện toán học chúng ta cần include:
```
#include<math.h>
```
Một số hàm trong thư viện "math.h"

*** <span class="fontstyle0">fabs</span> ***

Hàm này trả ra kết quả là giá trị tuyệt đối của một số.

Ví dụ:
```
double giatri_tuyetdoi = 0, sohang = -27;

giatri_tuyetdoi = fabs(sohang); // gia tri tuyet doi cua sohang se la 27

```

***ceil***

Hàm này sẽ trả về giá trị dạng số nguyên nếu như ta đưa cho nó một số thực. Đó là một dạng làm tròn. Nó luôn cho một số nguyên có giá trị lớn hơn.

Ví dụ:

```
double lamtron_len = 0, sohang = 52.71;

lamtron_len = ceil(sohang); // lamtron_len se bang 53
```

***floor***

Trái ngược với hàm ceil, hàm này cho ta số nguyên nhỏ hơn.

Ví dụ:

```
double lamtron_xuong = 0, sohang = 37.91;

lamtron_xuong = floor(sohang); // gia tri cua lamtron_xuong se bang 37
```

***pow***

Function này cho phép tính lũy thừa một số. Chúng ta cần phải chỉ ra 2 biến cho nó, số hạng và cấp lũy thừa.

Ví dụ muốn tính  5² như cách viết thông thường của chúng ta thì cần dùng hàm trong C như sau:

```
double ketqua = pow(5,2);

```

***sqrt***

Hàm này để tính căn bậc hai của một số, nó cho ta giá trị dạng double.

Ví dụ:

```
double ketqua = 0, sohang = 100;
ketqua = sqrt(sohang); // ketqua tro thanh 10
```

Ngoài ra thư viện này còn cung cấp nhiều phép toán nữa như sin, cos, tan, asin, acos, atan, log, ...

<span style="color: #ff0000;">Bài tập:</span>

<span style="color: #ff0000;">Tính bình phương của một biến số với biến số nhập từ bàn phím.</span>

<span style="color: #ff0000;">Tính căn bậc hai của một biến số với giá trị của biến số nhập từ bàn phím. </span>

Các kết quả của hai bài tập trên sẽ được sử dụng cho bài tiếp theo. Các bạn hãy cũng đón chờ nhé!!!


