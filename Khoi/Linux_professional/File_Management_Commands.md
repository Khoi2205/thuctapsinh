## Điều hướng tới thư mục ##
1. `pwd` : Chỉ ra đường dãn của thư mục
2. `cd - ` : Điều hướng tới thư mục cuối mà bạn đã làm
3. `cd .. ` : Trờ về thư mục cha
## Hiển thị danh sách của thư mục ##

`ls -l` : Hiển thị file,ngày tháng , quyền của thư mục
`ls -a` : Hiển thị cả file có cả file `.`
`ls -lt` Liệt kê các tệp được sắp xếp theo thời gian sửa đổi lần cuối với các tệp được sửa đổi gần đây nhất hiển thị ở trên cùng(tùy chọn nhớ -l cung cấp định dạng dài có khả năng đọc tốt hơn).
![Imgur](https://i.imgur.com/ulO77LD.png)
`ls -lh` Liệt kê kích thước tệp ở định dạng con người có thể đọc được.
`ls -lR` Hiển thị đệ quy tất cả các thư mục con.
cây Sẽ tạo một biểu diễn cây của hệ thống tệp bắt đầu từ thư mục hiện tại
![Imgur](https://i.imgur.com/xaxxIlb.png)
`cp -p`
Sẽ sao chép tệp từ nguồn đến đích. -p là viết tắt của bảo quản. Nó
giữ nguyên các thuộc tính ban đầu của tệp trong khi sao chép như chủ sở hữu tệp, dấu thời gian,
nhóm, quyền, v.v.
`cp -R source_dir`: Sẽ sao chép thư mục nguồn đến đích được chỉ định theo cách đệ quy.
`rm -R dir-name` :Sẽ xóa thư mục dir-name theo cách đệ quy.
`rm -rf tên thư mục` :Sẽ xóa thư mục dir theo cách đệ quy, bỏ qua các tệp không tồn tại 
`mkdir -p dir-name/dir-name` : Tạo phân cấp thư mục. Tạo các thư mục mẹ nếu cần, nếu không
hiện hữu.
(đã có trong file basic.md)

## Hiển thị thông tin hiện tại của hệ thống
`uname [OPTION]`
```
-s, --kernel-name In tên nhân.
-n, --nodename In tên máy chủ nút mạng.
-r, --kernel-release In bản phát hành kernel.
-v, --kernel-version In phiên bản kernel.
-m, --machine In tên phần cứng của máy.
-p, --processor In loại bộ xử lý hoặc "không xác định".
-i, --hardware-platform In nền tảng phần cứng hoặc "không xác định".
-o, --operating-system In hệ điều hành.
--help Hiển thị thông báo trợ giúp và thoát.
--version Hiển thị thông tin phiên bản và thoát.
```
Câu lệnh thường dùng là `uname -a` : Hiển thị tất cả thông tin  về hệ thống
![Imgur](https://i.imgur.com/vrfUs9n.png)

`systemctl start [tên dịch vụ]` : Để bắt đầu một dịch vụ
`systemctl stop [tên dịch vụ] `Để dừng một dịch vụ
`systemctl restart [tên dịch vụ]` Để khởi động lại một dịch vụ
`systemctl reload [tên dịch vụ]` Để yêu cầu dịch vụ tải lại cấu hình của nó
`systemctl status [tên dịch vụ]` Để hiển thị trạng thái hiện tại của dịch vụ