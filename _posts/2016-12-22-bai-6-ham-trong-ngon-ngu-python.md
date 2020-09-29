---
layout: post
title: "Bài 6: Hàm trong ngôn ngữ Python"
category: Python
tags: [Python]
date: 2016-12-22
---

***Hàm là gì?***

Hàm là cách thuận tiện để chia code của bạn thành các block hữu ích, cho phép chúng ta sắp xếp lại code, làm cho nó dễ đọc hơn, có thể sử dụng lại nhiều lần và giảm thời gian phát triển sản phẩm. Hàm cũng là cách để định nghĩa các giao diện mà các lập trình viên có thể chia sẻ code của họ.

***Làm thế nào để viết một hàm trong Python***

Như chúng ta đã tìm hiểu ở các bài trước, một block code của Python được đánh dấu khi chúng có cùng các thụt đầu dòng. Ví dụ:

```
block_head:
    1st block line
    2nd block line
    ...

```

Hàm trong python được định nghĩa bắt đầu bằng chữ "def", theo sau là tên hàm và các dòng lệnh. Ví dụ như sau:

```
def my_function():
    print "Hello From My Function!"

```

Hàm còn có những tham số truyền vào (các tham số chính là các biến lúc hàm được gọi). Ví dụ:

```
def my_function_with_args(username, greeting):
    print "Hello, %s , From My Function!, I wish you %s" % (username, greeting)

```

Hàm cũng trả về một giá trị lúc được gọi, bằng cách sử dụng từ khóa "return". Ví dụ:

```
def sum_two_numbers(a, b):
    return a + b

```

***Bạn gọi hàm trong Python như thế nào?***

Đơn giản bạn chỉ cần viết tên hàm với cặp dấu () kèm theo và các tham số cần truyền vào ở trong ngoặc.  Ví dụ về cách sử dụng hàm:

```

# Define our 3 functions
def my_function():
    print "Hello From My Function!"

def my_function_with_args(username, greeting):
    print "Hello, %s , From My Function!, I wish you %s"%(username, greeting) 

def sum_two_numbers(a, b):
    return a + b

# print(a simple greeting)
my_function()

#prints - "Hello, John Doe, From My Function!, I wish you a great year!"
my_function_with_args("John Doe", "a great year!")

# after this line x will hold the value 3!
x = sum_two_numbers(1,2)
print x

```
