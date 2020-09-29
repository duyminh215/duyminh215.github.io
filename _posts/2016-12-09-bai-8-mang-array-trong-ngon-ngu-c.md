---
layout: post
title: "Bài 8: Mảng (array) trong ngôn ngữ C"
category: C
tags: [C++]
date: 2016-12-09
---
Ở bài học trước, chúng ta đã học cách sử dụng con trỏ trong ngôn ngữ C. Hôm nay chúng ta sẽ tìm hiểu về mảng trong ngôn ngữ C và kết hợp sử dụng con trỏ với mảng.

***Mảng là gì?***

Mảng là một dãy các biến cùng type, chứa trong một vùng nhớ liên tục.

Như vậy, mảng có thể chứa lượng lớn biến cùng type (long, int, double, char, ...)

Mỗi mảng có một kích thước xác định. Nó có thể tạo bởi 2, 3, 5,10, 31, ...phần tử, tùy vào yêu cầu của bạn.

<img class="alignnone wp-image-57" src="http://hoctuduylaptrinh.com/wp-content/uploads/2016/12/array-300x185.png" alt="array" width="468" height="289" />

Khi bạn yêu cầu tạo một mảng kích thước 4 ô trong bộ nhớ, chương trình sẽ yêu cầu hệ điều hành quyền sử dụng 4 ô bộ

nhớ. 4 ô này phải nằm kề nhau, có nghĩa là ô sau sẽ kế tiếp ô trước. Giống như trên, các địa chỉ nằm nối tiếp nhau:

1600, 1601, 1602, 1603 và không có "khoảng trống" nào ở giữa.

Cuối cùng, mỗi ô trong mảng chứa một số cùng type. Nếu mảng có type int, thì mỗi ô trong mảng chứa một số type int.

Không thể tạo mảng cùng lúc chứa giá trị type int và double.

Tóm lại, sau đây là những điều buộc phải ghi nhớ:

1. Khi một mảng (array) được tạo ra, nó sử dụng một vùng liên tục trong bộ nhớ: ở đó các ô bộ nhớ sẽ nằm liên tục kề nhau. Tất cả các ô (case) trong mảng phải cùng type.

2. Một array type int chỉ chứa các số dạng int, không thể chứa các số dạng khác.

***Cách tạo một mảng***

Chúng ta bắt đầu bằng cách khai báo một mảng kiểu int có 4 giá trị

```
int array[4];

```

Vậy thôi, ta chỉ cần thêm vào trong dấu ngoặc vuông [ ] số lượng ô mà bạn muốn chứa trong mảng. Không có giới hạn (tùy theo dung lượng bộ nhớ của máy tính).

Trên đây là cách khai báo một mảng có 4 phần tử kiểu int. Tuy nhiên muốn gán giá trị của từng phần tử trong mảng thì

làm như thế nào? Chúng ta sẽ gán các phần tử của mảng như sau:

```
int array[4] ;
array[0] = 10;
array[1] = 23;
array[2] = 505;
array[3] = 8;

```

Vậy mối quan hệ giữa mảng và con trỏ là gì?

Nếu bạn chỉ viết là array thì đó chính là pointer. Đó là một pointer chỉ vào ô đầu tiên của mảng.
Test :

```
int array[4] ;
printf ("%d", array);

```

Kết quả ta nhận được là ô địa chỉ đầu tiên của mảng:

```
1600

```

Nếu bạn ghi thứ tự của ô trong mảng vào ngoặc vuông [ ], bạn sẽ nhận được giá trị của ô đó:

```
int array[4];
printf ("%d", array[0]);

```

Kết quả sẽ là

```
10

```

Tương tự với các ô khác. Nhắc lại là nếu bạn viết array, nó sẽ là một pointer, chúng ta có thể sử dụng kí tự * để có được

giá trị của ô đầu tiên:

```
int array[4];
printf ("%d", *array);

```

Kết quả

```
10

```

Và có thể nhận giá trị của ô tiếp theo với *(array+1) (địa chỉ của array+1). Cả 2 dòng code sau hoạt động tương tự nhau:

```
array[1] // Cho gia tri cua o thu 2 (o dau tien viet la [0])
*(array+ 1) // Tuong tu: cho gia tri o thu 2

```

Nói rõ hơn, nếu bạn viết array[0], cũng giống như bạn yêu cầu giá trị tìm thấy ở địa chỉ array + 0 (ở ví dụ là 1600). Nếu

bạn viết array[1], bạn sẽ nhận được giá trị ở địa chỉ array + 1 (1601 trong ví dụ). Và tương tự với những trường hợp còn

lại.

***Liệt kê các phần tử trong mảng***

Bây giờ tôi muốn hiển thị giá trị mỗi ô trong mảng. Tôi có thể sử dụng số lượng printf bằng với số ô trong mảng. Nhưng

tôi phải viết nhiều lần printf, điều này thật nhàm chán (hãy tưởng tượng đến trường hợp mảng chứa 8000 giá trị)

Vì vậy, tốt hơn là sử dụng vòng lặp. Và vòng lặp for rất tiện lợi trong việc này:

