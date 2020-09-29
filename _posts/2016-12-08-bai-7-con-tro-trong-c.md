---
layout: post
title: "Bài 7: Con trỏ trong C"
category: C
tags: [C++]
date: 2016-12-08
---
<span class="fontstyle0">Đã đến lúc chúng ta tìm hiểu về con trỏ. Hãy ra hít một hơi thật sâu trước khi bắt đầu vì mình biết
bài học này chắc chắn sẽ không khiến bạn thấy thú vị. Nhưng con trỏ là một khái niệm được sử
dụng rất thường xuyên trong C. Nói về tầm quan trọng, chúng ta không thể nào lập trình trên ngôn
ngữ C mà không dùng đến con trỏ, và bạn cũng đã từng dùng nó mà không biết.</span>

<span class="fontstyle0">***Một vấn đề nan giải*** 

</span><span class="fontstyle2">Đây là một trong những vấn đề lớn liên quan đến con trỏ, các bạn mới bắt đầu thường bị nhầm lẫn,
cảm thấy khó khăn trong việc nắm vững cách hoạt động và sử dụng.
"Con trỏ rất cần thiết, và chúng ta sẽ thường xuyên dùng đến nó, hãy tin tôi !"</span>

<span class="fontstyle0">Mình sẽ cho bạn xem một ví dụ mà các bạn không thể nào giải quyết được nếu không sử dụng đến
con trỏ. Đây cũng là tiêu điểm của bài học này, tôi sẽ hướng dẫn cách giải quyết ở cuối bài học.
Đây là vấn đề: Tôi muốn viết một function trả về hai giá trị. Việc này là </span><span class="fontstyle2">không thể </span><span class="fontstyle0">vì mỗi function
chỉ có thể trả về duy nhất một giá trị.</span>

```
int function ( )
{
	return giatri;
}

```

<span class="fontstyle0">Nếu ta khai báo function với type </span><span class="fontstyle2">int</span><span class="fontstyle0">, thì ta sẽ nhận được một số dạng </span><span class="fontstyle2">int </span><span class="fontstyle0">(nhờ vào instruction
</span><span class="fontstyle2">return</span><span class="fontstyle0">).
Chúng ta cũng đã học cách viết một function không trả về bất cứ giá trị nào với từ khóa </span><span class="fontstyle2">void</span><span class="fontstyle0">:</span>

```
void function( )
{
}

```

<span class="fontstyle0">Nhưng để nhận được hai giá trị trả về cùng lúc thật sự là việc không thể. Chúng ta không thể sử
dụng hai </span><span class="fontstyle2">return </span><span class="fontstyle0">cùng lúc.</span>

<span class="fontstyle0">Giả sử tôi muốn viết một function, trong parameter tôi sẽ cho nó một giá trị tính bằng phút, tôi muốn nó chuyển thành giờ và phút tương ứng: 
1. Nếu ta đưa vào giá trị 45, function sẽ trả về 0 giờ và 45 phút. 
2. Nếu ta đưa vào giá trị 60, function sẽ trả về 1 giờ và 0 phút. 
3. Nếu ta đưa vào giá trị 60, function sẽ trả về 1 giờ và 30 phút . 
Nhìn có vẻ khá đơn giản, nhưng hãy cùng test đoạn code sau:</span>

```
#include<stdio.h> 
#include<stdlib.h> 

void chuyenDoi(int gio, int phut);
int main (int argc, char *argv[ ])
{
	int gio = 0, phut = 90;
	/*Chung ta co bien so "phut" giá trị 90. Sau khi ket thuc function, toi muon bien so
	"gio" nhan gia tri 1 và bien so "phut" nhan gia tri 30 */
	chuyenDoi(gio, phut);
	printf ("%d gio va %d phut", gio, phut);
	return 0;
}
void chuyenDoi(int gio, int phut)
{
	gio= phut/ 60; // 90 / 60 = 1
	phut= phut% 60; // 90 % 60 = 30
}

```

<span class="fontstyle0">Và đây là kết quả:</span>

