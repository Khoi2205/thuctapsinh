# Basic Security

1. Mặc định linux sẽ có một số loại tài khoản để tách biệt với số lượng công việc 
    - 1.root
    - 2.system
    - 3.normal
    - 4.network
    
    Để cần kiếm soát truy cập, cần cấp các đặc quyền tối thiểu cho từng tài khoản , song song với đó xóa tài khoản không cần thiết , không hoạt động
    
    - Lệnh xem những tài khoản đăng nhập vào hệ thống cuối cùng
    
    `last`
    
    ![Imgur](https://i.imgur.com/JezRDzT.png)
    
    - root : Tài khoản đặc quyền cao nhất trong Linux/UNIX . Tài khoản có khả năng tạo ,xóa ,change passwd user.
    
     
    
    | su | sudo |
    | --- | --- |
    | 1. "su" là viết tắt của "switch user", cho phép người dùng chuyển đổi sang tài khoản root hoặc bất kỳ tài khoản khác cần thiết bằng cách nhập mật khẩu root | "sudo" là viết tắt của "superuser do", cho phép người dùng thực hiện các lệnh với quyền root mà không cần phải đăng nhập vào tài khoản root. |
    

 **Password encryption**

Bảo vệ mật khẩu đã trở thành một yếu tố quan trọng của bảo mật. Hầu hết các bản phân phối Linux đều dựa vào thuật toán mã hóa mật khẩu hiện đại có tên SHA-512 (Thuật toán băm an toàn 512 bit), do Cơ quan An ninh Quốc gia Hoa Kỳ (NSA) phát triển để mã hóa mật khẩu. Thuật toán SHA-512 được sử dụng rộng rãi cho các ứng dụng và giao thức bảo mật. Các ứng dụng và giao thức bảo mật này bao gồm TLS, SSL, PHP, SSH, S/MIME và IPSec. SHA-512 là một trong những thuật toán băm được thử nghiệm nhiều nhất

Sử dụng public/private key để xác thực  (nằm trong phần ssh)