# Setup Mail Account (dùng Postfix và Dovecot)

1. Cài đặt hostname

```
nano /etc/hosts
# trỏ lại domain và IP

hostnamectl set-hostname mail.tringuyen.space
```

2. Cài đặt Postfix và Dovecot

```
sudo apt update
sudo apt install postfix dovecot-core dovecot-imapd dovecot-pop3d
sudo systemctl enable postfix
```

3. Chỉnh sửa file /etc/dovecot/conf.d/10-mail.conf để sử dụng Maildir: mail_location = maildir:~/Maildir

4. Chỉnh sửa file /etc/dovecot/conf.d/10-auth.conf để bật xác thực:

```
disable_plaintext_auth = no
auth_mechanisms = plain login
```

5. Reset dịch vụ Dovecot

```
sudo systemctl restart dovecot
sudo systemctl enable dovecot
```

6. Cấu hình MX record

7. Fix lỗi không thấy file log của Postfix (nếu có)

```
sudo chown syslog:adm /var/log
sudo chmod 0775 /var/log

sudo service rsyslog restart
sudo service postfix restart
```

8. Tạo user và test gửi mail 

```
adduser tringuyen

su - tringuyen

echo "Test email, hello from Tri Nguyen" | mail -s "Test Send Mail from Tri Nguyen" blackpig@trungtranabc.site
```

![image](https://github.com/user-attachments/assets/5abdbfc1-49ea-4928-a9cc-55c2613e95a2)

Gửi thành công !

9. Test nhận mail

![image](https://github.com/user-attachments/assets/305c92db-56a7-400a-af9a-0f33e18cf6d4)

![image](https://github.com/user-attachments/assets/39dee195-1570-4a01-a03b-378a870f3fab)

Nhận thành công !

# Setup FTP

1. Cài đặt vsftpd (Very Secure FTP Daemon)

```
sudo apt update
sudo apt install vsftpd -y
```

2. Cấu hình vsftpd tại /etc/vsftpd.conf, câp nhật các dòng sau:

```
local_enable=YES
write_enable=YES
chroot_local_user=YES
pasv_enable=YES
pasv_min_port=10000
pasv_max_port=10100
```

3. Khởi động lại vsftpd: sudo systemctl restart vsftpd

4. Tạo và gán quyền cho thư mục của user

```
# Đã tạo user tringuyen ở phần trên

sudo chown ftp:tringuyen /home/tringuyen
sudo chmod 750 /home/tringuyen
```

5. Kiểm tra kết nối

![image](https://github.com/user-attachments/assets/bbf3bb10-879c-4fe2-8a88-95f838f8bf4a)

Kết nối thành công !