```
0 gio va 90 phut

```

<span class="fontstyle0">Chương trình đã không hoạt động. Vì sao vậy?

Khi bạn gửi giá trị của một biến số vào vị trí parameter của một function, một bản sao của biến sốnày được tạo ra. Nói cách khác, biến số "</span><span class="fontstyle2">gio</span><span class="fontstyle0">" trong function </span><span class="fontstyle2">chuyenDoi </span><span class="fontstyle0">không phải là biến số "</span><span class="fontstyle2">gio</span><span class="fontstyle0">" trong function </span><span class="fontstyle2">main</span><span class="fontstyle0">! Nó chỉ là bản sao!
Function </span><span class="fontstyle2">chuyenDoi </span><span class="fontstyle0">đã thực hiện nhiệm vụ của nó. Trong function </span><span class="fontstyle2">chuyenDoi</span><span class="fontstyle0">, những biến số "</span><span class="fontstyle2">gio</span><span class="fontstyle0">" và "</span><span class="fontstyle2">phut</span><span class="fontstyle0">" nhận giá trị chính xác: 1 và 30.
Nhưng sau đó, function kết thúc khi dấu ngoặc </span><span class="fontstyle0">} </span><span class="fontstyle0">đóng lại. Như ta đã học ở bài học trước, tất cả những biến số tạo ra trong một function sẽ bị xóa đi khi function đó kết thúc. Và ở đây, biến số</span><span class="fontstyle2">gio </span><span class="fontstyle0">và </span><span class="fontstyle2">phut </span><span class="fontstyle0">đã bị xóa đi. Sau đó chương trình tiếp tục phần tiếp theo của </span><span class="fontstyle2">main</span><span class="fontstyle0">, và ở đó biến số </span><span class="fontstyle2">gio </span><span class="fontstyle0">và </span><span class="fontstyle2">phut </span><span class="fontstyle0">của </span><span class="fontstyle2">main </span><span class="fontstyle0">giá trị vẫn là 0 và 90. Đó là lí do bạn thất bại!</span>

<span class="fontstyle0">Và tiếp theo, hãy thử tìm nhiều cách khác sửa đổi chương trình trên, như trả về một giá trị sau khi kết thúc function (sử dụng </span><span class="fontstyle2">return </span><span class="fontstyle0">và thay đổi </span><span class="fontstyle2">type </span><span class="fontstyle0">function thành </span><span class="fontstyle2">int</span><span class="fontstyle0">), bạn chỉ nhận được một trong hai giá trị bạn cần. Bạn không thể nào nhận được cùng lúc hai giá trị. Và bạn tuyệt đối không được sử dụng biến số </span><span class="fontstyle2">global</span><span class="fontstyle0">, lí do tôi đã giải thích ở bài trước.</span>

<span class="fontstyle0">Và đó là vấn đề khó khăn đặt ra , vậy con trỏ sẽ giải quyết vấn đề trên như thế nào?</span>

<span class="fontstyle0">***Địa chỉ và giá trị*** 

</span><span class="fontstyle2">Khi bạn tạo ra một biến số </span><span class="fontstyle3">tuoi </span><span class="fontstyle2">type </span><span class="fontstyle3">int</span><span class="fontstyle2">, lấy ví dụ:</span>

```
int tuoi = 10;

```

<span class="fontstyle0">... chương trình của bạn sẽ yêu cầu hệ điều hành (ví dụ là Windows) quyền sử dụng một ít bộ nhớ. Hệ điều hành sẽ trả lời bằng cách đưa ra địa chỉ bộ nhớ được phép chứa con số bạn cần.
Đây cũng là một trong những nhiệm vụ chính của hệ điều hành:
Khi chúng ta yêu cầu mượn bộ nhớ cho chương trình. Máy tính giống như ông chủ, nó điều hành từng chương trình và kiểm tra xem chúng có quyền sử dụng bộ nhớ tại vị trí được cấp hay không. </span>

