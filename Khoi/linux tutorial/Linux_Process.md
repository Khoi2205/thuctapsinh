# Linux_Process

## 1.Định nghĩa

- Là một đối tượng quan trọng trong hệ điều hành linux , thể hiện một tiến trình hoặc một chương trình đang chạy trong linux
- Mỗi quá trình được quản lý bởi kernel có các thuộc tính như ID, quá trình, tài nguyên sử dụng
- Các quá trình trên Linux hỗ trợ cho việc thực thi các tác vụ đa luồng, cho phép nhiều công việc được thực hiện đồng thời trên một máy tính. Việc quản lý và tương tác với các quá trình Linux là rất quan trọng khi phát triển ứng dụng trên hệ điều hành Linux.

## 2. Process

- Sử dụng lệnh  ********top********  để xem

```jsx
top
```
![Imgur](https://i.imgur.com/IS95RuI.png)

- Process Identification Number (PID)
- Process owner (USER)
- Priority (PR) and nice values (NI) :Ưu tiên (PR) và giá trị tốt
- Virtual (VIRT), physical (RES), and shared memory (SHR)
- Status (S) : Tình trạng
- Percentage of CPU (%CPU) and memory (%MEM) used: Chiềm bao nhiêu %
- Execution time (TIME+): thời gian thực hiện
- Command (COMMAND)

Lệnh **pstree** hiển thị các quy trình đang chạy trên hệ thống dưới dạng sơ đồ cây thể hiện mối quan hệ giữa một quy trình và quy trình mẹ của nó cũng như bất kỳ quy trình nào khác mà nó đã tạo. Các mục lặp lại của một quy trình không được hiển thị và các chuỗi được hiển thị trong dấu ngoặc nhọ

```jsx
yum install -y psmisc
pstree

```

![Imgur](https://i.imgur.com/zOSmdbc.png)

## 2. Kill Process

- Để kết thúc một tiến trình , gõ lệnh kill -n + pid ( cần sử dụng quyền cao nhất là quyền root)

| Signal Name | Single Value | Effect                  |
| ----------- | ------------ | ----------------------- |
| SIGHUP      | 1            | Hangup                  |
| SIGINT      | 2            | Interrupt from keyboard |
| SIGKILL     | 9            | Kill signal             |
| SIGTERM     | 15           | Termination signal      |
| SIGSTOP     | 17, 19, 23   | Stop the process        |
- vd **kill - 9**  + pid  : Dừng tiến trình mà không cho phép nó hoàn thành , hoặc lưu dữ liệu ,dừng ngay sau khi sử dụng lệnh