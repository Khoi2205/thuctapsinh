## Bài lab kết nối nguồn điện
### Mục tiêu bài lab , thực hiện kết nối nguồn giữa các thiết bị vs nhau hoặc các thiết bị với tủ rack

B1 : Thực hiện tạo  `Power Panels`

![Alt text](./anh_lab/image.png)

![Alt text](./anh_lab/image-1.png)


B2 : Thực hiện tạo  `Power Feeds`

![Alt text](./anh_lab/image-2.png)


B3 : Thực hiện kết nối các thiết bị (router)

- Trên các thiết bị thì cần add thêm thêm các   `components`

VD :

![Alt text](./anh_lab/image-3.png)
![Alt text](./anh_lab/image-4.png)

![Alt text](./anh_lab/image-5.png)

- Vào `divice` thêm R1 vào tủ rack,rồi sau đó vào `power Powort` thực hiện kết nối với tủ rack


![Alt text](./anh_lab/image-6.png)

![Alt text](./anh_lab/image-7.png)

![Alt text](./anh_lab/image-8.png)


Vào `Connections` để check xem kết nối, hoặc có thể vào `rack` để xem kết nối chưa



![Alt text](./anh_lab/image-9.png)


![Alt text](./anh_lab/image-10.png)


*   **Thực hiện kết nối nguồn cho switch**

![Alt text](./anh_lab/image-11.png)


![Alt text](./anh_lab/image-12.png)


### Mô hình tổng hợp (các phần định nghĩa nằm trong phần này ) [Định nghĩa](Introduction.md)


Mục Tiêu bài lab .Thưc hiện cấu hình VLAN cho mạng,thực hiện hoàn tất các modul trong device và origanization

B1 : Thực hiện cấu hình ở organization

![Alt text](./anh_lab/image-13.png)

![Alt text](./anh_lab/image-14.png)

![Alt text](./anh_lab/image-15.png)

![Alt text](./anh_lab/image-16.png)


`Trong contact `


![Alt text](./anh_lab/image-19.png)

![Alt text](./anh_lab/image-18.png)


![Alt text](./anh_lab/image-20.png)


![Alt text](./anh_lab/image-21.png)


Tiếp theo là đến phần rack



![Alt text](./anh_lab/image-22.png)


![Alt text](./anh_lab/image-25.png)

![Alt text](./anh_lab/image-24.png)


**Phần device**

![Alt text](./anh_lab/image-26.png)

![Alt text](./anh_lab/image-27.png)

![Alt text](./anh_lab/image-28.png)


![Alt text](./anh_lab/image-29.png)



**Cấu hình nguồn**


![Alt text](./anh_lab/image-30.png)


![Alt text](./anh_lab/image-31.png)


![Alt text](./anh_lab/image-32.png)

![Alt text](./anh_lab/image-33.png)


![Alt text](./anh_lab/image-34.png)



**Thực hiện tương tự với sw và firewall**

**Thực hiện thêm module bay**


![Alt text](./anh_lab/image-35.png)

![Alt text](./anh_lab/image-36.png)

 ![Alt text](./anh_lab/image-37.png)


 
**Thực hiện quá trình kết nối từ server đến sw**

![Alt text](./anh_lab/image-38.png)


**add cổng interface cho server và switch**

![Alt text](./anh_lab/image-42.png)


Sau khi add xong sẽ có kq như dưới



![Alt text](./anh_lab/image-41.png)

![Alt text](./anh_lab/image-40.png)



Thực hiện kết nối 


![Alt text](./anh_lab/image-44.png)

![Alt text](./anh_lab/image-43.png)



**Tiếp theo phần IPAM**


![Alt text](./anh_lab/image-45.png)

![Alt text](./anh_lab/image-46.png)

![Alt text](./anh_lab/image-47.png)

![Alt text](./anh_lab/image-48.png)

![Alt text](./anh_lab/image-49.png)

![Alt text](./anh_lab/image-50.png)

![Alt text](./anh_lab/image-51.png)


![Alt text](./anh_lab/image-52.png)   

![Alt text](./anh_lab/image-53.png)

![Alt text](./anh_lab/image-54.png)

![Alt text](./anh_lab/image-55.png)

![Alt text](./anh_lab/image-56.png)

![Alt text](./anh_lab/image-57.png)

![Alt text](./anh_lab/image-58.png)

![Alt text](./anh_lab/image-59.png)



Đây là kết quả sau khi tạo 


![Alt text](./anh_lab/image-60.png)


Thực hiện gán IP cho các cổng interface 


![Alt text](./anh_lab/image-63.png)


![Alt text](./anh_lab/image-64.png)


- Sau khi thiết lập cấu hình vào server để xem


![Alt text](./anh_lab/./anh_lab/image-65.png)
