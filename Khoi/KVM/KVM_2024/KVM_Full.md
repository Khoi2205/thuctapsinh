# KVM basic

# Mục Lục

 [1.Khái niệm](#1)
 [2.KVM Stack](#2)
 [3.KVM - QEMU](#3kvm---qemu)
 [4.Các tính năng của KVM](#4các-tính-năng-của-kvm)









## 1.Khái niệm

KVM (viết tắt của Kernel-based Virtual Machine) là một mô-đun ảo hóa mã nguồn mở được tích hợp nhân Linux , cho phép chạy cùng nhiều máy ảo trên một máy chủ vật lý . Hoạt động như Hypervisor tạo môi trường riêng biệt cho VM, gồm RAM, hệ điều hành , tài nguyên , phần cứng

## 2.KVM Stack


![](./image/Screenshot_1.png)


KVM Stack bao gồm 4 tầng : 

User-facing tools : Là các công cụ quản lý máy ảo hỗ trợ KVM .
VD Các công cụ giao diện đồ họa như (virt-manager) hoặc giao diện dòng lệnh như (virsh).

Management layer : Lớp này dùng thư viện libvirt cung cấp các API để các công cụ quản lý máy ảo hoặc hypervisor tương tác với KVM thực hiện các thao tác quản lý tài nguyên ảo hóa 

Virtual machine: Chính là các máy ảo người dùng tạo ra. Thông thường, nếu không sử dụng các công cụ như virsh hayvirt-manager, KVM sẽ sử được sử dụng phối hợp với một hypervisor khác điển hình là QEMU.

Kernel support: Chính là KVM, cung cấp một module làm hạt nhân cho hạ tầng ảo hóa (kvm.ko) và một module kernel đặc biệt hỗ trợ các vi xử lý VT-x hoặc AMD-V (kvm-intel.ko hoặc kvm-amd.ko)

## 3.KVM - QEMU

- Hệ thống ảo hóa KVM hay đi liền với QEMU. Về mặt bản chất, QEMU là một emulator. QEMU có khả năng giả lập tài nguyên phần cứng, trong đó bao gồm một CPU ảo. Các chỉ dẫn của hệ điều hành tác động lên CPU ảo này sẽ được QEMU chuyển đổi thành chỉ dẫn lên CPU vật lý nhờ một translator là TCG(Tiny Core Generator) nhưng TCG hiệu suất ko cao.

- Do KVM hỗ trợ ánh xạ CPU vật lý sang CPU ảo, cung cấp khả năng tăng tốc phần cứng cho máy ảo và hiệu suất của nó nên QEMU sử dụng KVM làm accelerator tận dụng tính năng này của KVM thay vì sử dụng TCG.

## 4.Các tính năng của KVM

4.1 . Memory Management

KVM thừa kế tính năng quản lý bộ nhớ mạnh mẽ của Linux. Vùng nhớ của máy ảo được lưu trữ trên cùng một vùng nhớ dành cho các tiến trình Linux khác và có thể swap. KVM hỗ trợ NUMA (Non-Uniform Memory Access - bộ nhớ thiết kế cho hệ thống đa xử lý) cho phép tận dụng hiệu quả vùng nhớ kích thước lớn.
- KVM hỗ trợ các tính năng ảo của mới nhất từ các nhà cung cấp CPU như EPT (Extended Page Table) của Microsoft, Rapid Virtualization Indexing (RVI) của AMD để giảm thiểu mức độ sử dụng CPU và cho thông lượng cao hơn.
- KVM cũng hỗ trợ tính năng Memory page sharing bằng cách sử dụng tính năng của kernel là Kernel Same-page Merging (KSM).


4.2 Live migration

KVM hỗ trợ live migration cung cấp khả năng di chuyển ác máy ảo đang chạy giữa các host vật lý mà không làm gián đoạn dịch vụ. Khả năng live migration là trong suốt với người dùng, các máy ảo vẫn duy trì trạng thái bật, kết nối mạng vẫn đảm bảo và các ứng dụng của người dùng vẫn tiếp tục duy trì trong khi máy ảo được đưa sang một host vật lý mới. KVM cũng cho phép lưu lại trạng thái 


