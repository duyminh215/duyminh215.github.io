---
layout: post
title: "Bài 2: Sử dụng biến trong Python"
category: Python
tags: [Python]
date: 2016-12-17
---

Ở bài học trước, chúng ta đã tìm hiểu để in ra một dòng chữ trên màn hình bằng Python. Rất đơn giản đúng không? Hôm nay chúng ta sẽ tìm hiểu cách khai báo và sử dụng biến trong ngôn ngữ Python.

Python là một ngôn ngữ hướng đối tượng và không ràng buộc kiểu dữ liệu. Bạn không cần phải khai báo biến trước khi sử dụng chúng hay là loại dữ liệu của biến. Mỗi biến trong Python đều là đối tượng.

***Biến số***

Python hỗ trợ hai kiểu biến số, đó là biến số nguyên và biến số thực (dấu phẩy động).

Để khai báo một biến thì bạn chỉ cần đơn giản viết như sau:

```
myint = 7
print myint

```

Để khai báo một biến số thực, bạn có thể sử dụng một trong hai cách sau:

```
myfloat = 7.0
print myfloat
myfloat = float(7)
print myfloat

```

***Biến chuỗi (String)***

Các chuỗi được định nghĩa với dấu nháy đơn hoặc dấu nháy kép như sau:

```
mystring = 'hello'
print mystring
mystring = "hello"
print mystring

```

Sự khác nhau giữa hai cách trên đó là sử dụng dấu nháy kép sẽ khiến cho nó dễ dàng để thể hiện các chuỗi có dấu nháy hơn. Ví dụ như sau:

```
mystring = "Don't worry about apostrophes"
print mystring

```

Việc có nhiều cách để khai báo biến chuỗi giúp cho ngôn ngữ Python rất dễ dàng để thể hiện chuỗi với nhiều ký tự phức tạp như là dấu xuống dòng, dấu gạch chéo và hỗ trợ ký tự Unicode.
Một số phép toán có thể được sử dụng cho cả số và ký tự như sau:

```
one = 1
two = 2
three = one + two
print three

hello = "hello"
world = "world"
helloworld = hello + " " + world
print helloworld

```

Ngoài ra, chúng ta có thể khai báo và gán biến đồng thời rất linh hoạt như sau:

```
a, b = 3, 4
print a,b

```

Kết hợp các phép toán giữa số và chuỗi không được hỗ trợ. Ví dụ sau đây sẽ không thể chạy được:

```
# This will not work!
one = 1
two = 2
hello = "hello"

print one + two + hello

```

<span style="color: #ff0000;">Hãy thử làm bài tập sau:</span>
Khai báo 1 biến chuỗi mystring và có giá trị là "hello". Một biến số thực float có tên là myfloat và có giá trị 10.0, và một biến số nguyên myint có giá trị 20.
Bạn hãy thay đổi đoạn code sau để nó có thể chạy được:

```
# change this code
mystring = None
myfloat = None
myint = None

# testing code
if mystring == "hello":
    print "String: %s" % mystring
if isinstance(myfloat, float) and myfloat == 10.0:
    print "Float: %f" % myfloat
if isinstance(myint, int) and myint == 20:
    print "Integer: %d" % myint

```