<span class="fontstyle0">Và đây là một trong những nguyên nhân khiến máy tính bạn bị đơ: Nếu chương trình đột nhiên hoạt động trên một vùng bộ nhớ không cho phép. Hệ điều hành (OS) sẽ từ chối và dừng ngay chương trình, giống như nói với bạn "Mày nghĩ ai là chủ ở đây?" Người dùng, sẽ nhìn thấy một cửa sổ hiện lên thông báo dạng "Chương trình bị dừng lại do thực hiện một công việc không được phép".
Quay trở lại với biến số </span><span class="fontstyle2">tuoi</span><span class="fontstyle0">. Giá trị 10 được đưa vào một vị trí nào đó trong bộ nhớ, lấy ví dụ nó được đưa vào địa chỉ 4655. Và điều xảy ra ở đây là (nhiệm vụ của compiler), từ </span><span class="fontstyle2">tuoi </span><span class="fontstyle0">trong chương trình sẽ thay thế bằng địa chỉ 4655 khi được chạy.
Việc đó giống như, mỗi khi bạn điền vào </span><span class="fontstyle2">tuoi </span><span class="fontstyle0">trong code source, chúng sẽ được chuyển thành 4655, và máy tính sẽ biết được cần đến địa chỉ nào trong bộ nhớ để lấy giá trị . Và ngay sau đó, máy tính xem giá trị được chứa trong địa chỉ 4655 và trả lời chúng ta "biến số tuoi co giá trị là 10"!
Và để lấy giá trị một biến số, đơn giản chỉ cần đánh tên của biến số đó vào code source. Nếu ta muốn hiển thị tuổi, ta có thể sử dụng function </span><span class="fontstyle2">printf</span><span class="fontstyle0">:</span>

```
printf ("Bien so tuoi co gia tri la : %d", tuoi);

```

<span class="fontstyle0">Không có điều gì mới với dòng code trên đúng ko.</span>

<span class="fontstyle0">Khuyến mãi thêm!
</span><span class="fontstyle2">Bạn đã biết cách hiển thị giá trị của một biến số, nhưng bạn có biết chúng ta cũng có thể hiển thị địa chỉ của biến số đó?
...Đương nhiên là bạn chưa biết rồi
Để hiển thị địa chỉ của một biến số, chúng ta cần sử dụng kí hiệu </span><span class="fontstyle3">%p </span><span class="fontstyle2">(p ở đây viết tắt của từ pointer) trong </span><span class="fontstyle3">printf</span><span class="fontstyle2">. Mặt khác, chúng ta phải đưa vào </span><span class="fontstyle3">printf </span><span class="fontstyle2">địa chỉ của biến số đó và để làm việc này, bạn cần phải đặt kí hiệu </span><span class="fontstyle3">& </span><span class="fontstyle2">trước biến số đó (</span><span class="fontstyle3">tuoi</span><span class="fontstyle2">), giống như cách tôi hướng dẫn bạn sử dụng </span><span class="fontstyle3">scanf</span><span class="fontstyle2">, xem code sau:</span>

```
printf ("Dia chi cua bien so tuoi la %p", &tuoi);

```

Kết quả

```
Dia chi cua bien so tuoi la 0023FF74

```

<span class="fontstyle0">Đó là địa chỉ của biến số </span><span class="fontstyle2">tuoi </span><span class="fontstyle0">trong thời điểm chương trình hoạt động. Vâng, 0023FF74 là một số, nó đơn giản chỉ được viết trên hệ hexadecimal (thập lục phân), thay vì hệ decimal (thập phân) mà chúng ta thường sử dụng. Nếu bạn thay kí hiệu </span><span class="fontstyle2">%p </span><span class="fontstyle0">thành </span><span class="fontstyle2">%d</span><span class="fontstyle0">, bạn sẽ nhận được một số thập phân mà bạn biết.
Nếu bạn chạy chương trình này trên máy tính của bạn, địa chỉ sẽ khác hoàn toàn. Tất cả phụ thuộc vào phần trống có trong bộ nhớ, chương trình bạn đang dùng,... Hoàn toàn không có khả năng báo trước địa chỉ nào của biến số sẽ được cấp. Nếu bạn thử chạy chương trình liên tục nhiều lần, địa chỉ có thể sẽ không đổi trong thời điểm đó. Nhưng nếu bạn khởi động lại máy tính, chương trình chắc chắn sẽ hiển thị một giá trị khác.
Vậy chúng ta sẽ làm gì với tất cả những thứ đó?
Tôi cần bạn nẵm vững những điều sau:

