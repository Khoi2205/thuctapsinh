# NFS

# 1.Định nghĩa

- NFS là viết tắt của Network File System, là một giao thức mạng được sử dụng để chia sẻ tệp tin và thư mục giữa các máy tính trong một mạng. NFS cho phép người dùng truy cập tệp tin từ xa như thể chúng đang nằm trên máy tính của họ, mà không cần sao chép tệp tin đó xuống máy tính cá nhân. NFS được sử dụng phổ biến trong các môi trường mạng lớn như doanh nghiệp, tổ chức và các trung tâm dữ liệu.

# 

# 

# 2.Chức năng của NFS

- Chức năng của NFS là cho phép người dùng truy cập và chia sẻ tệp tin và thư mục giữa các máy tính trong một mạng. Khi NFS được triển khai, các máy tính trong mạng có thể truy cập vào các tệp tin và thư mục từ xa như chúng đang tồn tại trên máy chủ NFS, mà không cần sao chép chúng xuống máy tính cá nhân.

# 3. Một số ưu nhược điểm của NFS

| Ưu điểm                                                                                                                                                                                                                                                                              | Nhược điểm                                                                                                                                                                                                                                        |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Tăng tính sẵn sàng: NFS cho phép nhiều máy tính có thể truy cập và sử dụng các tệp tin và thư mục từ xa. Điều này giúp tăng tính sẵn sàng và tăng hiệu suất cho người dùng.                                                                                                          |
| Dễ dàng quản lý và bảo trì: Với NFS, việc quản lý và bảo trì các tệp tin và thư mục chỉ cần được thực hiện trên máy chủ NFS duy nhất, điều này giúp đơn giản hóa công việc quản lý và bảo trì hơn nếu so sánh với việc quản lý các tệp tin và thư mục trên nhiều máy tính khác nhau. | Bảo mật yếu: NFS không cung cấp tính năng bảo mật tốt, điều này khiến cho các tệp tin và thư mục có thể bị truy cập và sửa đổi trái phép. Để giải quyết vấn đề này, cần phải triển khai các biện pháp bảo mật như sử dụng giao thức SSL hoặc VPN. |
| Hiệu suất giảm sút: Khi số lượng người dùng truy cập vào NFS tăng cao, hiệu suất của hệ thống có thể giảm sút do tài nguyên mạng bị giới hạn.                                                                                                                                        |

# Bài lab cấu hình NFS trên centOS 7 :

## Trong hướng dẫn này, tôi sẽ giới thiệu các cài đặt các phần mềm cần thiết cho chức năng NFS trên centos7, Định cấu hình hai giá trị NFS trên máy Server và máy Client, Muont và Umuont các thiết bị từ xa.

## 

## Chọn máy chủ 192.168.202.136 làm server

## chọn máy chủ 192.168.202.137 làm máy client

## 

- Trên máy chủ Server

Cài đặt Gói **nfs-untils** cho phép bạn chia sẻ các thư mục của mình. Vì đây là thao tác đầu tiên bạn thực hiện **yum**, hãy update các gois của bạn trước khi cài đặt:

yum install nfs-utils

mkdir -p /var/nfsshare

mkdir /nfs123

chmod -R 755 /var/nfsshare

---

systemctl enable rpcbind

systemctl enable nfs-server

systemctl enable nfs-lock

systemctl enable nfs-idmap

systemctl start rpcbind

systemctl start nfs-server

systemctl start nfs-lock

systemctl start nfs-idmap

---

Ý nghĩa các câu lệnh :

systemctl enable rpcbind: Kích hoạt và cấu hình cho dịch vụ rpcbind được tự động khởi động khi hệ thống được khởi động.

systemctl enable nfs-server: Kích hoạt và cấu hình dịch vụ NFS server, cho phép chia sẻ file system trên mạng qua giao thức NFS.

systemctl enable nfs-lock: Kích hoạt và cấu hình dịch vụ NFS lock, giúp đồng bộ hóa việc truy cập file giữa các client.

systemctl enable nfs-idmap: Kích hoạt và cấu hình dịch vụ NFS idmap, chuyển đổi user ID và group ID giữa client và server trong quá trình truy cập tài nguyên NFS.

---

vi /etc/exports

---

![NFS%2020756979677943509ae052499dcbc58c/image4.png](NFS%2020756979677943509ae052499dcbc58c/image4.png)

Tắt tường lửa

firewall-cmd --permanent --zone=public --add-service=nfs

firewall-cmd --permanent --zone=public --add-service=mountd

firewall-cmd --permanent --zone=public --add-service=rpc-bind

firewall-cmd --reload

---

Ý nghĩa các câu lệnh :

firewall-cmd --permanent --zone=public --add-service=nfs được sử dụng để mở cổng cho dịch vụ NFS (Network File System) trong khu vực public của tường lửa và lưu trữ cấu hình này vào tệp cấu hình của tường lửa.

firewall-cmd --permanent --zone=public --add-service=mountd được sử dụng để mở cổng cho dịch vụ mountd (dịch vụ đăng nhập NFS) trong khu vực public của tường lửa và lưu trữ cấu hình này vào tệp cấu hình của tường lửa.

firewall-cmd --permanent --zone=public --add-service=rpc-bind được sử dụng để mở cổng cho dịch vụ rpc-bind (Remote Procedure Call Bind) trong khu vực public của tường lửa và lưu trữ cấu hình này vào tệp cấu hình của tường lửa.

firewall-cmd --reload được sử dụng để tải lại cấu hình của tường lửa từ các tệp cấu hình được lưu trữ và áp dụng các thay đổi mới

---

- Cấu hình nfs trên client

yum install nfs-utils

mkdir -p /mmt/nfs/home

mkdir -p /mmt/nfs/nfs123

---

mount -t nfs 192.168.202.136:/home /mmt/nfs/home/

mount -t nfs 192.168.202.136:nfs123 /mmt/nfs/nfs123

---

show cấu hình vừa mount

![NFS%2020756979677943509ae052499dcbc58c/image3.png](NFS%2020756979677943509ae052499dcbc58c/image3.png)

Đến đây xem như đã hoàn thành g test thử xem

Vào thư mục nfs123 tạo thư mục và viết vào thư mục

![NFS%2020756979677943509ae052499dcbc58c/image1.png](NFS%2020756979677943509ae052499dcbc58c/image1.png)

![NFS%2020756979677943509ae052499dcbc58c/image6.png](NFS%2020756979677943509ae052499dcbc58c/image6.png)

G mình chuyển sang máy client để xem :

![NFS%2020756979677943509ae052499dcbc58c/image5.png](NFS%2020756979677943509ae052499dcbc58c/image5.png)

- Bài toán đặt ra

### 

- Khi reboot máy client thì sẽ bị mất, => sử dụng file fstab để lưu

### 

### Vào file có tên mtab

![NFS%2020756979677943509ae052499dcbc58c/image7.png](NFS%2020756979677943509ae052499dcbc58c/image7.png)

---

copy file này vào /etc/fstab

![NFS%2020756979677943509ae052499dcbc58c/image2.png](NFS%2020756979677943509ae052499dcbc58c/image2.png)

systemctl restart nfs-service

---