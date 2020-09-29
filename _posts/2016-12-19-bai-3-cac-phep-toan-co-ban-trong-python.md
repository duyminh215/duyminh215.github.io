---
layout: post
title: "Bài 3: Các phép toán cơ bản trong Python"
category: Python
tags: [Python]
date: 2016-12-19
---

Như các bạn đã biết, ở bài học trước, chúng ta đã học cách khai báo biến trong Python. Bài học này chúng ta sẽ học cách sử dụng một số phép toán cơ bản trong ngôn ngữ Python.

***Các phép toán số học***

Cũng giống như các ngôn ngữ lập trình khác, Python sử dụng các phép cộng, trừ, nhân, chia với các số. Chúng ta thử ví dụ sau:

```
number = 1 + 2 * 3 / 4.0
print number

```

Các bạn có đoán được kết quả không? Theo các bạn, Python có tính theo trật tự số học thông thường. Các bạn hãy tự chạy đoạn code trên để tự kiểm nghiệm nhé.
Một phép toán khác là phép lấy số dư (modulo). Chúng ta hãy thử ví dụ sau:

```
remainder = 11 % 3
print remainder

```

Ngoài ra, chúng ta còn sử dụng dấu nhân hai lần để thể hiện lũy thừa của một số. Chúng ta hãy xem ví dụ sau:

```
squared = 7 ** 2
cubed = 2 ** 3

```

Hàm trên tương ứng với lấy bình phương của 7, lấy lập phương của 2.

***Sử dụng phép toán với chuỗi (string) trong Python***

Python hỗ trợ việc nối các chuỗi bằng dấu cộng (+). Chúng ta hãy xem ví dụ này:

```
helloworld = "hello" + " " + "world"
print helloworld

```

Python cũng hỗ trợ việc nhân các chuỗi lên nhiều lần bằng dấu nhân (*). Chúng ta hãy thử ví dụ:

```
lotsofhellos = "hello" * 10
print lotsofhellos

```

***Sử dụng phép toán với danh sách (list)***

Các chuỗi có thể được nối với nhau bằng dấu cộng (+). Hãy xem xét ví dụ sau:

```
even_numbers = [2,4,6,8]
odd_numbers = [1,3,5,7]
all_numbers = odd_numbers + even_numbers

```

Cũng giống như chuỗi, Python hỗ trợ việc nhân một list lên nhiều lần. Ví dụ như sau:

```
print [1,2,3] * 3

```

<span style="color: #ff0000;">***Bài tập:***</span>

Mục tiêu của bài này là tạo ra 2 list là x_list và y_list, mỗi list chứa 10 phần tử của biến x và y. Bạn cũng được yêu cầu phải tạo một list là big_list, big_list này chứa 10 biến x và 10 biến y bằng cách cộng hai danh sách đó lại với nhau.

Bạn hãy sửa đoạn code sau để nó giải quyết được bài toán trên.

```
x = object()
y = object()

# TODO: change this code
x_list = [x]
y_list = [y]
big_list = []

print "x_list contains %d objects" % len(x_list)
print "y_list contains %d objects" % len(y_list)
print "big_list contains %d objects" % len(big_list)

# testing code
if x_list.count(x) == 10 and y_list.count(y) == 10:
    print "Almost there..."
if big_list.count(x) == 10 and big_list.count(y) == 10:
    print "Great!"

```
