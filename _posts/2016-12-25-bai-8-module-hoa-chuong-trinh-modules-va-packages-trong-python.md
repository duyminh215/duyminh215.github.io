---
layout: post
title: "Bài 8: Module hóa chương trình: modules và packages trong Python"
category: Python
tags: [Python]
date: 2016-12-25
---

Module hóa chương trình trong ngôn ngữ Python chỉ đơn giản là các bạn sử dụng các file có .py, trong file này sẽ chứa một số hàm. Để sử dụng được file .py thì bạn sẽ sử dụng từ khóa "import".

Để sử dụng các thư viện đã viết sẵn, các bạn sử dụng từ khóa "import".

Đầu tiên, một module sẽ được load vào chương trình python, nó sẽ được khởi tạo lúc chương trình chạy chỉ một lần. Nếu có một module khác trong chương trình của bạn cũng import cùng một module đó, nó cũng sẽ được load 2 lần nhưng mà cũng chỉ được khởi tạo có 1 lần thôi. Do đó, biến cục bộ trong một module hoạt động như một "singleton" - tức là những biến chỉ được khởi tạo một lần.

Nếu chúng ta muốn import module "urllib", thư viện này dùng để đọc dữ liệu từ các URL, thì chúng ta sử dụng từ khóa import như sau:

```
# import the library
import urllib

# use it
urllib.urlopen("http://vnexpress.net/")

```

***Tìm hiểu một module***

Có 2 hàm rất quan trọng khi bạn muốn tìm hiểu một module là hàm "dir" và "help".
Chúng ta có thể xem được các hàm đã được tạo ra trong một module bằng hàm "dir" như sau:

```
import urllib
dir(urllib)
['ContentTooShortError', 'FancyURLopener', 'MAXFTPCACHE', 'URLopener', '__all__', '__builtins__', '__doc__', '__file__', '__name__', '__package__', '__version__', '_ftperrors', '_get_proxies', '_get_proxy_settings', '_have_ssl', '_hexdig', '_hextochr', '_hostprog', '_is_unicode', '_localhost', '_noheaders', '_nportprog', '_passwdprog', '_portprog', '_queryprog', '_safe_map', '_safe_quoters', '_tagprog', '_thishost', '_typeprog', '_urlopener', '_userprog', '_valueprog', 'addbase', 'addclosehook', 'addinfo', 'addinfourl', 'always_safe', 'basejoin', 'c', 'ftpcache', 'ftperrors', 'ftpwrapper', 'getproxies', 'getproxies_environment', 'getproxies_macosx_sysconf', 'i', 'localhost', 'main', 'noheaders', 'os', 'pathname2url', 'proxy_bypass', 'proxy_bypass_environment', 'proxy_bypass_macosx_sysconf', 'quote', 'quote_plus', 'reporthook', 'socket', 'splitattr', 'splithost', 'splitnport', 'splitpasswd', 'splitport', 'splitquery', 'splittag', 'splittype', 'splituser', 'splitvalue', 'ssl', 'string', 'sys', 'test', 'test1', 'thishost', 'time', 'toBytes', 'unquote', 'unquote_plus', 'unwrap', 'url2pathname', 'urlcleanup', 'urlencode', 'urlopen', 'urlretrieve']

```

Khi chúng ta tìm thấy được một hàm trong module và muốn sử dụng nó, chúng ta có thể đọc thêm về chức năng của hàm bằng hàm "help"

```
help(urllib.urlopen)

```

***Viết các modules mới***

Viết các modules Python mới rất đơn giản. Để tạo một module mới trong python, các bạn đơn giản là tạo ra một file .py mới với tên mà bạn muốn đặt, và sau đó sử dụng từ khóa import với tên file mà bạn vừa đặt để sử dụng nó.
Ví dụ bạn tạo một file my_utils.py, trong file main.py bạn muốn sử dụng các hàm trong my_utils.py thì chỉ cần đơn giản như sau

```
#day la file main.py
import my_utils //import file my_utils.py de su dung

```

***Viết các gói (packages)***

Các gói (packages) là các không gian name (namespace) chứa nhiều modules hoặc chính là các packages. Chúng đơn giản chính là các thư mục.
Mỗi gói (package) trong python là một thư mục phải có một file đặc biệt là __init__.py. File này có thể rỗng, và nó sẽ đánh dấu rằng thư mục này chứa một package, và nó có thể được gọi bằng hàm import giống như một module.
Nếu chúng ta tạo ra một thư mục có tên là "foo" và được coi là package có tên như vậy, chúng ta có thể tạo ra một module có tên "bar" trong package này. Chúng ta cũng không được quên tạo ra một file __init__.py trong thư mục "foo".
Để sử dụng module "bar", chúng ta sẽ làm bằng 2 cách sau:

```
import foo.bar

```

hoặc

```
from foo import bar

```

Ở cách đầu tiên, chúng ta sử dụng foo như là một tiền tố để chúng ta truy cập đến module "bar". Trong cách thứ hai, chúng ta không làm vậy mà sử dụng không gian tên để import một module.

