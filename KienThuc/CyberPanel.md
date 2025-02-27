## Cấu trúc file
- cyperpanel sử dụng cấu trúc file mặc định cho các service hệ thống
  - /usr/local/CyberCP/CyberCP/settings.py - cấu hình chính cho cyberpanel
  - Các file data của CyberPanel: /usr/local/CyberCP/
  - cyberpanel tạo user cyberpanel, với một số cấu hình đặt ở /home/cyberpanel
  - Các tool hỗ trợ xem thông tin pass: /etc/cyberpanel
- cyberpanel hỗ trợ cli với lệnh cyberpanel
- Hỗ trợ API: https://cyberpanel.docs.apiary.io/#reference/server/verify-connection

## Cài đặt thành công CyperPanel

![image](https://github.com/user-attachments/assets/483e3016-fbef-40f8-a37c-39ed9026a780)

![image](https://github.com/user-attachments/assets/4ee324f0-c317-454a-9610-5ca442aec299)

## Tạo dự án website ngôn ngữ Laravel
### Tạo Website: Home >> Websites >> Create Website

![image](https://github.com/user-attachments/assets/83e65d9d-020c-432a-a9d0-b6cb589c20db)

### Gán self signed SSL: Home >> Manage SSL >> Select Website >> Issue SSL

![image](https://github.com/user-attachments/assets/5a6e5681-e8a5-4294-af7e-0b46092ae35f)

### Chuyển hướng HTTP sang HTTPS (Home >> Website >> Select Website >> Manage >> Rewrite Rules 

![image](https://github.com/user-attachments/assets/5a35a2be-72b6-4bad-a40d-913f09d5aaa7)


### Trỏ domain về VPS hosting

![image](https://github.com/user-attachments/assets/a685ed35-0824-42db-a2cf-a259ea0a7e1e)

### Cài đặt dự án Laravel
1. SSH vào VPS
2. Chạy các dòng lệnh sau

```
# Đến thư mục website chứa source code vừa tạo trên cyberpanel
cd /home/lavarel.tringuyen.space

# Cài đặt project Lavarel
composer create-project laravel/laravel laravel-app

# Xóa thư mục public_html
rm -fr public_html

# Tạo liên kết mềm public_html trỏ đến thư mục laravel-app để chạy web
ln -s laravel-app/public public_html

#Tạo thư mục và file chứa log
touch /home/tringuyen.space/laravel-app/storage/logs/laravel.log

# Fix lại quyền
sudo chmod -R ugo+rw storage
```

3. Kiểm tra

![image](https://github.com/user-attachments/assets/8f0c1fc9-ffe7-4dcf-bbd7-e3cba81af803)

### Bật debug log trong site Laravel

- Truy cập File Manager của website >> tìm file .env

![image](https://github.com/user-attachments/assets/20e82bca-9fbf-428c-a13b-30e2f9a5ed8c)

- Tìm chứ **APP_DEBUG** chuyển **false** thành **true**

![image](https://github.com/user-attachments/assets/c70f4ff2-6d71-4d8b-a9c0-e70452a64386)
