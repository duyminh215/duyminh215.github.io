---
layout: post
title: "Xây dựng một bộ máy tìm kiếm(search engine) đơn giản bằng MySQL"
category: Mysql
tags: [Mysql]
date: 2017-01-01
---

Hôm nay mình sẽ chia sẻ cách tạo ra một bộ máy tìm kiếm (search engine) đơn giản bằng MySQL.

Khi phát triển ứng dụng Clingme, mình được yêu cầu xây dựng một bộ máy tìm kiếm. Clingme là một mobile

application để tìm kiếm các địa điểm xung quanh bạn. Lúc đó, công ty sử dụng MySQL nên mình đã nghiên cứu để

xây dựng bộ máy tìm kiếm (search engine) bằng chính MySQL mà không cần dùng công cụ bên ngoài.

Link tham khảo các bạn có thể vào <a title="Fulltext Search Index" href="http://dev.mysql.com/doc/refman/5.6/en/fulltext-search.html" target="_blank">tài liệu fulltext của MySQL</a>.

Yêu cầu lúc đó là  tìm kiếm địa điểm bằng tên địa điểm, địa chỉ hoặc sản phẩm, dịch vụ mà địa điểm cung cấp.

Tức là chúng ta có bảng place(place_id, name, address, product_service, tag). MySQL có cung cấp query sử dụng

chính fulltext search index. Để có thể sử dụng query này, bạn phải đánh fulltext search index cho các trường mà bạn muốn query.

```

CREATE FULLTEXT INDEX `idx_fulltext` ON `place_db`.`place` (`name`, `address`, `product_service`, `tag`);

```

Yêu cầu là search địa điểm theo tên, địa chỉ, sản phẩm dịch vụ mà địa điểm cung cấp. Do vậy chúng ta sẽ đánh full

text search index cho 4 trường là (name, address, product_service, tag), chú ý ở đây tag chứa các từ chúng ta sẽ thêm

vào để search.

MySQL cung cấp hàm search full text theo cú pháp sau:

```

SELECT * FROM place WHERE MATCH (name,address, product_service, tag) AGAINST ('nhà hàng abc');

```


Ở ví dụ trên chúng ta muốn search “nhà hàng abc”. Tuy nhiên với câu lệnh như trên, MySQL sẽ trả ra kết quả là các

records hoặc chứa chữ “nhà”, hoặc chữ “hàng”, hoặc chữ “abc”. Như vậy kết quả sẽ không được chính xác lắm.

Do vậy chúng ta cần tối ưu kết quả. Các cách tối ưu MySQL search engine bao gồm:

***a. Chọn bộ mã thích hợp để lưu trữ dữ liệu:***

Có một lưu ý rằng, MySQL fulltext index sẽ đối xử với các ký tự khác nhau tùy theo bộ mã mà chúng ta sẽ sử dụng

để lưu trữ dữ liệu. Thông thường, để lưu trữ tiếng VIệt trong MySQL chúng ta dùng bộ mã “utf8_general_ci”. Nếu

dùng bộ mã này, fulltext search sẽ không phân biệt chữ có dấu hay không dấu của tiếng Việt. VD chúng ta muốn

search quán cơm bằng tiếng Việt không dấu:

```

SELECT * FROM place WHERE MATCH (name,address, product_service, tag) AGAINST ('cơm');

```

thì ở đây kết quả có thể ra các records chứa từ “cơm”, “cốm”, “còm”, …

Thoạt nhìn, chúng ta có cảm giác sẽ ra được nhiều kết quả. Tuy nhiên, nếu sử dụng bộ mã này, search engine sẽ bị

nhiễu rất nhiều, và kết quả không chính xác lắm.  Theo kinh nghiệm trong quá trình phát triển Clingme thì

chúng ta nên sử dụng bộ mã “utf8_bin”. Với bộ mã này, fulltext index sẽ phân biệt chữ có dấu và không dấu. Nghĩa

là lúc đó search “cơm” sẽ ra các records chứa từ “cơm”, “cốm” sẽ ra các bảng có từ “cốm”. Còn nếu search “com” thì

chỉ chứa các bảng có từ “com”. Nghĩa là bây giờ bạn muốn người ta search “com” ra cơm thì chỉ cần trong các địa

điểm liên quan đến quán cơm chúng ta thêm từ “com” vào column tag. Mục đích của column “tag” để chúng ta chủ

