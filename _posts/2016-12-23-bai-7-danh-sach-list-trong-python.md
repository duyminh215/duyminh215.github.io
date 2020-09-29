---
layout: post
title: "Bài 7: Danh sách (list) trong Python"
category: Python
tags: [Python]
date: 2016-12-23
---

Danh sách rất giống với mảng. Không giống như các ngôn ngữ bắt buộc phải chứa các phần từ cùng loại, danh sách trong python có thể chứa bất cứ loại dữ liệu nào và bao nhiêu phần tử cũng được. Chúng ta có thể lướt qua danh sách một cách rất đơn giản như sau:

```
mylist = []
mylist.append(1)
mylist.append(2)
mylist.append(3)
print mylist[0] # prints 1
print mylist[1] # prints 2
print mylist[2] # prints 3

# prints out 1,2,3
for x in mylist:
    print x

```

Nếu bạn muốn lấy phần tử thứ n mà n không nằm trong danh sách thì sẽ gây ra lỗi.

```
mylist = [1,2,3]
print mylist[10]

```

<span style="color: #ff0000;">***Bài tập:***</span>

Trong bài tập này, bạn cần phải thêm các số và các chuỗi string để làm cho danh sách chính xác bằng cách sử dụng hàm append của list. Bạn cần phải thêm các số 1,2,3 vào trong danh sách "numbers", các từ "hello" và "world" vào các biến strings.
Bạn cũng phải gán giá trị chính xác cho biến second_name với cái tên thứ 2 trong danh sách tên. Chú ý rằng index bắt đầu từ 0, nếu bạn muốn lấy phần tử thứ 2 thì index của nó là 1. Hãy sửa đoạn code sau để chương trình chạy chính xác.

```
numbers = []
strings = []
names = ["John", "Eric", "Jessica"]

# write your code here
second_name = None


# this code should write out the filled arrays and the second name in the names list (Eric).
print numbers
print strings
print "The second name on the names list is %s" % second_name

```
