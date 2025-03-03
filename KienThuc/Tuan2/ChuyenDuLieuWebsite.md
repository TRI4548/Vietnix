# Chuyển dữ liệu website WordPress

## Backup website

Đăng nhập website WordPress >> Sử dụng plugin Duplicator >> Tạo bản backup >> Tải bản backup về máy

![image](https://github.com/user-attachments/assets/8f063a33-aad3-48a5-926a-451d4b9219aa)

![image](https://github.com/user-attachments/assets/74847362-c7f5-432f-adde-688157543bc4)

![image](https://github.com/user-attachments/assets/46db756e-a8b1-4ff8-bb7d-d924999929cf)

![image](https://github.com/user-attachments/assets/875c6617-2309-47dc-beb2-6f0d8d47b1b8)

![image](https://github.com/user-attachments/assets/b368c248-1a1d-4d65-bbc0-8583b492bb06)

## Restore website

Trước khi tiến hành restore file, đảm bảo đã trỏ tên miền về IP máy chủ hosting hoặc VPS.

- Upload 2 file đã được tải xuống lên hosting mới và đưa chúng vào website muốn thực hiện.
- Tạo 1 database mới.
- Sau khi tạo database xong, truy cập vào website của mình. tringuyen.space/installer.php.
-  tick chọn vào dòng I have read and accept term & notice > Nhấn Next. Tại mục Setup  điền các thông tin như sau:
  - Action: Chọn Connect and Remove All Data.
  - Hosts: Điền localhost.
  - Database: Nhập tên database mới tạo vào.
  - User: Nhập tên user database mới tạo.
  - Password: Nhập password database mới tạo.
- Xuất hiện bảng thông báo thì  nhấn chọn OK. Sau đó, hệ thống sẽ tiến hành nhập database.
- Có thể điều chỉnh title và URL. Sau đó nhấn Next.

Mất vài phút để hoàn tất và sau khi thành công sẽ hiện thông báo. Sau đó, có thể truy cập vào website. Những thông tin về tài khoản WordPress vẫn như cũ, không có thay đổi.

# Chuyển dữ liệu website bất kỳ

## Backup website

- Truy cập website trên panel >> Nén và tải tất cả các file ở docroot (/home/tringuyen.space)
- Truy cập phpMyAdmin và Export/Xuất database của website

![image](https://github.com/user-attachments/assets/ad247590-5e60-40e9-9d52-f86c563fd894)

## Restore website: Trước khi tiến hành restore file, đảm bảo đã trỏ tên miền về IP máy chủ hosting hoặc VPS.

- Upload và giải nén các file docroot đã tải lên VPS/Hosting mới
- Tạo database mới
- Import file database
  
![image](https://github.com/user-attachments/assets/05670060-8446-44fd-ba78-9a3ca3b61909)

- Kiểm tra lại site sau khi restore và fix các lỗi phát sinh (nếu có)
