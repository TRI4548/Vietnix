## cPanel Part 2

### Software

- Wordpress Manager by Softaculous: đa dạng cài đặt các phần mềm mã nguồn mở hơn thay vì chỉ cài đặt và quản lý wordpress như WordPress Management

- MultiPHP Manager (hỗ trợ bởi cPanel): tùy chọn các phiên bản PHP khác nhau cho từng website.

- Select PHP Version (hỗ trợ bởi cloudlinux): áp dụng version PHP giống nhau cho toàn bộ website, thường sẽ cài thêm extension ở đây
- Setup Node.js App: hỗ trợ người dùng cài đặt các ứng dụng có mã nguồn nodejs

- Cronjob: lập lịch chạy tự động

### Câu hỏi tìm hiểu thêm

#### So sánh Disk Usage và Database Disk Usage ở mục Statistic trên cPanel

 => Trả lời:
  - Disk Usage thể hiện tổng dung lượng tất cả các file mà account đó sử dụng:
    - Các tập tin mà chứa trong thư mục /home
    - Các tập tin tồn tại trong các thư mục con ẩn
    - Các mail được quản lý bởi Mailman
    - Các tập tin mà thư mục /home của bạn không chứa (chưa hiểu, sẽ hỏi lại mentor sau)
 
  - Database disk usage thể hiện dung lượng sử dụng của database của tài khoản đó. Tuy nhiên khi dung lượng của disk usage chạm mức quota thì vẫn có thể ghi thêm dữ liệu vào database

Nguồn tham khảo:
  - [Document cPanel](https://docs.cpanel.net/cpanel/files/disk-usage/)

  - [Forum: Does the Disk Usage include MySQL usage?](https://support.cpanel.net/hc/en-us/articles/7232236971927-Does-the-Disk-Usage-include-MySQL-usage)


#### So sánh Number of Processes vs Entry Processes

=> Trả lời:
  - Number of Processes là chỉ số thể hiện số lượng tiến trình mà hosting có thể xử lý đồng thời tại một thời điểm

  - Entry Processes là số lượng PHP script có thể chạy tại cùng một thời điểm

Nguồn tham khảo:
  - [Number of Processes (Vietnix)](https://vietnix.vn/number-of-processes-la-gi/)

  - [Entry Processes (Vietnix)](https://vietnix.vn/entry-processes-la-gi/)


## Lab
### Tạo Wordpress site với primary domain

1. Trỏ IP về Hosting

![image](https://github.com/user-attachments/assets/140dd68c-3ee2-4112-9c80-5234eeda6f25)

![image](https://github.com/user-attachments/assets/43301d3f-9e99-4464-a50b-1a813d9e1131)

2.	Tạo email cho domain

![image](https://github.com/user-attachments/assets/a5a47d90-23f0-4282-8e13-5ffe0f76962d)

![image](https://github.com/user-attachments/assets/9b4658bd-871a-475f-b25d-8ac5eab9831b)

3.	Cài đặt WordPress với WordPress Manager by Softaculous

![image](https://github.com/user-attachments/assets/4fe6d156-7d98-463f-8cae-092f233dbd98)

![image](https://github.com/user-attachments/assets/4066beed-2153-4bc1-bf11-b0962dafbd1a)

4.	Cài đặt free SSL (Let’s Encrypt)

![image](https://github.com/user-attachments/assets/beb2254c-7702-4e60-9bc3-bd6a7b81a000)

![image](https://github.com/user-attachments/assets/c921ba3a-e716-4a8d-98a8-ff5927bb4c61)

5.	Chuyển hướng site từ http sang https

![image](https://github.com/user-attachments/assets/ddf9fe2a-5dfb-4737-b529-326b927d44e0)

![image](https://github.com/user-attachments/assets/a82ea4f7-317c-43a8-b624-7dd577398d36)

6. Test site

![image](https://github.com/user-attachments/assets/a28c462e-d644-4cf1-a895-70fd64a4a312)

### Tạo Web với Sub domain

1. Tạo sub domain

![image](https://github.com/user-attachments/assets/04293700-1d14-4016-a005-2a5fbdeac62e)

![image](https://github.com/user-attachments/assets/d3becc50-7ad5-4b1a-ad92-7c15b01d3619)

2.	Trỏ sub domain về hosting (dùng CNAME cho sub domain vì record A đã trỏ về hosting)

![image](https://github.com/user-attachments/assets/56496f7c-ca1d-4380-846c-9b278311d3c1)

3.	Vào document root và tạo file index.html để test

![image](https://github.com/user-attachments/assets/ea329366-b0a7-4c90-a141-782ff2abe083)

![image](https://github.com/user-attachments/assets/8bf08e53-87ee-451c-8fa3-7b4533e1f248)

4. Test site sub domain

![image](https://github.com/user-attachments/assets/455a9e0c-b021-48ed-b68b-759d9cd8d424)


