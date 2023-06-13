# NTP

# NTP là gì :

- Network Time Protocol – Là giao thức đồng bộ thời gian mạng) là một giao thức để đồng bộ hóa đồng hồ của máy tính thông qua mạng dữ liệu chuyển mạch gói với độ trễ có biến đổi .
- Giao thức này được thiết kế ra để tránh ảnh hưởng của độ trễ biến đổi bằng cách là sử dụng bộ đệm jitter. NTP cũng được gọi là của phần mềm được triển khai trong một dự án Dịch vụ NTP Công cộng (NTP Public Services Project)

# 

# Cách thức hoạt động của NTP :

- NTP client gửi đi một gói tin, trong đó có chứa một thẻ thời gian tới cho NTP server.
- NTP server nhận được gói tin, và gửi trả lại NTP client một gói tin khác, có thẻ thời gian là thời điểm nó đã gửi gói tin đó đi.
- NTP client nhận được gói tin đó, rồi tính toán độ trễ, dựa vào thẻ thời gian mà nó nhận được cùng với độ trễ của đường truyền, NTP client sẽ tự động set lại thời gian của nó.

# 

# Cách cấu hình ntp trên server và client :

# yêu cầu cài đặt ntp server trên centos7

# Thực hiện show cấu hình cài đặt

# Đồng bộ hóa với client

Cách cấu hình trên centos7

![NTP%20b63b44a13da048bfa3c480960b1560ef/image2.png](./NTP%20b63b44a13da048bfa3c480960b1560ef/image2.png)

Sau khi cài đặt , truy cập chọn khu vực , chọn quốc gia để cài đặt

[https://www.ntppool.org/zone/vn](https://www.ntppool.org/zone/vn)

![NTP%20b63b44a13da048bfa3c480960b1560ef/image8.png](NTP%20b63b44a13da048bfa3c480960b1560ef/image8.png)

Sau đó , mở tệp cấu hình chính của ntp để chỉnh sửa , thay thế máy chủ công cộng mặc định bằng danh sách cung cấp quốc gia , khu vực

vi /etc/ntp.conf

---

![NTP%20b63b44a13da048bfa3c480960b1560ef/image9.png](NTP%20b63b44a13da048bfa3c480960b1560ef/image9.png)

Cần cho phép các máy khách từ mạng của mình đồng bộ hóa thời gian với máy chủ này. Để thực hiện điều này, hãy thêm dòng sau vào tệp cấu hình NTP, nơi kiểm soát câu lệnh **hạn chế** , mạng nào được phép truy vấn và thời gian đồng bộ hóa – thay thế IP mạng tương ứng.

![NTP%20b63b44a13da048bfa3c480960b1560ef/image3.png](NTP%20b63b44a13da048bfa3c480960b1560ef/image3.png)

Nếu cần lưu cấu hình, để khắc phục sự cố thêm một tệp nhật ký sẽ ghi lại tất cả các sự cố của máy chủ

![NTP%20b63b44a13da048bfa3c480960b1560ef/image3.png](NTP%20b63b44a13da048bfa3c480960b1560ef/image3.png)

Đây là hoàn thiện sau khi cài đặt xong

![NTP%20b63b44a13da048bfa3c480960b1560ef/image6.png](NTP%20b63b44a13da048bfa3c480960b1560ef/image6.png)

![NTP%20b63b44a13da048bfa3c480960b1560ef/image5.png](NTP%20b63b44a13da048bfa3c480960b1560ef/image5.png)

B2: Thiết lập tường lửa (để chống lại tác động của độ trễ

# firewall-cmd --add-service=ntp --permanent

# firewall-cmd --reload

---

Sau khi kích hoạt tường lửa xong, Khởi động máy chủ NTP và đảm bảo rằng nó đang hoạt động

systemctl start ntpd

systemctl enable ntpd

systemctl status ntpd

---

![NTP%20b63b44a13da048bfa3c480960b1560ef/image4.png](NTP%20b63b44a13da048bfa3c480960b1560ef/image4.png)

Sau đó chạy các lệnh sau để xác minh trạng thái đồng bộ hóa NTP ngang hàng và thời gian hệ thống

ntpq -p

date -R

---

![NTP%20b63b44a13da048bfa3c480960b1560ef/image10.png](NTP%20b63b44a13da048bfa3c480960b1560ef/image10.png)

Thực hiện cấu hình trên client :

![NTP%20b63b44a13da048bfa3c480960b1560ef/image1.png](NTP%20b63b44a13da048bfa3c480960b1560ef/image1.png)