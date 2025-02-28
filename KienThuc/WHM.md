## Ðổi Primary Domain

B1: Modify an Account => Tìm kiếm User => Modify
B2: Tại giao diện Modify => đổi Primary Domain => bấm Save

Có 2 trường hợp xảy ra:
- Save thành công
- WHM báo đã có domain này tồn tại trên hệ thống => Check domain này khách hàng có add trước đó là add-on domain hay không, nếu đã add thì báo khách chủ động remove ra.

## Migrate và Transfer
Lab

Server Hosting WHM-1 là gói Hosting Maxspeed: 14.225.220.231
Server Hosting WHM-2 là gói Business        : 14.225.220.235

Yêu cầu: Nâng cấp gói Hosting từ Business lên Maxspeed

B1: Login WHM Maxspeed => Transfer tool => đăng nhập thông tin server Business => Scan Remote Server
B2: Chọn tài khoản cần nâng cấp => Copy
B3: Check lại server WHM Maxspeed (List account) thấy tồn tại gói, WHM Business account bị suspend
B4: Trỏ IP về IP gói Hosting Maxspeed và kiểm tra lần cuối

## Terminal
### Reload Hosting

Cách 1: cagefs -m <user>
Cách 2: Thao tác trên giao diện portal của khách hàng

### Check domlogs

File log của domain nằm tại:
```
Domain không có SSL: /var/log/apache2/domlogs/<domain>
Domain có SSL: /var/log/apache2/domlogs/<domain>-ssl_log
```

### Tìm một add-on domain đang thuộc user nào.

Dùng terminal

```
cat /etc/userdatadomains | grep "conheo.com"
abc.conheo.com:

khanhtest==root==sub==khanhtest.com==/home/khanhtest/abc.conheo.com==103.200.23
.68:80==103.200.23.68:443====0==
conheo.com.khanhtest.com:
khanhtest==root==sub==khanhtest.com==/home/khanhtest/conheo.com==103.200.23.68:
80==103.200.23.68:443====0==
conheo.com:
khanhtest==root==addon==conheo.com.khanhtest.com==/home/khanhtest/conheo.com==1
03.200.23.68:80==103.200.23.68:443====0==
```

Dùng UI

![image](https://github.com/user-attachments/assets/b2996baa-866b-43cd-a55f-1a75238ad137)

