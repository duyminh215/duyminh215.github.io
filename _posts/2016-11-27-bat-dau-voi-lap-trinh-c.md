---
layout: post
title: "Bắt đầu với lập trình C"
category: Java
tags: [C, C++]
date: 2016-11-27
---
Xin chào các bạn, hôm nay mình sẽ bắt đầu viết bài về lập trình C cơ bản cho người mới bắt đầu. 

Nếu các bạn theo dõi các bài viết này của mình các bạn sẽ học cách lập trình với kiến thức ban đầu bằng không. 

Do vậy các bạn không cần lo lắng hay thắc mắc là mình có cần kiến thức có sẵn hay không.

Nói trước với các bạn là mình sẽ dạy các bạn học lập trình C trên môi trường Linux (Ubuntu) nên các bạn sẽ cần cài đặt hệ điều hành Ubuntu lên máy các bạn. 

Tại sao lại học trên môi trường Linux? Câu hỏi này mình sẽ trả lời vào cuối khóa học này.

Để chuẩn bị học lập trình C, chúng ta cần chuẩn bị các phần mềm sau:

Môi trường: hệ điều hành Ubuntu.

Bộ biên dịch: g++

Một phần mềm để viết code: sublime Text 2.

Chúng ta bắt đầu thôi.

Chúng ta sẽ bắt đầu với chương trình "hello world".

Các bạn mở sublime Text và gõ đoạn mã sau:

```
#include<stdio.h>
int main(){

   printf("Hello world!\n");
   return 0;
}
```
Sau khi đã gõ (lưu ý là gõ chứ không được copy và paste vào sublime text), chúng ta sẽ lưu file vào folder "/home/username/Documents/codeC" với tên là "hello_word.cpp".

Để chạy chương trình C++ này chúng ta cần dịch thành mã máy. Muốn dịch chương trình, chúng ta sẽ sử dụng make file trên linux để dịch file "hello_word.cpp" thành file chạy.

Chúng ta sẽ tạo một make file với nội dung như sau:
```
all:
    g++ -g hello_world.cpp -o hello_world
```

Chúng ta sẽ lưu file này thành "make_file_hello_world" vào folder "/home/username/Documents/codeC" (cùng folder với file "hello_world.cpp" ở trên).

Sau khi đã tạo make file, chúng ta mở terminal lên (phần mềm để gõ lệnh trên Linux). Trên terminal, chúng ta gõ như sau:
```
cd /home/username/Documents/codeC
ls -la
make -f make_file_hello_world
```
Đó là các lệnh để biên dịch mã nguồn thành file chạy. Sau khi biên dịch xong, chúng ta sẽ thấy xuất hiện một file "hello_world" chính là file chạy. 

Lưu ý file "hello_world" chứ không phải "hello_world.cpp".

Để chạy file này, chúng ta sử dụng terminal và gõ như sau:

```
./hello_world
```
Các bạn sẽ thấy chữ "Hello world!" xuất hiện trên terminal.

Chúng ta bắt đầu đi tìm hiểu từng dòng lệnh trong bài "hello_world.cpp" ở trên.
```#include<stdio.h>``` là dòng lệnh để gọi phần input và output của hệ thống thư viện ngôn ngữ C.

Các bạn lưu ý là "stdio.h" chứ không phải "studio.h". "sdtio" là viết tắt của standard input output. 

Viết như vậy để các bạn đỡ nhầm. Thư viện này thực hiện các lệnh vào ra như là nhập liệu vào từ bàn phím, hiển thị thông tin ra trên màn hình.

```int main()```Đây là cách khai báo hàm main ở trong C. Chúng ta sẽ tìm hiểu thêm về hàm sau này. 

Các bạn cứ mặc định đây là hàm để chương trình C chạy.```printf("Hello world!\n");```là hàm ở trong thư viện "stdio.h" ở trên để hiển thị lên màn hình. 

Ở đây chúng ta sẽ in ra màn hình dòng chữ "Hello world!" còn ký tự "\n" là viết tắt của new line.

Nghĩa là trên màn hình sẽ xuất hiện chữ "Hello world!" và một dòng trắng bên dưới.

```   return 0;``` là kết quả trả về của hàm main này. Chúng ta sẽ tìm hiểu về phần return này trong phần học về hàm trong C.

Về phần biên dịch và make file, các bạn hãy đăng ký khóa học để tiếp tục học theo phương pháp này.

Như vậy là chúng ta đã học qua bài đầu tiên là hiển thị dòng chữ "Hello world!" lên màn hình. Rất đơn giản phải không? 

Các bài tiếp theo sẽ phức tạp dần lên. Các bạn hãy chờ xem nhé.



