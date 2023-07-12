## Các bước cài đặt KVM trên centOS7
Yêu cầu phần mềm để thực hiện bài Lab : 
+ VMware Workstation 
+ Hệ điều hành Linux có  hỗ trợ công nghệ ảo hóa: 2CPU, 2GB RAM, 20GB Disk
+ File ISO của hệ điều hành để cài lên máy ảo KVM


B1: Check VMware Workstation có lỗi hỗ trợ ảo hóa không nếu báo lỗi thì thực hiện bước sau : 

Mở cmd run với quyền administrator 
chạy câu lệnh sau rồi vào VMware 
`bcdedit /set hypervisorlaunchtype off`

**B2: Kiểm tra xem hỗ trợ ảo hóa không bằng câu lệnh** 

`egrep -c "svm|vmx" /proc/cpuinfo`


![Alt text](image-12.png)


- Nếu kq trả về `0` thì không hỗ trợ ảo hóa .Còn khác số 0 là số nhân có thể hỗ trợ làm ảo hóa 

Nếu VMware, ta phải bật hỗ trợ ảo hóa trong Vitual Machine Setting của máy ảo. Đánh dấu vào 2 ô như hình dưới đây:


![Alt text](image-11.png)




**B3: Thực hiện cài đặt các gói cần thiết**

`yum -y install qemu-kvm libvirt virt-install bridge-utils virt-manager`

Trong đó:

`qemu-kvm`: Phần phụ trợ cho KVM.
`libvirt`: Cung cấp libvirt mà bạn cần quản lý qemu và KVM bằng Libvirt.
`Bridge-utils`: Chứa một tiện ích cần thiết để tạo và quản lý các thiết bị bridge
`virt-manager`: Cung cấp giao diện đồ họa để quản lý máy ảo
`virt-install`: Cung cấp lệnh để cài đặt máy ảo.

- Khi cài đặt hoàn tất ,kiểm tra bằng câu lệnh dưới

`lsmod | grep kvm`


![Alt text](image-13.png)



**Bật libvirt và khởi động cùng hệ thống**
`systemctl start libvirtd`
`systemctl enable libvirtd`


**Tạo một card mạng Brigde**

```
nmcli connection add type bridge autoconnect yes con-name br0 ifname br0
nmcli connection modify br0 ipv4.addresses 192.168.202.55/24 ipv4.method manual 
nmcli connection modify br0 ipv4.gateway 192.168.202.2
nmcli connection modify br0 ipv4.dns 8.8.8.8  	
nmcli connection delete ens33
nmcli connection add type bridge-slave autoconnect yes con-name ens33 ifname ens33 master br0
```

Sau khi chạy câu lệnh trên thì khởi động lại hệ thống bằng câu lệnh 
`init 6`

Nhìn vào card mạng thì thấy có thêm `br0`.Thực hiện ssh vào `192.168.202.55` để tiếp tục làm bài lab


![Alt text](image-14.png)


**Sử dụng công cụ virt-manager**
Download và lưu file ISO Minimal vào thư mục /var/lib/libvirt/file-iso/

```
cd /var/lib/libvirt/
mkdir file-iso
cd file-iso

yum install -y wget
wget http://repos-va.psychz.net/centos/7.6.1810/isos/x86_64/CentOS-7-x86_64-Minimal-1810.iso
```

*Lưu ý có thể dùng mobaxter để tải file iso vào linux thay cho bước weget*


![Alt text](image-15.png)


Đối với bản Minimal thì để sử dụng công cụ đồ họa virt-manager, ta cần cài đặt gói X-Window

 `yum install -y "@X Window System" xorg-x11-xauth xorg-x11-fonts-* xorg-x11-utils`

**Truy cập Virt-manager để cấu hình VM**
`virt-manager`

Xuất hiện công cụ bằng GUI


![Alt text](image-16.png)


Thực hiện tạo máy ảo 


![Alt text](image-17.png)


Thực hiện chọn hệ điều hành 


![Alt text](image-18.png)



Chọn đường dẫn cho File ISO để cài cho VM


![Alt text](image-19.png)


![Alt text](image-20.png)


![Alt text](image-21.png)

![Alt text](image-22.png)


Cài đặt các thông số phần cứng cơ bản muốn đặt cho máy VM


![Alt text](image-23.png)


![Alt text](image-24.png)

![Alt text](image-25.png)


Phần Network selection ta sẽ gắn card mạng vào bridge bro



![Alt text](image-26.png)


Sau đó cài CentOS 7 như bình thường

Xem danh sách cũng như trạng thái các máy ảo KVM
`virsh list --all`


![Alt text](image-27.png)


**3. Một số thao tác khác trên virt-manager**

Quản lý các VM đã tạo tạo giao diện của virt-manager


![Alt text](image-28.png)


Vào đây để xem thông số 


![Alt text](image-29.png)



Để tạo snapshot cho VM, open VM đó và vào chọn vào biểu tượng như trong hình


![Alt text](image-30.png)


![Alt text](image-31.png)

