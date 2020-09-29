---
layout: post
title: "Bài 5: Vòng lặp trong Python"
category: Python
tags: [Python]
date: 2016-12-21
---

Có hai kiểu vòng lặp trong Python, đó là vòng lặp for và while.

***Vòng lặp for***

Vòng lặp for chạy lần lượt theo tuần tự. Ví dụ như sau:

```
primes = [2, 3, 5, 7]
for prime in primes:
    print prime

```

Vòng lặp for có thể chạy lần lượt qua các số bằng cách sử dụng hàm "range" hay "xrange". Sự khác nhau giữa range và xrange là range đưa ra danh sách các số theo thứ tự đó, còn xrange đưa ra một biến lặp, cách này hiệu quả hơn. Chú ý là hàm range bắt đầu từ 0. Ví dụ:

```
# Prints out the numbers 0,1,2,3,4
for x in range(5):
    print x

# Prints out 3,4,5
for x in range(3, 6):
    print x

# Prints out 3,5,7
for x in range(3, 8, 2):
    print x

```

***Vòng lặp while***

Vòng lặp while thực hiện lặp lại cho đến lúc điều kiện bị dừng lại. Ví dụ:

```
# Prints out 0,1,2,3,4

count = 0
while count &lt; 5:
    print count
    count += 1  # This is the same as count = count + 1

```

***Câu lệnh "break" và "continue"***

"break" được sử dụng để thoát ra một vòng lặp for hay while trong khi lệnh "continue" được sử dụng để bỏ qua đoạn lặp hiện tại và tiếp đến for hay while tiếp theo, ví dụ

```
# Prints out 0,1,2,3,4

count = 0
while True:
    print count
    count += 1
    if count &gt;= 5:
        break

# Prints out only odd numbers - 1,3,5,7,9
for x in range(10):
    # Check if x is even
    if x % 2 == 0:
        continue
    print x

```

***Chúng ta có thể sử dụng else cho vòng lặp không?***

Không giống như c hay c++, chúng ta có thể sử dụng else cho vòng lặp for. Khi điều kiện trong vòng lặp for hay while trả ra giá trị sai, thì đoạn code trong đoạn else sẽ được chạy. Nếu câu lệnh break chạy trong vòng lặp, thì đoạn lệnh sau else sẽ bị bỏ qua. Chú ý rằng đoạn lệnh else sẽ chạy nếu có câu lệnh continue.

Một số ví dụ:

```
# Prints out 0,1,2,3,4 and then it prints "count value reached 5"

count=0
while(count&lt;5):
    print count
    count +=1
else:
    print "count value reached %d" %(count)

# Prints out 1,2,3,4
for i in range(1, 10):
    if(i%5==0):
        break
    print i
else:
    print "this is not printed because for loop is terminated because of break but not due to fail in condition"

```

