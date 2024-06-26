# text_command

## 1.Hiển thị nội dung cat và tac

- `cat` thường được sử dụng để đọc và in các tệp cũng như để xem nội dung tệp một cách đơn giản.
- `tac` Thường được sử dụng để đọc các tệp , nội dung từ dưới lên

```
$ cat > myfile.txt
xin chao
day la test
welcome
Ctrl-D
```

![](../images/Untitled%203.png)

`tac`

![Untitled](../images/Untitled%204.png)

## 2.Thao tác với awk

Lệnh `awk` được sử dụng để trích xuất và sau đó in nội dung cụ thể của tệp và thường được sử dụng để tạo báo cáo. Nó là một tiện ích mạnh mẽ và ngôn ngữ lập trình được giải thích, được sử dụng để thao tác với các tệp dữ liệu, truy xuất và xử lý văn bản. Nó hoạt động tốt với các trường (chứa một phần dữ liệu, về cơ bản là một cột) và các bản ghi (một tập hợp các trường, về cơ bản là một dòng trong tệp)

```
[root@localhost ~]# awk '{ print $0 }' myfile.txt
xin chao
day la test
welcome
[root@localhost ~]# awk '{ print $1 }' myfile.txt
xin
day
welcome
[root@localhost ~]# awk '{ print $2 }' myfile.txt
chao
la
```

.Có thể thấy được sự khác biệt khi sử dụng lệnh tìm kiếm 0,1,2 ( tìm kiếm theo ký tự)

## 3.Thao tác với `sort,uniq`,`paste`,`join`

sort : sắp xếp theo thứ tự a b c … tăng dần 

```
cat myfile.txt
xin chao
day la test
welcome
sort myfile.txt
day la test
welcome
xin chao
```

`uniq` được sử dụng để loại bỏ các dòng trùng lặp trong tệp văn bản và rất hữu ích để đơn giản hóa việc hiển thị văn bản. Nó yêu cầu các mục trùng lặp được loại bỏ là liên tiếp.

```
cat myfile.txt
xin chao
day la test
welcome
welcome
sort myfile.txt | uniq
day la test
welcome
xin chao
```

Với tuỳ chọn -c,
Tham số -c cho phép chúng ta đếm số lần lặp lại của một dòng bất kì. Uniq sẽ in ra số lần lặp lại của dòng ở đầu dòng đó

`sort myfile.txt | uniq -c`

![Untitled](../images/Untitled%205.png)

Với tuỳ chọn -d,
-d chỉ in ra những dòng bị lặp lại bỏ qua những dòng không lặp lại 

![Untitled](../images/Untitled%206.png)

Với tuỳ chọn -u,
-u chỉ in ra những dòng không lặp lại , bỏ qua những dòng lặp lại

![Untitled](../images/Untitled%207.png)

`paste` lệnh được sử dụng để kết hợp các trường từ các tệp khác nhau

```
[root@localhost ~]# cat myfile.txt
xin chao
day la test
welcome
welcome
[root@localhost ~]# cat ages.txt
50
31
12
43
paste myfile.txt ages.txt
xin chao        50
day la test     31
welcome 12
welcome 43
```


![Untitled](../images/Untitled%208.png)

`join` lệnh kết hợp hai tệp trên một trường chung

![Untitled](
![Untitled](../images/Untitled%209.png)

## 4.Thao tác với `Grep`

Là lệnh tìm kiếm văn bản trong Linux

Có 2 văn bản sau 


![Untitled](../images/Untitled%2010.png)

vd: Tìm từ welcome trong văn bản myfile.txt

`grep "welcome" myfile.txt`

![Untitled](../images/Untitled%2011.png)

Tìm kiếm từ “su dung” trên nhiều file 

![Untitled](../images/Untitled%2012.png)

Tìm kiếm không phân biệt chữ hoa chữ thường chọn **-i**

![Untitled](../images/Untitled%2013.png)

Tìm kiếm ngược, sử dụng tùy chọn **-v**

![Untitled](../images/Untitled%2014.png)
. Hiển thị số dòng, số lượng, giới hạn số dòng đầu ra

• -n : Hiển thị số thứ tự của dòng và dòng chứa từ cần tìm

![Untitled](../images/Untitled%2015.png)

• -c : Hiển thị số dòng với thứ tự khớp cần tìm

![Untitled](../images/Untitled%2016.png)

.Tìm kiếm nhiều chuỗi 

c1:

`grep -e "keyword1" -e "keyword2" [tenfile1][tenfile2]`

c2:

`egrep "keyword1"|keyword2" [tenfile1][tenfile2]`

c3: 

`grep "keyword1"\|"keyword2" [tenfile1][tenfile2]`

![Untitled](../images/Untitled%2017.png)

![Untitled](../images/Untitled%2018.png)
![Untitled](../images/Untitled%2019.png)

**Tìm kiếm tên tệp**

`-l` : Để có được các tập tin phù hợp với tìm kiếm

![Untitled](../images/Untitled%2020.png)
`-L` : Tìm kiếm trong thư mục **file**,in ra các tên có trong chữ tìm kiếm

![Untitled](../images/Untitled%2021.png)

`-h` : in ra kết quả những dòng không kèm tên file

`-H` : in ra kết quả + tên file 

![Untitled](../images/Untitled%2022.png)

`-w` In ra chính xác những dòng có chứa keyword

![Untitled](../images/Untitled%2023.png)

`-r` Tìm tất cả các file ở tất cả các thư mục con

![Untitled](../images/Untitled%2024.png)
`-w -c`  Đếm số kq + hiển thị tên file chứa

![Untitled](../images/Untitled%2025.png)

`-l -r -w` Chỉ hiển thị tên file

![Untitled](../images/Untitled%2026.png)

**Đọc file loại bỏ comment, dòng trống**

Đây là file nhiều command

![Untitled](../images/Untitled%2027.png)

Đây là file sau khi loại bỏ command

`egrep -v "^#|^*#|^$” /etc/nginx/nginx.conf`

![Untitled](../images/Untitled%2028.png)