động thêm vào các từ mà chúng ta muốn người dùng search từ đó sẽ ra. Như vậy về mặt dữ liệu, chúng ta hoàn toàn

chủ động điều khiển search cái gì sẽ ra cái nào, không bị nhiễu.  Tuy nhiên, lúc lưu trữ chúng ta phải đặt các luật

trước rồi mới lưu vào.

***b. Chọn chế độ(mode) lúc search:***

Mặc định lúc sử dụng fulltext index mà không nêu rõ chế độ (mode) nào thì MySQL sẽ cho ra kết quả  các records

chứa từng từ trong input mà chúng ta cho vào. Ví dụ, bạn muốn search “quán ăn” với chế độ (mode) mặc định:

```

SELECT * FROM place WHERE MATCH (name,address, product_service, tag) AGAINST ('quán cơm');

```

thì kết quả sẽ ra kết quả các records hoặc chứa từ “quán” hoặc từ “cơm”. Như vậy, “quán” game, “quán” nước, …

cũng sẽ lẫn vào trong kết quả trả ra. Để tránh điều này MySQL cung cấp các mode “Natural Language” và

“Boolean”. Chúng ta sẽ sử dụng “Boolean” mode để tránh trường hợp trên. Trong “boolean mode”, MySQL có cung

cấp nhiều cách để chúng ta search, vd muốn search ra các records chứa cả hai ký tự “quán” và “cơm” thì câu query

có dạng:

```

SELECT * FROM place WHERE MATCH (name,address, product_service, tag) AGAINST ('+quán+cơm' IN BOOLEAN MODE);

```

Ở câu trên, chúng ta chú ý dấu cộng  “+” trước mỗi từ, dấu “+” trong chế độ boolean có nghĩa là các records phải

chứa cả hai từ đó thì mới ra kết quả. Tuy nhiên, với cách dùng này thì quán có từ “quán có bán bún, cơm rang” thì

vẫn ra. Nghĩa là chỉ cần records chứa 2 từ đó nhưng mà không cần cạnh nhau thì vẫn ra.

Để search ra kết quả chính xác từ “quán cơm” cạnh nhau thì ta dùng query:

```

SELECT * FROM place WHERE MATCH (name,address, product_service, tag) AGAINST ('"quán cơm"' IN BOOLEAN MODE);

```

Câu trên chú ý là từ quán cơm đã được cho vào dấu “”.

Trong quá trình phát triển sản phẩm, vì yêu cầu search các place theo cả địa chỉ, tên, sản phẩm dịch vụ nên mình đã

sử dụng boolean mode theo câu query đầu, nghĩa là chèn dấu cộng “+”. Vd muốn search quán cơm ở đường

Trường Chinh thì câu query sẽ như sau:

```

SELECT * FROM place WHERE MATCH (name,address, product_service, tag)AGAINST ('+quán+cơm+Trường+Chinh' IN BOOLEAN MODE);

```

với câu query trên chúng ta sẽ ra các records bắt buộc có từ “quán”, “cơm”, “trường”, “chinh”. Mặc dù không hoàn

toàn chính xác nhưng MySQL fulltext boolean mode đã cho ra kết quả tương đối chấp nhận được.

***c. Set tham số để MySQL search chính xác hơn:***

Lúc tạo DB, chúng ta có hai chế độ lưu trữ của DB là “MyISAM” và “InnoDB”. Vì yêu cầu dữ liệu của mình, nên

mình dùng “InnoDB”. Với hai cách trên, MySQL cũng sẽ có nhiều tham số khác nhau để sử dụng fulltext hiệu quả

hơn. Mặc định, MySQL chỉ cho phép search các từ có hai ký tự trở lên, vd từ “dù” sẽ ra, nhưng nếu mà muốn search

từ “ô” thì sẽ không ra. Do vậy, chúng ta cần config MySQL để search được các từ bé hơn 2 ký tự. Để lấy được tham

số về từ có bao nhiêu ký tự đang mặc định MySQL sử dụng, chúng ta chạy query sau:

```

SHOW VARIABLES LIKE "ft_min_word_%";

SHOW VARIABLES LIKE "innodb_ft_min_token_size%";

```

với chú ý, “ft_min_word” là dành cho “MyISAM”, còn “innodb_ft_min_token_size” là dành cho InnoDB.