</span>
1. <span class="fontstyle2">tuoi</span><span class="fontstyle0">: tượng trưng cho </span><span class="fontstyle4">giá trị </span><span class="fontstyle0">của biến số.</span>

2. <span class="fontstyle2">&tuoi</span><span class="fontstyle0">: tượng trưng cho </span><span class="fontstyle4">địa chỉ </span><span class="fontstyle0">của biến số.</span>

<span class="fontstyle0">Với </span><span class="fontstyle2">tuoi</span><span class="fontstyle0">, máy tính sẽ đọc và gửi lại giá trị của biến số.
Với </span><span class="fontstyle2">&tuoi</span><span class="fontstyle0">, máy tính sẽ nói với chúng ta ở địa chỉ nào sẽ tìm thấy biến số.</span>

<span class="fontstyle0">***Cách sử dụng pointers (con trỏ)***

</span><span class="fontstyle2">Đến bây giờ, bạn chỉ có thể tạo biến số để chứa các số hạng. Và sau đây chúng ta sẽ học cách tạo ra những biến số chứa địa chỉ của chúng, những biến số này gọi là con trỏ.</span>

<span class="fontstyle0">Cách tạo một con trỏ

</span><span class="fontstyle2">Để tạo một biến số dạng con trỏ, ta cần phải thêm kí tự * trước tên của biến số.</span>

```
int *pointer;

```

<span class="fontstyle0">Giống như điều tôi dạy bạn khi khai báo biến số, bạn cần cho nó giá trị ngay khi khởi tạo, rất quan trọng, bằng cách cho nó giá trị 0 (lấy ví dụ với biến số). Và đối với con trỏ, điều này còn quan trọng hơn nữa! Để khởi tạo con trỏ, có nghĩa là cho nó một giá trị mặc định, người ta không dùng giá trị 0 mà dùng từ khóa </span><span class="fontstyle2">NULL </span><span class="fontstyle0">(phải được viết hoa):</span>

```
int *pointer = NULL;

```

<span class="fontstyle0">Bạn đã khởi tạo một con trỏ giá trị </span><span class="fontstyle2">NULL</span><span class="fontstyle0">. Như vậy, bạn chắc rằng con trỏ của bạn không chứa địa
chỉ nào.
Việc này diễn ra như thế nào? Đoạn mã trên sẽ đặt trước một chỗ trong bộ nhớ, giống như cách
bạn tạo ra một biến số thông thường. Nhưng điều thay đổi ở đây là giá trị của con trỏ chỉ dùng để
chứa địa chỉ của một biến số khác.</span>

<span class="fontstyle0">Vậy thử xem vơi địa chỉ của </span><span class="fontstyle2">tuoi </span><span class="fontstyle0">thì sao?
Và đây là cách chỉ ra địa chỉ của một biến số (</span><span class="fontstyle2">tuoi</span><span class="fontstyle0">) dựa trên giá trị của nó (bằng cách sử dụng kí tự &), nào bắt đầu thôi!</span>

```
int tuoi = 10;
int *pointerTuoi = &tuoi;

```

Dòng thứ nhất : "Tạo một biến số type int có giá trị là 10".
Dòng thứ hai : "Tạo một con trỏ có giá trị là địa chỉ của biến số tuoi".
Dòng thứ hai thực hiện cùng lúc hai việc. Nếu bạn thấy phức tạp nên không muốn gộp hai việc với
nhau, tôi sẽ tách biệt chúng bằng cách chia thành hai giai đoạn, xem đoạn code sau :

