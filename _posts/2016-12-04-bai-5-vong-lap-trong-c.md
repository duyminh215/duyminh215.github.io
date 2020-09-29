---
layout: post
title: "Bài 5: Vòng lặp trong C"
category: C
tags: [C++]
date: 2016-12-04
---
Ở bài học trước chúng ta đã được học thiết lập các điều kiện, trong bài này, chúng ta sẽ học cách sử dụng vòng lặp trong ngôn ngữ C.

***Vòng lặp là gì?***
Vòng lặp là phương pháp giúp ta lặp lại nhiều lần các dòng lệnh.

Chúng ta sẽ tìm hiểu 3 dạng vòng lặp trong ngôn ngữ C:
1. while
2. do...while
3. for
<img class="alignnone size-medium wp-image-40" src="http://hoctuduylaptrinh.com/wp-content/uploads/2016/12/loop-300x163.png" alt="loop" width="300" height="163" />

Cách máy tính thực hiện lệnh với vòng lặp như sau:

Máy tính thực hiện các dòng lệnh từ cao xuống thấp:

i. Khi đến cuối vòng lặp, nó quay lại dòng lệnh đầu tiên.

ii. Nó chạy lại các dòng lệnh từ cao xuống thấp.

iii. ...Và cứ lặp lại như vậy

Nếu mà chúng ta không dừng lại thì máy tính sẽ tiếp tục thực hiện các câu lệnh đó. Vậy thì làm sao để không lặp lại mãi. Chúng ta cần những điều kiện.

Khi chúng ta thực hiện một vòng lặp, chúng ta phải tạo một điều kiện. Điều kiện có nghĩa là "lặp lại các câu lệnh nếu điều kiện này vẫn đúng".

***Vòng lặp while***

Chúng ta hãy thử một ví dụ:

```
#include<stdio.h>
#include<stdlib.h>

int main(){
	
    int counter = 0;
    while (counter < 10)
    {
        printf ("Xin chao cac ban !\\n");
        counter++;
    }
    return 0;
}

```

Chúng ta hãy cùng phân tích chương trình trên. Chương trình trên khai báo một biến đếm counter với giá trị counter ban đầu bằng 0. Câu lệnh tiếp theo, chương trình sẽ kiểm tra xem counter có bé hơn 10 hay không.

Lúc này counter = 0 nên bé hơn 10, do đó chương trình sẽ vào vòng lặp và thực hiện in ra màn hình dòng chữ "Xin chao cac bạn!". Sau khi in ra màn hình dòng chữ đó, biến counter sẽ được tăng giá trị lên 1.

Chương trình lại quay lại kiểm tra counter có bé hơn 10. Mà counter = 1 thì bé hơn 10 nên sẽ tiếp tục thực hiện các lệnh in ra và tăng couter như trên. Cứ tiếp tục như vậy, counter sẽ tăng lên thành 2,3,4,5,6,7,8,9. Cho đến lúc counter = 10, chương trình kiểm tra xem counter có bé hơn 10 hay không. Lúc này counter đã bằng 10 rồi nên vòng lặp sẽ dừng lại.

Vậy là chúng ta đã thấy chương trình với vòng lặp while thì điều kiện rất quan trọng. Nếu không có điều kiện này chương trình sẽ chạy cho đến lúc máy tính tắt. Nếu chương trình nào mà thực hiện các dòng lệnh phức tạp và tốn tài nguyên hệ thống mà không dừng lại được sẽ rất hại cho máy tính, gây đơ máy.

***Vòng lặp do...while***

Thử lại ví dụ trên nhưng có khác biệt một chút:

```
#include<stdio.h>
#include<stdlib.h>

int main(){
	
    int counter = 0;
    do
    {
        printf ("Xin chao cac ban !\\n");
        counter++;
    }while (counter < 10);
    return 0;
}

```

Dạng vòng lặp này cũng tương tự như while, nhưng ít được sử dụng hơn. Điều khác biệt so với while là vị trí điều kiện. Với while thì điều kiện nằm ở đầu còn do...while thì điều kiện nằm ở cuối.

Vậy khác biệt ở đây là gì?

Vòng lặp while sẽ luôn kiểm tra điều kiện rồi mới thực hiện lệnh. Nghĩa là điều kiện ban đầu mà đã sai thì sẽ không thực hiện lệnh nào cả. Ví nếu counter = 11 ngay từ đầu thì ví dụ 1 sẽ không in ra màn hình dòng chữ nào cả.

Với do...while thì nó thực hiện ít nhất 1 lần. Nghĩa là nó chắc chắn in ra 1 lần dòng chữ "Xin chao cac ban". Sau đó nó sẽ kiểm tra điều kiện counter. Ví dụ nếu counter = 50 thì vẫn in ra được 1 lần. Tuy vậy, ở ví dụ vừa xong, counter = 0 nên nó cũng sẽ thực hiện 10 lần và in ra 10 dòng "Xin chao cac ban".

