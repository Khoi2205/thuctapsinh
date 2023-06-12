# File system

## 1.Cấu trúc hệ thống tập tin
![Imgur](https://i.imgur.com/UbAy009.png)
- File cấu trúc hệ thống tập tin trong linux được có cấu trúc kiểu dạng cây Cây thường được miêu tả là đảo ngược và bắt đầu từ thư mục thường được gọi là thư mục gốc, đánh dấu điểm bắt đầu của hệ thống tệp phân cấp và cũng được ký hiệu là /.
- 
- Dùng lệnh **ll** để xem chi tiết thư mục trong file linux

![Imgur](https://i.imgur.com/92GgAgw.png)

## Trong đó :

- **/** : Là thư mục root nơi mở đầu logic cho hệ thống của Linux ,tất cả đường dẫn bắt đầu đều từ / . Thư mục / là thư mục cao nhất , chỉ có người có quyền root mới được thay đổi trong thư mục này
- **/bin :**  Thư mục chứa các file nhị phân của chương trình như pwd , cat , mv …

![Imgur](https://i.imgur.com/1ti5Fkp.png)

- **/ sbin :** Chứa đựng các file nhị phân của chương trình hoạt động của hệ thống , Thường được sử dụng cho mục đích duy trì của hệ thống
- **/boot :** Chứa các tệp khi bắt đầu khởi động và tệp của kernel

![Imgur](https://i.imgur.com/afYpFPG.png)

- ****/dev:**** Nơi lưu trữ các ổ cứng , thiết bị ngoại vi , hay các thiết bị được cài vào
- ********/etc******** : Chứa các file cấu hình cho chương trình hoạt động
- **************/home************** Thư mục file của từng user
- **************/lib :************** Chứa các file hỗ trợ cho các file được thực thi
- /****mnt**** : Về cơ bản, đây là một thư mục giữ chỗ được sử dụng để gắn các thư mục hoặc ổ đĩa khác.
- ********/proc******** : Chứa đựng thông tin về quá trình xử lý của hệ thống
- ****/usr**** : Chứa đựng các file binary ,library cho các chương trình
    - Trong ****/usr**** sẽ có : **/usr/bin ,/usr/sbin,/usr/lib,/usr/local**
- ******/var :****** Chứa đựng nhật ký các file trong quá trình chạy
    - VD : /var/log : Nhật ký của hệ thống…