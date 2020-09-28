---
layout: post
title: "Bài 2: Sử dụng biến trong C"
category: C
tags: [C, C++]
date: 2016-11-28
---

Trong bài học trước, chúng ta đã làm quen với lập trình bằng chương trình "hello world". Trong bài này, chúng ta sẽ học cách sử dụng biến ở ngôn ngữ C.

***Biến là gì?***

Biến là một vùng nhớ trong máy tính được sử dụng để lưu trữ dữ liệu. Vùng nhớ này được dùng để lưu trữ giá trị của biến. Giá trị của biến có thể thay đổi được ở trong chương trình máy tính.

Ví dụ: bạn muốn lưu thông tin về tuổi của một người, bạn sẽ dùng một biến số để lưu trữ thông tin tuổi của người đó. 

Theo năm tháng, tuổi của người đó tăng lên, chúng ta có thể thay đổi giá trị biến số tuổi để lưu trữ đúng tuổi.

***Cách khai báo biến trong C:***

Trong ngôn ngữ C, một biến có hai thành phần:

1. Giá trị của biến số

2. Tên gọi của biến số, tên gọi này giúp ta nhận ra nó.

Ví dụ:
```
int tuoi = 18;
```

Ở ví dụ trên, chúng ta khai báo một biến "tuoi" để lưu trữ tuổi của một người, sau đó chúng ta gán giá trị biến này với một số, ở đây là 18.

Để đặt tên cho biến số, chúng ta cần phải tuân thủ theo các nguyên tắc sau:

1. Tên biến có thể là chữ hoa, chữ thường và những con số (abcABC012...)

2. Tên của biến phải bắt đầu bằng một chữ cái, không được bắt đầu bằng số. Chúng ta không được sử dụng khoảng trống " ", mà phải sử dụng ký tự "_".

3. Không sử dụng ký tự đặc biệt của tiếng Việt (vd: èéêà, ...)

Lưu ý, ngôn ngữ C phân biệt chữ hoa với chữ thường, vd "tuoi" khác với "Tuoi" và khác với "tUoi".

Mỗi người sẽ có cách đặt tên khác nhau, nhưng có một số quy định để đặt tên biến trong ngôn ngữ C:

1. Tên của biến nên hoàn toàn là chữ thường

2. Nếu tên biến là một từ có nhiều chữ thì nên cách nhau bằng dấu "_". Vd: "mang_song_nhan_vat", "ho_va_ten", ...

***Những dạng biến số:***

Ở ví dụ trên, ta đã khai báo biến tuoi và trước biến tuoi có chữ "int". int là một kiểu dữ liệu biến số. Biến số dùng để tính toán trong C. Có rất nhiều dạng biến số.

Ví dụ:

Những số tự nhiên dương 0, 10, 20, 50, ...

Những số thực: 1.24, 3.14, ...

Những số nguyên âm: -15, -273, ...

Những số thực âm: -20.24, -32.13, ...

Khi khai báo biến, bạn phải ghi nó thuộc dạng nào.

Ngôn ngữ C cung cấp cho chúng ta các kiểu dữ liệu số đó để chúng ta sử dụng. Các kiểu dữ liệu số trong ngôn ngữ C:

3 dạng đầu dùng để khai báo những số nguyên.

2 dạng sau dùng để khai báo những số thực.

Câu hỏi đặt ra là tại sao để biểu diễn một số tự nhiên mà cần đến 3 loại là char, int, long? Hoặc chỉ để khai báo một số thực, tại sao người ta cần dùng đến 2 loại là float và double?

Người ta tạo nhiều kiểu dữ liệu như vậy để tiết kiệm bộ nhớ máy tính. Vì tài nguyên bộ nhớ máy tính là có hạn, nếu chúng ta khai báo biến không cần thiết thì sẽ tốn bộ nhớ máy tính rất nhiều.

Vd như biến số dùng để lưu trữ số lần xem của youtube đã sử dụng kiểu int vì không ai nghĩ rằng một video có thể đến hơn 2 tỷ. Nhưng rồi video "Gangnam style" đã vượt qua mức xem đó. Do vậy các kĩ sư Google đã phải sửa lại biến để lưu trữ số lần xem đó.

Như vậy, lúc khai báo biến, chúng ta cần phải hình dung được ngữ cảnh sử dụng của biến và giới hạn mà biến có thể đạt đến.

***Hiển thị giá trị của biến số:***

Như ở bài trước, chúng ta đã sử dụng hàm printf để hiển thị một đoạn ký tự.

Bây giờ, chúng ta cũng sẽ hiển thị biến số bằng hàm printf.

VD:

```
printf("Tuoi cua bạn la %d", tuoi);
```

Chúng ta sử dụng %d để hiển thị một dạng số kiểu int.

Còn các kiểu dữ liệu khác thì sao, chúng ta cũng có các ký tự khác để sử dụng.

Sau đây là code ví dụ một bài:
```
#include<stdio.h>
#include<stdlib.h>

int main(){
  int bien_so_nguyen;//khai bao bien
  bien_so_nguyen = 0;//gan gia tri cho bien
  printf("Gia tri cua bien so nguyen la %d\n", bien_so_nguyen);
  double bien_so_thap_phan = 10.2424; // khai bao va khoi tao gia tri cho bien so
  printf("Gia tri cua bien so thap phan la %f\n", bien_so_thap_phan);
  return 0;
}
```

Chúng ta có thể hiển thị nhiều biến trong một dòng bằng hàm printf.

Vd:
```
printf("Gia tri cua bien so nguyen la %d, cua so thap phan la %f\n", bien_so_nguyen,bien_so_thap_phan);
```

***Cách gán giá trị cho biến:***

Như ở ví dụ trên ta đã khai báo biến và gán giá trị cho biến đó. Tuy nhiên, trong thực tế, chúng ta muốn thay đổi và muốn tự nhập giá trị cho biến số đó thì phải làm như thế nào?

Ngôn ngữ C cung cấp cho chúng ta một hàm để nhập giá trị của biến số từ bàn phím. Đó là hàm scanf. Cách sử dụng hàm scanf khá giống với hàm printf. Nghĩa là tương ứng với kiểu số nào thì bạn cũng cần khai báo "%d" hay "%f" để nhập số nguyên hay số thực.

Vd:
```
scanf("%d", &tuoi);
```

Chúng ta cần đặt %d ở trong dấu "" và cần đặt dấu & trước tên biến.

Thêm ví dụ về cách nhập giá trị biến từ bàn phím và in ra kết quả:
```
#include<stdio.h>
#include<stdlib.h>
int main(int argc, char *argv[]) {
    int tuoi = 0; // Khoi tao bien so gia tri la 0
    printf ("Ban bao nhieu tuoi?\\n");
    scanf ("%d", &amp;tuoi); // May tinh yeu cau nhap tuoi voi scanf
    printf ("Oh! tuoi cua ban la %d !\n\n", tuoi);
    return 0;
}
```
