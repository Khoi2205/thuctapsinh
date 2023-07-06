## Giới thiệu về `sed`
### 1.Định nghĩa
Là một trình biên soạn thường được thực hiện những thao tác chỉnh sửa đối với dữ liệu đến từ một đầu vào hoặc một chuẩn file text.`sed`
### 2. Cách sử dụng cơ bản 

`sed [option] commands [file-to-edit]`

**2.1 Sử dụng `sed` để xem nội dung file**

`sed '' [file_name]`

VD: tạo file `test.sh` có nội dung 
```
xin chao viet nam
xin chao han quốc 
xin chao trung quoc
```

sửa dụng câu lệnh `sed '' test.sh` sẽ hiển thị kq sau

[Imgur](https://i.imgur.com/wRXqiw9.png)

- Cặp nháy đơn sẽ chứa các câu lệnh dùng để chỉnh sửa đoạn văn bản mà truyền vào `sed` vì không truyền vào gì nên sẽ in ra màn hình mỗi dòng nó nhận được từ đầu vào 


**2.2 Sử dụng `sed 'p' `  đã in ra mỗi dòng 2 lần**

`sed 'p' tesh.sh`

[Imgur](https://i.imgur.com/rjgWFLs.png)


Để có thể linh hoạt hơn trong việc in kết quả ra màn hình, ví dụ như chỉ in ra dòng đầu tiên, in ra các dòng từ 1 - 5, hoặc in ra các dòng có thứ tự lẻ... thì chúng ta cần sử dụng thêm các tham số kết hợp với lệnh p.

Chỉ in ra dòng đầu tiên:

`sed -n '1p' test.sh`

In ra các dòng từ 1 - 4:
`sed -n '1,4p' test.sh `

In ra các dòng với số thứ tự lẻ:

`sed -n '1~2p' test.sh` 


[Imgur](https://i.imgur.com/TZ7XDGc.png)


**2.3 Sử dụng `sed '' `  để thay thế**

`'s/old_word/new_word'`

Ký tự `s` là thay thế văn bản . Ba dấu `/` dùng để ngăn cách những trường văn bản khác nhau 

VD:

`sed 's/xin chao/BAN DA CHUYEN ĐỔI/' test.sh`


[Imgur](https://i.imgur.com/4IQcYBZ.png)

- Với câu lệnh trên sẽ hiển thị kí tự mình thay đổi nhưng sẽ không đổi trong file test.sh 


[](https://i.imgur.com/7p7fWsa.png)


- Sử dụng tham số `i` sẽ thay đổi trong cả file gốc 

vd 
`sed -i 's/trung quoc/brazil/g' test.sh `

Chú thích:
"'s/trung quoc/brazil/g'" là một biểu thức chính quy (regular expression) được sử dụng để chỉ định quy tắc thay thế. Trong trường hợp này, nó cho phép tìm kiếm chuỗi "trung quoc" và thay thế nó bằng chuỗi "brazil".
"g" ở cuối biểu thức chính quy là một tuỳ chọn để thực hiện thay thế toàn bộ các xuất hiện của "trung quoc" trong văn bản. Nếu không sử dụng tuỳ chọn này, chỉ có xuất hiện đầu tiên của "trung quoc" trong mỗi dòng sẽ được thay thế.


[](https://i.imgur.com/Oo1PX0X.png)