```
int tuoi = 10;
int *pointerTuoi; // 1) co nghia la "Toi tao mot con tro poiterTuoi"
pointerTuoi = &tuoi; // 2) co nghia la "con tro pointerTuoi chua dia chi cua bien so tuoi"

```

Bạn cần nhớ rằng không có type "pointer" như type int hay double. Người ta không ghi như sau:

pointer pointerTuoi;

Thay vì vậy, chúng ta sẽ sử dụng kí tự *, sau int. Tại sao lại như vậy? Thật ra, chúng ta cần phải chỉ rõ type của biến số mà con trỏ sẽ chứa địa chỉ của nó.
Ở trên, pointerTuoi sẽ chứa địa chỉ của biến số tuoi (type là int), vậy con trỏ phải có type int* Nếu biến số tuoi có type là double, ta phải viết double *pointerTuoi.
Giá trị của con trỏ pointerTuoi chỉ ra địa chỉ của biến số tuoi.
<img class="alignnone wp-image-53" src="http://hoctuduylaptrinh.com/wp-content/uploads/2016/12/pointer-229x300.png" alt="pointer" width="344" height="451" />

Trong biểu đồ trên, biến số tuoi được đặt vào ô địa chỉ 177450 (và bạn thấy tại đó giá trị tương ứng là 10), và con trỏ pointerTuoi được đặt vào ô địa chỉ 3 (tất cả địa chỉ đều được chọn ngẫu nhiên, và các địa chỉ trong biểu đồ cũng do tôi tự viết ra ).
Khi con trỏ được tạo ra, hệ điều hành sẽ dành một ô trong bộ nhớ giống như cách nó tạo ra với biến số tuoi. Khác nhau là giá trị của pointerTuoi là địa chỉ của biến số tuoi.
Chúng ta bắt đầu tiến vào thế giới huyền diệu của những con trỏ. Thế giới bí mật của những chương trình viết trên ngôn ngữ C (C++).
Hiển nhiên, nó không giúp máy tính bạn biến đổi thành máy làm ra café. Chỉ là, ta có một con trỏ
pointerTuoi chứa địa chỉ của biến số tuoi. Hãy dùng printf xem thử nó chứa gì trong đó:

```
int tuoi = 10;
int *pointerTuoi = &tuoi;
printf ("%d", pointerTuoi);

```

Kết quả

```
177450

```

uhm, thật sự điều này không có gì ngạc nhiên lắm. Người ta yêu cầu giá trị chứa trong pointerTuoi và đó là địa chỉ của biến số tuoi (177450).
Vậy làm sao có được giá trị của biến số mà pointerTuoi chỉ vào?
Chúng ta phải đặt kí tự * trước tên của con trỏ:

```
int tuoi = 10;
int *pointerTuoi = &tuoi;
printf ("%d", *pointerTuoi);

```

Kết quả

```
10

```

Đó, bạn làm được rồi đấy! Bằng cách đặt kí tự * trước tên con trỏ, ta nhận được giá trị của biến số tuoi.

Nếu chúng ta sử dụng kí tự & trước tên của con trỏ, chúng ta sẽ nhận được địa chỉ để tìm thấy con trỏ (trong trường hợp này là 3).
Những điều cần nắm vững

Đây là những điều mà bạn cần hiểu và nắm vững trước khi tiếp tục bài học:

1. Đối với một biến số, lấy ví dụ biến số tuoi:

tuoi có nghĩa là: "Tôi muốn giá trị của biến số tuoi",

&tuoi có nghĩa là: "Tôi muốn địa chỉ để tìm thấy biến số tuoi";

2. Đối với một con trỏ, lấy ví dụ con trỏ pointerTuoi:

pointerTuoi có nghĩa là: "Tôi muốn giá trị của con trỏ pointerTuoi" (giá trị này là địa chỉ của một biến),

*pointerTuoi có nghĩa là: "Tôi muốn giá trị của biến số mà con trỏ pointerTuoi chỉ vào".

