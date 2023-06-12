# System_info

## 1. Định nghĩa

Là một thuật ngữ trong lập trình để chỉ thông tin về hệ thống (system) mà chương trình đang chạy trên đó. Thông tin này có thể bao gồm các thông số như tên hệ điều hành, phiên bản hệ điều hành, kiến trúc CPU, dung lượng ổ cứng, RAM, và các phần cứng khác của máy tính hoặc thiết bị.

## 2. Xem thông tin về system

### 2.1 .Xem thông tin về nhà phân phối

```jsx
cat /etc/*release
```

![Imgur](https://i.imgur.com/j6yiIGu.png)

### 2.2 .Xem version của kenel

```jsx
uname -r
```

![Imgur](https://i.imgur.com/4IPvvs5.png)

### 2.3 .Xem thông tin về bộ nhớ

```jsx
head /proc/meminfo
```

![Imgur](https://i.imgur.com/TVA8r6Z.png)

### 2.4 .Xem thông tin về File system

`df -h`

![Imgur](https://i.imgur.com/Ws49oEA.png)

### 2.5 .Xem thông tin về CPU

`cat /proc/cpuinfo | grep mode | uiq -c`

Hoặc có thể xem chi tiết về CPU 

`cat /proc/cpuinfo` 

![Imgur](https://i.imgur.com/oOzINUU.png)