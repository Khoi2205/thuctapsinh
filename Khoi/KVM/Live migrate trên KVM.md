## Live migrate trên KVM
### Bài toán đặt ra 
Trong quá trình vận hành để phục vụ cho việc nâng cấp và bảo trì hệ thống Cần chuyển từ VM từ host này sang host khác . Vậy các ứng dụng **quan trọng** đang chạy thì sẽ phải tắt rồi chuyển => Bài toán ở đây sẽ sử dụng KVM **live mirgate** sẽ đảm bảo được yêu cầu trên (ứng dụng vẫn chạy mà vẫn có thể chuyển được )

### Chuẩn bị các bước
Chuẩn bị ba máy cài đặt hệ điều hành CentOS 7 trong đó một máy dùng để cài đặt NFS dùng làm máy lưu file disk của VM và 2 máy cài đặt KVM.

Cấu hình

NFS server
1 CPU
1G RAM
20G disk
Host KVM
2 CPU
1.5G RAM
20G disk
