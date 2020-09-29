---
layout: post
title: "Bài 9: Đọc và ghi file trong Python"
category: Python
tags: [Python]
date: 2016-12-31
---

***Đóng và mở file trong Python***

Python cung cấp một số hàm  và phương thức cơ bản để điều khiển file. Bạn có thể hầu hết điều khiển file bằng đối tượng "file".

***Hàm open***

Trước khi bạn muốn đọc hay ghi một file, bạn cần mở file đó bằng hàm open(). Hàm này sẽ tạo ra một đối tượng (object) ***file,*** đối tượng này sẽ dùng để điểu khiển file.

```
file object = open(file_name [, access_mode][, buffering])

```

Các tham số:

1. file_name: tham số file_name là một chuỗi chứa tên của một file mà bạn muốn tác động.

2. access_mode: access_mode sẽ quyết định chế độ mà file sẽ mở, ví dụ như đọc, ghi, thêm dòng,...Đây là một tham số tự chọn (có thể có hoặc không cần truyền vào) và chế độ mặc định là đọc (read).

3. buffering: nếu giá trị này bằng 0 thì không có buffering cần. Nếu giá trị này bằng 1, buffering các dòng sẽ được thực hiện.

Các chế độ mở file:

[table id=2 /]

***Các thuộc tính trong đối tượng (object) file***

Một khi file đã mở bạn sẽ có một đối tượng file, bạn có thể lấy được một số thông tin từ đối tượng file này.

file.closed trả về true nếu file đã đóng, false với các trường hợp khác.

file.mode trả về chế độ mở của file.

file.name trả về tên của file.

file.softspace trả về false nếu không gian rõ ràng cần thiết cho việc print, các trường hợp lại là true

Ví dụ:

```
#!/usr/bin/python

# Open a file
fo = open("foo.txt", "wb")
print "Name of the file: ", fo.name
print "Closed or not : ", fo.closed
print "Opening mode : ", fo.mode
print "Softspace flag : ", fo.softspace

```

Kết quả sẽ là:

```
Name of the file:  foo.txt
Closed or not :  False
Opening mode :  wb
Softspace flag :  0

```

***Hàm close()***
Hàm close() sẽ xóa hết tất cả thông tin đang chờ để ghi và đóng file lại, sau hàm này sẽ không có thông tin nào được ghi.
Python sẽ tự động đóng một file sau khi đối tượng file đó được gán cho file khác.
Ví dụ

```
#!/usr/bin/python

# Open a file
fo = open("foo.txt", "wb")
print "Name of the file: ", fo.name

# Close opend file
fo.close()

```

***Đọc và ghi file***

Đối tượng file cung cấp cho chúng ta một số hàm để chúng ta có thể tương tác với file rất dễ dàng.

***Hàm write()***

Hàm write() sẽ ghi một chuỗi kí tự bắt kì vào file. Chú ý rằng, chuỗi Python có thể là binary hoặc ký tự. Hàm này không thêm ký tự dòng mới (new line \\n) vào cuối chuỗi.

Ví dụ:

```
#!/usr/bin/python

# Open a file
fo = open("foo.txt", "wb")
fo.write( "Python is a great language.\\nYeah its great!!\\n");

# Close opend file
fo.close()

```

Ví dụ trên sẽ tạo ra một file mới có tên là "foo.txt" và ghi nội dung chuỗi ký tự vào file, sau đó file sẽ được đóng lại. Nếu bạn mở file lên bạn sẽ thấy nội dung file như sau:

```
Python is a great language.
Yeah its great!!

```

***Hàm read()***

Hàm read sẽ dùng để đọc một chuỗi từ một file đã mở. Chú ý chuỗi ở đây có thể là binary hoặc text.

Hàm cụ thể như sau:

```
fileObject.read([count]);

```

Chú ý tham số count được truyền vào là số bytes được đọc từ file đã mở. Hàm này sẽ đọc từ đầu file đến bytes count thì dừng lại. Nếu count không được truyển thì nó sẽ đọc nhiều nhất có thể, có thể đến cuối file.
Ví dụ:

```
#!/usr/bin/python

# Open a file
fo = open("foo.txt", "r+")
str = fo.read(10);
print "Read String is : ", str
# Close opend file
fo.close()

```

Kết quả:

```
Read String is :  Python is

```

***Đổi tên và xóa file***

Module ***os ***trong Python cung cấp công cụ cho bạn để xử lý file, như đổi tên hay xóa file.

Để dụng được module này bạn cần import nó trước.

***Hàm rename()***

Hàm này có 2 tham số, tên hiện tại và tên mới.

Ví dụ:

```
#!/usr/bin/python
import os

# Rename a file from test1.txt to test2.txt
os.rename( "test1.txt", "test2.txt" )

```

***Hàm remove()***

Bạn có thể sử dụng hàm remove() để xóa file bằng cách cung cấp tên file mà bạn muốn xóa.

Ví dụ:

```
#!/usr/bin/python
import os

# Delete file test2.txt
os.remove("text2.txt")

```