Bạn co thể set lại giá trị này, vd là 1 nếu bạn muốn MySQL có thể search các từ có 1 ký tự, việc set giá trị bao 
nhiêu dựa vào dữ liệu của bạn. Nếu dữ liệu của bạn không có từ nhỏ hơn 1 ký tự thì bạn có thể set giá trị đó. Để 
set giá trị này, chúng ta sẽ tạo một file “my.cnf” hoặc search file này nếu lúc cài MySQL đã có. Nội dung của file 
“my.cnf” như

sau:

```


[mysqld]

innodb_ft_min_token_size=1

ft_min_word_len=1


```

Với giá trị số ký tự mà MySQL fulltext mà bạn muốn MySQL search.

Sau khi tạo file xong, nếu ở trên linux, bạn lưu file vào đường dẫn “/etc/my.cnf”  hoặc ““/etc/mysql/my.cnf”. Việc lưu

trữ file config này bạn có thể đọc tài liệu MySQL để tìm hiểu thêm hoặc chạy lệnh sau để biết thông tin:

```
mysqld –verbose –help
```

Sau khi tạo file và lưu file vào đường dẫn đó, chúng ta restart lại MySQL, trên linux, command sẽ là:

```
/etc/init.d/mysql restart
```

Sau khi MySQL đã khởi động xong, để kiểm tra lại giá trị “min word length”, chúng ta sẽ chạy câu lệnh sau:

```

SHOW VARIABLES LIKE "ft_min_word_%";

SHOW VARIABLES LIKE "innodb_ft_min_token_size%";

```

***d. Cập nhật lại stop word của MySQL:***

Mặc định, MySQL sẽ có một bảng chứa các stop words, nếu trong records chứa các stop words này, lúc bạn search

các từ đó, bạn sẽ không lấy được kết quả. Tùy thuộc bạn sử dụng kiểu “MyISAM” hay”InnoDB”, MySQL sẽ có các

stop words khác nhau. Vì mình sử dụng InnoDB nên mình sẽ nói về các stop words với InnoDB. Để lấy danh sách

stop words của InnoDB bạn sử dụng câu query sau:

```
SELECT * FROM INFORMATION_SCHEMA.INNODB_FT_DEFAULT_STOPWORD;
```

Trong bảng sẽ chứa các giá trị các stop word, trong đó chú ý có một số từ mà tiếng Việt có thể gặp như “com”, “be”,

“la”, “the”. Với các từ đó, lúc user search “com” (có thể họ search cơm không dấu) thì MySQL không trả ra kết quả.

Do vậy, chúng ta cần cập nhật lại bảng stop word này. Để cập nhật stop word, chúng ta cần tạo bảng có cấu trúc

như stop word của MySQL.  Bảng stop word của MySQL có cấu trúc `INNODB_FT_DEFAULT_STOPWORD`(`value`). Do vậy, chúng ta cũng sẽ tạo một bảng có cấu trúc tương tự:

```

CREATE TABLE `admin_stopword` (
`value` VARCHAR(18) NOT NULL DEFAULT ” COLLATE ‘latin2_general_ci’
)
COLLATE=’latin2_general_ci’
ENGINE=InnoDB;

```

Chú ý, ở đây, qua thực nghiệm thì sử dụng collate ‘latin2_general_ci’ thì hiệu quả, còn “utf8_general_ci” không hiệu

quả. Trong bảng ‘admin_stopword’ chúng ta có thể thêm tùy ý các stop word của chúng ta hoặc bỏ trống.

Sau khi tạo xong bảng stop word, chúng ta set lại bảng stop word bằng câu lệnh:

set global innodb_ft_server_stopword_table = ‘place_db/admin_stopword';

Sau khi set lại tham số stopword, chúng ta cần index lại fulltext index:

```

DROP INDEX `idx_fulltext` ON `place_db`.`place` ;

CREATE FULLTEXT INDEX `idx_fulltext` ON `place_db`.`place` (`name`, `address`, `product_service`, `tag`);

```

Sau đó, chúng ta sẽ thử search ‘com’ để kiểm chứng lại.

***Tổng kết***

Như vậy, với các cách tối ưu như trên, chúng ta có thể sử dụng MySQL fulltext index như một công cụ để xây dựng bộ máy tìm kiếm mà không cần sử dụng các thư viện bên ngoài. Với MySQL fulltext search, chúng ta sẽ tìm kiếm nhanh hơn so với sử LIKE.