<span class="fontstyle0">Cách sử dụng con trỏ trong một function
</span><span class="fontstyle2">Điều khá thú vị ở con trỏ là chúng ta có thể sử dụng chúng trong các function để có thể thay đổi trực tiếp giá trị của biến số trong bộ nhớ chứ không phải một bản sao như bạn đã thấy ở đoạn đầu bài học.
Vậy nó hoạt động như thế nào? Có rất nhiều cách thức để sử dụng. Đây là ví dụ đầu tiên:</span>

```
void triplePointer(int *pointerSoHang);
int main (int argc, char *argv[ ])
{
	int soHang = 5;
	triplePointer(&soHang); // Ta gui dia chi cua soHang vao function
	printf ("%d", soHang); /* Ta hien thi bien so soHang. Va function da truc tiep thay doi gia tri cua bien so vi no biet dia chi cua bien so nay */
	return 0;
}
void triplePointer(int *pointerSoHang)
{
	*pointerSoHang *= 3; // Ta x3 gia tri cua so hang duoc dua vao
}

```

Và đây là những gì diễn ra theo thứ tự, bắt đầu bởi function main:
1. Một biến số soHang được tạo ra trong main. Khởi tạo với giá trị 5. 

2. Ta gọi function triplePointer. Ta gửi vào parameter địa chỉ của biến số. 

3. Function triplePointer nhận địa chỉ là giá trị của pointerSoHang. Và trong funtion triplePointer, ta có một con trỏ pointerSoHang chứa địa chỉ của biến số soHang 

4. lúc này, ta có một con trỏ chỉ lên biến số soHang, ta đã có thể thay đổi trực tiếp giá trị của biến số soHang trong bộ nhớ! Chỉ cần dùng *pointerSoHang để điều chỉnh giá trị của biến số soHang! Ở ví dụ trên, người ta chỉ đơn giản thực hiện: nhân 3 lần giá trị của biến số soHang. 

5. kết thúc bằng return trong function main, lúc này soHang đã có giá trị 15 vì function triplePointer đã trực tiếp thay đổi giá trị của nó. 

Tất nhiên, tôi có thể thực hiện return để trả về giá trị như cách chúng ta đã học trong bài học về function. Nhưng điều thú vị ở đây là, bằng cách sử dụng con trỏ, chúng ta có thể thay đổi giá trị của nhiều biến số trong bộ nhớ (có nghĩa là "chúng ta có thể trả về nhiều giá trị"). Không còn giới hạn một giá trị duy nhất được trả về nữa !
Điều này phụ thuộc vào bạn và chương trình bạn viết. Chúng ta cần hiểu là cách dùng return để trả về giá trị là một cách viết khá đẹp và được sử dụng thường xuyên trong C.
Và thường xuyên nhất, người ta dùng return để thông báo lỗi của chương trình: ví dụ, function trả về 1 (true) nếu tất cả diễn ra bình thường, và 0 (false) nếu có lỗi trong chương trình.Một cách khác để sử dụng con trỏ trong function.
Trong những code source mà chúng ta vừa thấy, không có con trỏ trong function main. Duy nhất chỉ biến số soHang.

Con trỏ duy nhất được sử dụng nằm trong function triplePointer (có type int *)

Bạn cần biết rằng có cách viết khác cho đoạn code vừa rồi bằng cách thêm vào con trỏ trong function main:

```
void triplePointer(int *pointerSoHang);
int main (int argc, char *argv[ ])
{
	int soHang = 5;
	int *pointer = &soHang; // con tro nhan dia chi cua bien so soHang
	triplePointer (pointer); // Ta dua con tro (dia chi cua soHang) vao function
	printf ("%d", *pointer); // Ta hien thi gia tri cua soHang voi *pointer
	return 0;
}
void triplePointer(int *pointerSoHang)
{
	*pointerSoHang *= 3; // Ta x3 gia tri cua soHang
}

```

Hãy so sánh đoạn code source này với đoạn code source trước đó. Có một số thay đổi nhưng chúng sẽ cho ta cùng một kết quả.

