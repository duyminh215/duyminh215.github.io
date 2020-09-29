---
layout: post
title: "Bài 4: Điều kiện if else trong Python"
category: Python
tags: [Python]
date: 2016-12-20
---

Python sử dụng biến logic để quyết định điều kiện. Biến logic True và False được trả về khi một biểu thức được so sánh hay đánh giá. Ví dụ:

```
x = 2
print x == 2 # prints out True
print x == 3 # prints out False
print x &lt; 3 # prints out True

```

Chú ý rằng phép gán sử dụng một dấu "=" trong khi phép so sánh sử dụng 2 dấu "==". Còn phép so sánh khác thì dùng dấu "!=".
***Phép toán logic***

Phép and và or cho phép sử dụng nhiều biểu thức so sánh, ví dụ như sau:

```
name = "John"
age = 23
if name == "John" and age == 23:
    print "Your name is John, and you are also 23 years old."

if name == "John" or name == "Rick":
    print "Your name is either John or Rick."

```

***Phép logic "in"***

Phép logic "in" được dùng để kiểm tra xem một đối tượng có nằm trong một container (vd: list) hay không. Ví dụ

```
name = "John"
if name in ["John", "Rick"]:
    print "Your name is either John or Rick."

```

Python sử dụng các dấu thụt đầu dòng để đánh dấu một block code, thay vì dấu đóng mở ngoặc ({}). Chuẩn trong Python là 4 dấu cách, tuy nhiên dấu cách hay dấu tab đều được sử dụng.
Sau đây là một ví dụ về sử dụng if trong Python

```
if :
    
    ....
    ....
elif : # else if
    
    ....
    ....
else:
    
    ....
    ....


```

Ví dụ về code Python:

```
x = 2
if x == 2:
    print "x equals two!"
else:
    print "x does not equal to two."

```

Một biểu thức được trả về là đúng khi nó thỏa mãn một trong hai điều kiện sau:

1. Biến True được đưa ra, hoặc các biểu thức tính toán được là chính xác (như là phép so sánh). 

2. Một đối tượng không phải là "empty" được đưa ra.

Một số đối tượng được coi là empty là:

1. Một chuỗi rỗng: "" 
2. Một danh sách rỗng: [] 
3. Số 0 
4. Biến False 

***Phép toán "is"***

Không giống như phép so sánh bằng "==", phép "is" không match giá trị của biến số, mà match một instance. Ví dụ:

```
x = [1,2,3]
y = [1,2,3]
print x == y # Prints out True
print x is y # Prints out False

```

***Phép not***

Sử dụng not trước một biểu thức để đảo ngược nó. Ví dụ

```
print (not False) # Prints out True
print ((not False) == (False)) # Prints out False

```
