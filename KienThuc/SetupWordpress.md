# Demo setup tự động trên gói hosting có cPanel

Chuẩn bị: 
- Setup hosting website ([tham khảo](https://github.com/TRI4548/Vietnix/blob/main/KienThuc/SetupHosting_VPS.md#setup-hosting-website))

- Cài SSL

- Redirect http => https

## Setup tự động bởi Wordpress Management

Đăng nhập cPanel >> Wordpress Management >> Install >> Lưu lại các thông tin và tiến hành cài đặt

![image](https://github.com/user-attachments/assets/3fd41f72-c6ee-4b91-a30c-934890422ec5)

![image](https://github.com/user-attachments/assets/1993675f-f136-4600-a0fd-68044d2c343f)

![image](https://github.com/user-attachments/assets/7ea04a4b-c13e-4497-b9ed-7184bcd4bf93)

## Setup tự động bởi Wordpress Manager by Softaculous (nếu có hỗ trợ bởi hosting provider)

Đăng nhập cPanel >> Wordpress Manager by Sofataculous >> Install >> Lưu lại các thông tin, chọn plugin và theme phù hợp và tiến hành cài đặt

![image](https://github.com/user-attachments/assets/0150c4c6-e28d-422e-b6e4-f0a701bb8700)

![image](https://github.com/user-attachments/assets/2c7eb9c5-6ff1-4c71-b1a7-8abba84d2609)

![image](https://github.com/user-attachments/assets/cd16f280-08c9-407b-9251-f12d49c45c5d)

![image](https://github.com/user-attachments/assets/9896fda6-a83e-4f62-95bb-6ee467aafe66)

# Demo setup thủ công với CyberPanel

- Chuẩn bị:

  - Tên miền, VPS hoặc Hosting sử dụng CyberPanel

  - Trỏ tên miền về IP của VPS hoặc Hosting

- Setup:

  - Đăng nhập CyberPanel >> Create Website

  ![image](https://github.com/user-attachments/assets/fe652795-814c-46d5-b9b8-4df177cd3979)

  - Tạo database cho website
 
  ![image](https://github.com/user-attachments/assets/28ede9aa-496e-4f37-9366-b785829ed660)


  - Tải WordPress >> Upload file zip lên website >> Giải nén
 
  ![image](https://github.com/user-attachments/assets/bea1cfc2-28ad-4127-abe2-bd246e364985)

  - Truy cập và cài đặt (Khai báo database và tạo username/password của WordPress
 
  ![image](https://github.com/user-attachments/assets/d6e02baa-bbe3-46c9-a576-9c5e6a1207c4)

  ![image](https://github.com/user-attachments/assets/70d27f93-b1af-4d9d-bfb7-90dc8ffd42ea)

# Cài đặt các Theme và các Plugin trong WordPress

- Theme trong WordPress là một công cụ cho phép thay đổi bố cục và thiết kế của website.

  - Cài đặt theme tại giao diện
  
  ![image](https://github.com/user-attachments/assets/a7c518ab-d87f-46fa-bad0-d14556fc4021)

  - Hoặc bằng cách upload lên thư mục chứa theme của WordPress (thường nằm ở File Manager của các Hosting Control Panel): /home/"<user>"/public_html/wp-content/themes
 
- Plugin là một chương trình, ứng dụng bổ sung được tích hợp vào website WordPress, giúp mở rộng chức năng hiện có hoặc thêm một tính năng mới cho website.

  - Cài đặt plugin tại giao diện (sau khi Install thì Activate để có thể sử dụng)
 
  ![image](https://github.com/user-attachments/assets/cc25f9d7-f9bf-4c5d-bd6a-295b42075015)

  - Hoặc bằng cách upload lên thư mục chứa plugin của WordPress (thường nằm ở File Manager của các Hosting Control Panel): /home/"<user>"/public_html/wp-content/plugins
    Rồi lên giao diện WordPress để Activate