Điều cần xét đến là cách đưa địa chỉ của biến số soHang vào function, cách sử dụng địa chỉ của biến số soHang. Điều khác biệt xảy ra ở đây là cách tạo con trỏ trong function main.
VD trong printf, tôi muốn hiển thị giá trị của biến số soHang bằng cách viết *pointer. Bạn cần biết rằng tôi vẫn thể viết soHang: kết quả sẽ giống nhau vì*pointer và soHang đều có chung một giá trị trong bộ nhớTrong chương trình "Lớn hơn hay nhỏ hơn", chúng ta đã sử dụng con trỏ bất chấp việc biết nó là gì, trong việc sử dụng function scanf.

Thật ra, function này có tác dụng đọc những thông tin mà người dùng nhập vào bàn phím và gửi lại kết quả.
Để scanf có thể thay đổi trực tiếp giá trị của một biến số bằng cách nhập từ bàn phím, ta cần địa chỉ của biến số đó:

```
int soHang = 0;
scanf ("%d", &soHang);

```

function làm việc với con trỏ của biến số soHang và có thể thay đổi trực tiếp giá trị của soHang.
Và như chúng ta biết, chúng ta có thể làm như sau:

```
int soHang = 0;
int *pointer = &soHang;
scanf ("%d", pointer);

```

Chú ý là ta không đặt kí tự & trước pointer trong function scanf Tại đây, pointer bản thân nó đã là địa chỉ của biến số soHang, không cần thiết phải thêm & vào nữa !

Nếu bạn làm điều đó, bạn sẽ đưa cho scanf địa chỉ của pointer: nhưng thứ chúng ta cần là địa chỉ của soHang.

Giải quyết vấn đề nan giải ở đầu bài?

Đã đến lúc chúng ta xem lại tâm điểm của bài học. Nếu bạn hiểu bài học này, bạn đã có thể tự giải quyết vấn đề đặt ra. Hãy thử đi! trước khi xem kết quả tôi đưa bạn:

```
#include 
#include 
void chuyenDoi(int *pointerGio, int *pointerPhut);
int main (int argc, char *argv[ ])
{
	int gio = 0, phut = 90;
	// Ta dua vao dia chi cua gio va phut
	chuyenDoi(&gio, &phut);
	// Luc nay, gia tri cua chung da duoc thay doi !
	printf ("%d gio va %d phut", gio, phut);
	return 0;
}
void chuyenDoi(int *pointerGio, int *pointerPhut)
{
	/*Note: dung quen dat dau * o phia truoc ten cua con tro! Bang cach nay ban co the thay doi
	gia tri cua bien so chu khong phai dia chi của no! Han la ban khong muon chia dia chi cua no
	dung khong? */
	*pointerGio = *pointerPhut / 60;
	*pointerPhut = *pointerPhut % 60;
}

```

Không có gì khiến bạn ngạc nhiên trong đoạn code source này. Và như mọi khi, để tránh những nhầm lẫn không đáng có, tôi sẽ giải thích những gì đã diễn ra để chắc chắn rằng các bạn theo kịp tôi, vì đây là một bài học quan trọng, bạn cần cố gắng rất nhiều để hiểu, và tôi cũng cố gắng hết sức để giải thích rõ ràng giúp các bạn hiểu:

1. Biến số gio và phut được khởi tạo trong function main.

2. Ta gửi vào function chuyenDoi địa chỉ của gio và phut.

3. Function chuyenDoi nhận địa chỉ bằng cách đưa vào các con trỏ pointerGio và pointerPhut. Bạn cần biết rằng, cách gọi tên con trỏ không quan trọng. Tôi có thể gọi là g và p, hoặc cũng có thể là gio và phut.

4. function chuyenDoi thay đổi trực tiếp các giá trị của gio và phut trong bộ nhớ vì nó đã có địa chỉ của chúng trong các con trỏ. 

Và điều cần biết ở đây, tuyệt đối chấp hành, là phải đặt * trước tên của con trỏ nếu như ta muốn thay đổi giá trị của gio và phut. 

Nếu ta không làm việc này, ta sẽ thay đổi địa chỉ chứa trong con trỏ, và nó chẳng giúp ta được gì.
