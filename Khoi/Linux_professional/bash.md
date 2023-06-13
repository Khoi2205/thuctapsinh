## Làm việc basic vs Bash
### Hello Word
1. Interactive Shell
- Interactive shell là một chương trình dòng lệnh (command-line interface) cho phép bạn tương tác với hệ thống máy tính của mình thông qua việc nhập các lệnh và nhận kết quả trực tiếp từ hệ thống. Với interactive shell, bạn có thể thực hiện nhiều tác vụ khác nhau trên hệ thống của bạn, từ việc di chuyển giữa các thư mục đến thực thi các ứng dụng và chương trình. Interactive shell thường được sử dụng trong các hệ thống Unix và Linux, và là công cụ rất hữu ích cho các lập trình viên và nhà quản trị hệ thống.
![Imgur](https://i.imgur.com/gNjNe34.png)
- Lệnh `echo` : Ghi các đối số mà nó nhận được vào đầu ra tiêu chuẩn 
***1.1 Shell không tương tác**
Shell Bash cũng có thể được chạy không tương tác từ một tập lệnh, làm cho shell không yêu cầu tương tác của con người.Hành vi tương tác và hành vi theo kịch bản phải giống hệt nhau - một cân nhắc thiết kế quan trọng của Unix V7.Vỏ Bourne và Bash chuyển tiếp. Do đó, bất cứ điều gì có thể được thực hiện tại dòng lệnh đều có thể được đưa vào tập lệnh tập tin để tái sử dụng
- Tạo 1 file scrip Hello word 
- Thêm quyền thực thi đối với file: chmod +x hello.sh
- Thêm code vào file hello.sh
Dòng đầu tiên chuỗi ký tự #! được gọi là shebang1. Shebang hướng dẫn hệ điều hành chạy
Dòng 2 sử dụng echo để ghi Hello World vào đầu ra tiêu chuẩn
```
#!/bin/bash
echo "Hello World"
```
Thực thi tập lệnh hello.sh từ dòng lệnh bằng cách sử dụng một trong những cách sau
Cách mà được sử dụng phổ biến nhất `./hello.sh``
`/bin/bash hello.sh`
`bash hello.sh`
`sh hello.sh`

- Tất cả đều được in ra màn hình với kq cuối cùng là `Hello Word`
![Imgur](https://i.imgur.com/BODVbTZ.png)
***1.2 Helloword sử dụng biển**

- Tạo 1 file có tên là hello.sh với nội dung, và cấp quyền thực thi cho file đấy
```
#!/usr/bin/env bash
# Note that spaces cannot be used around the `=` assignment operator
whom_variable="World"
# Use printf to safely output the data
printf "Hello, %s\n" "$whom_variable"
```
Sau khi chạy sẽ in ra dòng Hello,Word

- Sửa nội dung thành như sau để xuất ra một chuỗi định dạng 
```
#!/usr/bin/env bash
printf "Hello, %s\n" "$1"
```
![Imgur](https://i.imgur.com/Dr6uSO3.png)
- Câu lệnh đầu tiên không có đối số
- Câu lệnh thứ 2 đối số bằng một chuỗi
- Cấu lệnh thứ 3  đối với chuỗi có phân cách nhau bằng dấu cách, đối số $1 chỉ được ứng với 1 chuỗi đầu tiền sau câu lệnh.
- Để xử lý câu lệnh thứ 3 không hiện thị được chuỗi thì ta cần thêm dấu ngoặc kép cho câu lệnh
***1.3 Hello World with user Input**
```
#!/usr/bin/env bash

echo "who are you"
read name
echo "Hello, $name."
```
- Lệnh `read` ở đây đọc dữ liệu từ đầu vào tiêu chuẩn vào tên biến. Sau đó sử dụng $name và in ra bằng echo
![Imgur](https://i.imgur.com/a0DD4NJ.png)

- Nếu bạn muốn nối một cái gì đó vào giá trị biến trong khi in nó, hãy sử dụng dấu ngoặc nhọn quanh biến tên như được hiển thị trong ví dụ sau
```
#!/usr/bin/env bash
echo "what are you doing"
read action
echo "You are ${action}ing and .... 
```
output:
![Imgur](https://i.imgur.com/qZwd5Yl.png)
***1.4 Tầm quan trong trích dẫn trong chuỗi**
- Có hai kiểu trích dẫn 
- Yếu : Sử dụng trích dẫn `"`
- Mạnh : Sử dụng trích dẫn `'`
VD: 
- Trích dẫn yếu 
```
#!/usr/bin/env bash
word="Word"
echo "Hello $word"
```
- Trích dẫn mạnh
```
#!/usr/bin/env bash
word="Word"
echo 'Hello $word'
```
![Imgur](https://i.imgur.com/gSVUwYW.png)
***1.5 Xem thông tin cho Bash tích hợp**
help [command]: Dùng để xe thông tin, cách sử dụng và các tùy chọn có trong câu lệnh
***1.6  Hello World chế độ "Debug"**
![Imgur](https://i.imgur.com/a1s9Vlb.png)
Đối số -x cho phép bạn xem qua từng dòng lệnh trong tệp
vd 2 : 
```
#!/usr/bin/env bash
echo "Hello word"
adding_string_to_number="s"
v=$(expr 9 + $adding_string_to_number)
```
output
Thông số đưa vào sẽ không đúng định dạng

![Imgur](https://i.imgur.com/KhvCM4H.png)
```
#!/usr/bin/env bash
echo "Hello word"
adding_string_to_number="9"
v=$(expr 9 + $adding_string_to_number)
```
output
Thông số đưa vào sẽ đúng định dạng
![Imgur](https://i.imgur.com/DUayfQi.png)



### Phần 2 Script shebang
**2.1 ENV Shebang**
- Để thực thi tệp tập lệnh với tệp thực thi bash được tìm thấy trong biến môi trường PATH bằng cách sử dụng tệp thực thi env, dòng đầu tiên của tệp script phải chỉ ra đường dẫn tuyệt đối đến tệp thực thi env với đối số bash:
`#!/usr/bin/env bash`
- Đường dẫn env trong shebang được giải quyết và chỉ được sử dụng nếu tập lệnh được khởi chạy trực tiếp:
`script.sh`
**2.1 Direct shebang**
- Để thự thi một tập lệnh scrip với tệp thực hi bash, dòng đầu tiên chỉ ra tuyệt đối đến tập thực thi bash:
`#!/bin/bash`
- Đường dẫn  bash trong path được giải quyết và sử dụng lệnh chạy trực tiếp
`./scrip`
**2.3: Other shebangs**
Có 2 loại chương trình mà kernel biết. Một chương trình nhị phân được xác định bởi tiêu đề ELF(ExtenableLoadableFormat - Định dạng có thể tái mở rộng), thường được tạo bởi trình biên dịch. Thứ hai là kịch bản của bất kỳ loại nào.

Nếu một tệp bắt đầu với dòng đầu tiên bằng chuỗi #! thì tiếp theo phải là tên đường dẫn của trình thông dịch.

Nếu kernel đọc được dòng này, nó sẽ gọi trình thông dịch được đặt tên theo tên đường dẫn này và đưa các từ trong dòng làm đối số thông dịch.
![Imgur](https://i.imgur.com/sft2eGP.png)
- Sẽ không thực thi được câu lệnh vì trong /usr/bin/evn không có trình thông dịch something, something không thể xử lý được lệnh



### Phần 3 Navigating directories
**3.1 Điều hướng thư mục**
- Thay đổi đến thư sử dụng cuối cùng 
`cd -`
**3.2 Change to the home directory**
`echo $HOME`
![Imgur](https://i.imgur.com/tCtfaYu.png)
**3.3 Thay đổi thư mục của script**
- Có 2 tool
1.System tool-Các công cụ hệ thống hoạt động từ thư mục làm việc hiện tại
2.Project tool-Các công cụ dự án sửa đổi các tệp liên quan đến vị trí của chúng trong hệ thống tệp

**3.4 Listing Files**
- Sử dụng bash shell's File name expansion(mở rộng tên tệp) và brace expansion(mở rộng dấu ngoặc nhọn) để lấy các tên tệp:
` printf "%s\n" * == ls`
anaconda-ks.cfg
certbot-auto
hello.sh
liệt kê file có đuôi txt 
`printf "%s\n" *.txt`
Liệt kê các file có đuôi txt,md,conf, nếu không có file thì dấu * sẽ được hiển thị ở đầu
`printf "%s\n" *.{txt,md,conf}`
![Imgur](https://i.imgur.com/IRHDnew.png)
### Phần 4 Jobs and Processes
**4.1 Xử lý công việc**
- Createing jobs
Để tạo job, chỉ cần thêm dấu & sau lệnh. & không phải là một tham số cho chương trình. Nó cho shell. & là chạy chương trình ở chế độ nền trong shell.
```
 sleep 10 &
[1] 74773
```
Vd : Thực hiện sleep trong vòng 10s .
Bạn có thể thực hiện một lệnh tiếp theo mà không cần đợi job thực hiện xong bằng tổ hợp phím Ctr + Z. Sử dụng Crl+z sẽ ngưng lại tiến trình
Background(bg) and foreground(fg)(đặt vấn đề lên trước) a process
**Killing running jobs**
![Imgur](https://i.imgur.com/8gjtRnz.png)

-  Kiểm tra Process đang chạy trên cổng cụ thể
` lsof -i :22`
`lsof -i :80`
![Alt text](image-2.png)