***Vòng lặp for***

Vòng lặp for được sử dụng khá nhiều trong lập trình. Theo như kinh nghiệm bản thân mình thì vòng lặp này được sử dụng nhiều hơn so với vòng lặp while.

Bắt đầu luôn bằng ví dụ về vòng lặp for:

```
#include<stdio.h>
#include<stdlib.h>

int main(){
	
    int counter = 0;
    for(counter = 0; counter < 10; counter++){
        printf("Xin chao cac ban\\n");
    }
    return 0;
}

```

Có bao nhiêu điểm khác biệt? 
1. Bạn có thể thấy rằng chúng ta đã không khai báo giá trị của biến số ngay sau khi tạo ra nó (nhưng chúng ta có quyền làm điều đó)

2. Có rất nhiều thứ trong ngoặc sau for (chúng ta sẽ xem xét sau).</li>

3. Cũng không có counter++ trong vòng lặp giống như khi dùng vòng lặp while. Nó được tìm thấy trong ngoặc ( ) và cũng chính điểm này khiến vòng lặp for trở nên thú vị.

<span class="fontstyle0">Có 3 instructions viết ngắn gọn trong ngoặc và chúng </span><span class="fontstyle2">cách nhau bởi những dấu chấm phẩy:</span>

1. <span class="fontstyle0">instruction đầu tiên </span><span class="fontstyle2">dùng để khai báo</span><span class="fontstyle0">: khai báo biến số </span><span class="fontstyle4">counter</span><span class="fontstyle0">. Trong trường hợp của chúng ta, biến số có giá trị là 0.</span></li>

2. <span class="fontstyle0">instruction thứ hai là </span><span class="fontstyle2">điều kiện</span><span class="fontstyle0">: giống như vòng lặp while, đây là điều kiện để vòng lặp được thực hiện. Khi điều kiện vẫn còn đúng, thì vòng lặp lại sẽ được tiếp tục.</span></li>

3. <span class="fontstyle0">Cuối cùng có một </span><span class="fontstyle2">increment </span><span class="fontstyle0">ở đây: instruction cuối cùng sẽ được thực hiện ở cuối mỗi vòng lặp để cập nhật giá trị của biến số counter. Tương tự, chúng ta cũng có thể thực hiện decrement (</span><span class="fontstyle4">counter--;</span><span class="fontstyle0">) hoặc bất kì dạng phép tính nào (</span><span class="fontstyle4">counter += 2</span><span class="fontstyle0">)</span><span class="fontstyle4">; </span><span class="fontstyle0">để tăng hoặc giảm giá trị cho những biến số.</span>

<span class="fontstyle0">Tóm lại, giống như ta đã thấy vòng lặp </span><span class="fontstyle2">for </span><span class="fontstyle0">không có gì khác biệt ngoài một số thứ được viết ngắn
gọn hơn so với vòng lặp </span><span class="fontstyle2">while
</span><span class="fontstyle0">Hãy nắm vững nó, chúng ta sẽ cần sử dụng nó rất nhiều lần!</span>

***Các lỗi hay gặp khi làm việc với vòng lặp***

Lỗi điều kiện trong vòng lặp while hoặc do...while.

Các bạn không đưa ra điều kiện đúng để thực hiện hoặc điều kiện không có điểm dừng. Như ở ví dụ counter ở trên, nếu bạn nào thiếu dòng lệnh counter++ thì chương trình sẽ chạy mãi. Bởi vì counter = 0 luôn bé hơn 10 nên chương trình sẽ lặp mãi.

Thừa dấu ; sau điều kiện while.

Ví dụ:

```
while(counter < 10);
```

Không thụt vào một tab ở trong vòng lặp while hoặc for. Lưu ý trong các ví dụ trên, ở trong vòng lặp while hoặc for, code luôn thụt vào một tab. Cái này để chúng ta hiểu rằng các câu lệnh này được thực hiện trong vòng lặp. Do đó các bạn chú ý để code chương trình nhìn dễ hiểu hơn.

<span style="color: #ff0000;">***Bài tập cho các bạn:***</span>

<span style="color: #ff0000;">Sử dụng while, tính tổng các số từ 0 đến 100.</span>

<span style="color: #ff0000;">Sử dụng while, tính tổng sau: tong = 1/1 + 1/2 + ...+ 1/n với n là 100.</span>

<span style="color: #ff0000;">Sử dụng while, tính trung bình cộng các số lẻ từ 0 đến 100.</span>

<span style="color: #ff0000;">Sử dụng for, tính tổng các số chẵn từ 0 đến 100.</span>

<span style="color: #ff0000;">Sử dụng for, tính trung bình cộng từ 0 đến 100.</span>

<span style="color: #ff0000;">Sử dụng for, vẽ hình vuông bằng các dấu *. </span>

<span style="color: #ff0000;">Sử dụng for, vẽ hình tam giác vuông bằng dấu *.</span>
