# swap

# Định nghĩa

- "**swap**" là một phân vùng trên đĩa cứng được sử dụng để lưu trữ các trang dữ liệu không còn sử dụng trong bộ nhớ RAM của hệ thống. Khi bộ nhớ RAM đầy, các trang này sẽ được ghi vào swap để giải phóng bộ nhớ RAM và tiếp tục hoạt động. Swap được sử dụng như một phương tiện để tăng dung lượng bộ nhớ ảo cho hệ thống, điều này có thể cải thiện hiệu suất của hệ thống trong các trường hợp quá tải bộ nhớ.

# Khi nào cần phải sử dụng bộ nhớ Swap Memory

- Tối ưu hóa bộ nhớ: Hệ thống sẽ di chuyển các tài nguyên và dữ liệu hiện không được sử dụng trong bộ nhớ ram đến Swap, điều này giúp hệ thống phục vụ các mục đích khác tốt hơn.
- Tránh các trường hợp không lường trước: Trong một số trường hợp, Bạn không dự tính được bộ nhớ dành cho các chương trình mà bạn chuẩn bị thử nghiệm, hoặc một trương trình bất kỳ nào đó nổi điên lên, hoặc bất cứ điều gì đó bất thường Các bước tạo Swap File

+

Kiểm tra phân vùng Swap : ` swapon -s`

Kiểm tra dung lượng còn trống trên ổ cứng: df -TH

Tạo file Swap, tùy biến dung lượng 1G :fallocate -l 1G /swapfile

---

Tạo swapfile :

`dd if=/dev/zero of=/swapfile bs=1024 count=1048576`

bs: kích thướng Swap File

count: tốc độ

---

Phân quyền cho file vừa tạo

`chmod 600 /swapfile`

`chown root:root swapfile`

---

‘Sử dụng mkswap để thiết lập file trở thành file swap

`mkswap``/swapfile   

---

Khởi động Swap File bằng lệnh sau:

swapon /swapfile

Mở file `/etc/fstab` và thêm vào cuối dòng sau :/swapfile swap swap defaults 0 0

Giá trị của swappiness : Có giá trị từ 0 -> 100

- 0 : swap được sử dụng khi ram bị hết sử dụng
- 10 : swap được sử dụng khi ram còn 10%
- 60 : swap được sử dụng khi ram còn 60%
- 100: swap được sử dụng ưu tiên như ram

Kiểm tra mức độ dùng của hệ thống bằng lệnh:

cat /proc/sys/vm/swappiness

Mặc định của swap trong hệ thống là 30 nhưng sau phần cài đặt phía trên bây g chỉ còn 10

![Imgur](https://i.imgur.com/cAwfLbw.png)

# Bảng Tóm tắt các bước trong swap :

`swapon -s` → kiểm tra swap

`df -h` → Để kiểm tra dung lượng còn trống

`sudo dd if=/dev/zero of=/swapfile bs=1024 count=1024k` →tạo swap

`mkswap /swapfile` → Tạo phân vùng swap

`swapon /swapfie` → kích hoạt swap

`echo /swapfile none swap default 0 0 >> /etc/fstab` → thiết lập swap tự động mỗi khi reboot

`cat /proc/sys/vm/swappiness` → kiểm tra mức độ sử dụng file swap hệ thống

`sysctl vm.swappiness=10` → chỉnh thống số swappiness

---