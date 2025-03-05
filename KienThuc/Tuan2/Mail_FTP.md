## Setup Mail Account (dùng Postfix và Dovecot)

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