```
#include<stdio.h>

int tong_array(int array[], int array_size);

int main(){

	int kich_thuoc_mang = 4;
	int array[kich_thuoc_mang];

	for(int i = 0; i < kich_thuoc_mang; i++){
		array[i] = i;
	}

	for(int i = 0; i < kich_thuoc_mang; i++){
		printf("\\nPhan tu thu %d cua mang co gia tri %d", i, array[i]);
	}

}

```

Kết quả sẽ là

```
Phan tu thu 0 cua mang co gia tri 0
Phan tu thu 1 cua mang co gia tri 1
Phan tu thu 2 cua mang co gia tri 2
Phan tu thu 3 cua mang co gia tri 3

```

Vòng lặp sẽ chạy dọc các ô trong mảng nhờ vào biến số i (các nhà lập trình thường dùng i, đây là một biến

số khá thông dụng để chạy dọc một mảng)Cách này đặc biệt thông dụng, ta để một biến số trong dấu [ ]. Những biến số

tuyệt đối cấm sử dụng trong việc tạo các mảng (để khai báo kích thước), nhưng nó được phép sử dụng để "di chuyển"

trong mảng, có nghĩa là để hiển thị các giá trị! Trong ví dụ trên, tôi đặt biến số i, nó sẽ tăng dần từ 0, 1, 2 rồi 3. Như

vậy, nó sẽ hiển thị các giá trị của array[0], array[1], array[2] và array[3]!

***Khởi tạo các giá trị trong một mảng***

Bạn đã biết cách di chuyển trong mảng, điều này có nghĩa bạn có thể khởi tạo mảng với giá trị 0 ở tất cả các ô bằng việc

sử dụng vòng lặp!

```
#include<stdio.h>

int tong_array(int array[], int array_size);

int main(){

	int kich_thuoc_mang = 4;
	int array[kich_thuoc_mang];

	for(int i = 0; i < kich_thuoc_mang; i++){
		array[i] = 0;
	}

	for(int i = 0; i < kich_thuoc_mang; i++){
		printf("\\nPhan tu thu %d cua mang co gia tri %d", i, array[i]);
	}

}
```

***Một cách khác để khởi tạo giá trị***

Bạn cần biết là còn một cách khác để khởi tạo giá trị trong mảng khá thủ công trong C.

Bằng cách viết từng giá trị trong ngoặc nhọn { }, cách nhau bởi dầu phẩy “,” :

array[4] = { giaTri1, giaTri2, giaTri3, giaTri4};

```
int main (int argc, char *argv[ ])
{
	int array[4] = {0, 0, 0, 0}, i = 0;
	for (i = 0 ; i < 4 ; i++)
	{
		printf ("%d\\n", array[i]);
	}
	return 0;
}

```

Mặt khác, lợi ích của cách làm này là, bạn chỉ cần khai báo giá trị những ô đầu tiên, những ô còn lại sẽ tự động nhận giá trị 0:

Cụ thể, nếu tôi viết:

```
int array[4] = {10, 23};

```

Ô đầu tiên nhận giá trị 10, ô thứ 2 nhận giá trị 23, các ô còn lại nhận giá trị 0.

Vậy làm cách nào để khai báo tất cả các ô với giá trị 0? Bạn chỉ cần khai báo ô đầu tiên giá trị 0, sau đó các ô còn lại

cũng sẽ nhận giá trị 0.

<span style="color: #ff0000;">Bài tập cho bạn:</span>

<span style="color: #ff0000;">***Bài tập 1***</span>
<span style="color: #ff0000;">Tạo một function tongArray để tính tổng các giá trị chứa trong nó (sử dụng return để trả về giá trị). Và để giúp bạn </span>

<span style="color: #ff0000;">hiểu rõ hơn, đây là prototype của function cần viết:</span>

<span style="color: #ff0000;">C code:</span>
<span style="color: #ff0000;">int tongArray (int array[ ], int kichthuocArray);</span>

<span style="color: #ff0000;">***Bài tập 2***</span>
<span style="color: #ff0000;">Tạo một function trungBinhArray để tính trung bình các giá trị chứa trong nó.</span>

<span style="color: #ff0000;">Prototype:</span>
<span style="color: #ff0000;">C code:</span>
<span style="color: #ff0000;">double trungBinhArray (int array[ ], int kichThuocArray);</span>

<span style="color: #ff0000;">***Bài tập 3***</span>
<span style="color: #ff0000;">Tạo một function copyArray để chép nội dung array này sang một array khác.</span>

<span style="color: #ff0000;">Prototype:</span>
<span style="color: #ff0000;">C code:</span>
<span style="color: #ff0000;">void copyArray (int array1[ ], int array2[ ], int kichThuoc);Bài tập 4</span>

<span style="color: #ff0000;">Viết một function maximumArray có nhiệm vụ so sánh tất cả các giá trị chứa bên trong array với giaTriMax. Nếu có </span>

<span style="color: #ff0000;">giá trị lớn hơn biến số giaTriMax đưa vào, nó sẽ chuyển thành 0.</span>

<span style="color: #ff0000;">Prototype:</span>
<span style="color: #ff0000;">C code:</span>
<span style="color: #ff0000;">void maximumArray (int array[ ], int kichThuoc, int giaTriMax);</span>

<span style="color: #ff0000;">VD: array {1,5,7,8,5,2,3} và max=5, sẽ chuyển thành {1,5,0,0,5,2,3}.</span>
