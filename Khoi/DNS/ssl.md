# Cài đặt SSL

## 1. Định nghĩa

- SSL/TLS là viết tắt của Secure Socket Layer/Transport Layer Security, là một giao thức bảo mật được sử dụng để bảo vệ thông tin truyền tải qua mạng. SSL/TLS đảm bảo tính toàn vẹn, độ tin cậy và bảo mật cho các thông tin nhạy cảm như tài khoản ngân hàng, thông tin cá nhân hay mật khẩu.
- Chức năng của SSL/TLS là mã hóa thông tin giữa hai bên truyền tải thông qua mạng, từ đó ngăn chặn các kẻ xâm nhập không trung thực đánh cắp hoặc thay đổi thông tin trên đường truyền.
- Ưu điểm của SSL/TLS là đảm bảo tính bảo mật cao cho thông tin truyền tải qua mạng, giúp người dùng yên tâm khi giao dịch trực tuyến. Ngoài ra, SSL/TLS có thể được sử dụng trên nhiều loại giao thức như HTTP, SMTP, FTP...và được hỗ trợ rộng rãi trên các trình duyệt web và máy chủ.

## 2. Các bước cài đặt SSL

Let's Encrypt là Tổ chức phát hành chứng chỉ (CA) mới cung cấp cách lấy và cài đặt chứng chỉ TLS/SSL miễn phí, từ đó kích hoạt HTTPS được mã hóa trên các máy chủ web. Nó hợp lý hóa quy trình bằng cách cung cấp ứng dụng khách phần mềm, Certbot, cố gắng tự động hóa hầu hết (nếu không phải tất cả) các bước cần thiết. Hiện tại, toàn bộ quá trình lấy và cài đặt chứng chỉ hoàn toàn tự động trên cả máy chủ web Apache và Nginx.

### Yêu cầu cần cài đặt nginx , hoặc apache (yêu cầu có domain)

### B1 : Cài  đặt Certbot Let encrypt client

`yum install epel-release`

`yum install certbot-nginx`

### B2 : Cài đặt nginx

`yum install nginx`

- Sau khi cài đặt thì khởi động nginx bằng câu lệnh

`systemctl start nginx`

- Chỉnh sửa file cấu hình nginx thêm domain vào chỗ tên server_name

`vi /etc/nginx/nginx.conf`

![Untitled](./C%C3%A0i%20%C4%91%E1%BA%B7t%20SSL%20251c6c2d35fd4234a0ebf8d8f51d9e03/Untitled.png)

- Kiểm tra xem nginx có hoạt động bình thường không

`nginx -t`

![Untitled](./C%C3%A0i%20%C4%91%E1%BA%B7t%20SSL%20251c6c2d35fd4234a0ebf8d8f51d9e03/Untitled%201.png)

- Restart lại nginx

`nginx -s reload`

### B3: Tắt tường lửa

`sudo firewall-cmd --add-service=http`

`sudo firewall-cmd --add-service=https`

`sudo firewall-cmd --runtime-to-permanent`

`sudo iptables -I INPUT -p tcp -m tcp --dport 80 -j ACCEPT`
`sudo iptables -I INPUT -p tcp -m tcp --dport 443 -j ACCEPT`

### B4: Tạo chứng chỉ

`certbot --nginx -d khoiht.click-d www.khoiht.click`

- Sau khi chạy câu lệnh thì điền email của mình vào

### B5: Vào lại để kiểm tra

![Untitled](./C%C3%A0i%20%C4%91%E1%BA%B7t%20SSL%20251c6c2d35fd4234a0ebf8d8f51d9e03/Untitled%202.png)

![Untitled]./C%C3%A0i%20%C4%91%E1%BA%B7t%20SSL%20251c6c2d35fd4234a0ebf8d8f51d9e03/Untitled%203.png)

## Các file ssl sau khi cấu hình

- Sau khi cấu hình ssl thì có những file như sau

![Untitled](./C%C3%A0i%20%C4%91%E1%BA%B7t%20SSL%20251c6c2d35fd4234a0ebf8d8f51d9e03/Untitled%204.png)

1. File csr là gì 
- Được viết tắt là Certificate Signing Request (csr) Nó chứa thông tin sẽ được bao gồm trong giấy chứng nhận của bạn như tên tổ chức của bạn, tên thông thường (tên miền), địa phương và quốc gia. 1 CSR sẽ được tạo ra ngay trước khi gửi yêu cầu cho bên cung cấp SSL để sinh ra SSL.Chứa **public key** mà nhà cung cấp chứng chỉ số sẽ sử dụng để tạo ra chứng chỉ ssl

Trong csr file chứa public key là `abcd.pem`

![Untitled](././C%C3%A0i%20%C4%91%E1%BA%B7t%20SSL%20251c6c2d35fd4234a0ebf8d8f51d9e03/Untitled%205.png)

1. File `options-ssl-nginx.conf` Là một số file thiết lập SSL trong file cấu hình nginx

![Untitled](./C%C3%A0i%20%C4%91%E1%BA%B7t%20SSL%20251c6c2d35fd4234a0ebf8d8f51d9e03/Untitled%206.png)

- ssl_session_cache shared:le_nginx_SSL:10m; - Thiết lập bộ nhớ cache cho các phiên kết nối SSL. Ở đây, sử dụng bộ nhớ được chia sẻ (shared memory) với tên "le_nginx_SSL", có dung lượng là 10 MB.
- ssl_session_timeout 1440m; - Thiết lập thời gian timeout (hết hạn) cho các phiên kết nối SSL, ở đây là 1440 phút (tương đương với 1 ngày).
- ssl_session_tickets off; - Tắt tính năng "session ticket" trên SSL. Session ticket là một cơ chế để lưu trữ thông tin phiên kết nối SSL trên máy khách thay vì lưu trữ trên server.
- ssl_protocols TLSv1.2 TLSv1.3; - Chỉ sử dụng các phiên bản mới nhất của giao thức SSL/TLS là TLSv1.2 và TLSv1.3.
- ssl_prefer_server_ciphers off; - Tắt tính năng ưu tiên sử dụng thuật toán mã hóa do server chọn. Khi được bật, tính năng này sẽ đảm bảo rằng client sẽ sử dụng các thuật toán mã hóa được ưu tiên bởi server thay vì sử dụng các thuật toán mà client ưa thích
- Còn dòng cuối chỉ định các thuật toán được sử dụng trên SSL

1. Thư mục "live": Chứa các tệp chứng chỉ SSL đã ký. Các tệp này được tải xuống trực tiếp từ Let's Encrypt và được cập nhật tự động khi chứng chỉ được gia hạn hoặc tái phát hành.
2. Thư mục "archive": Chứa các bản sao của các tệp chứng chỉ SSL đã ký. Các tệp này được lưu trữ cho mục đích sao lưu và không được cập nhật tự động.
3. Thư mục "renewal": Chứa các tệp cấu hình cho quá trình tái phát hành tự động của chứng chỉ SSL. Các tệp này đảm bảo rằng chứng chỉ được tự động gia hạn cùng với cấu hình máy chủ web của bạn.
4. Thư mục "keys": Chứa các khóa riêng tư được sử dụng để chỉ định các yêu cầu phát hành chứng chỉ SSL của bạn.