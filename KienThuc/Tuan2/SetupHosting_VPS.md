## Setup hosting website
Chuẩn bị: mua tên miền, gói hosting phù hợp

Cài đặt
- Trỏ tên miền về IP hosting

![image](https://github.com/user-attachments/assets/5c70ad44-225c-4359-9c93-41a6e9202dce)


![image](https://github.com/user-attachments/assets/a54f18ca-dc99-4ceb-a929-4ba6d8e37f58)

- Truy cập File Manager trên cPanel vào thư mục public_html => Upload source code

![image](https://github.com/user-attachments/assets/b0d5bba3-b5a5-41e9-bc35-3032f36ad0fa)

- Kiểm tra website

![image](https://github.com/user-attachments/assets/3b19b677-b01c-414c-bed6-983b61f0daad)


## Setup VPS
Chuẩn bị: lựa chọn các gói VPS và hệ điều hành của VPS phù hợp với nhu cầu

Cài đặt:
- Kiểm tra các thông số của VPS:

  - Thông tin OS:
    
  ```
  root@14-225-220-231:~# cat /etc/os-release
  PRETTY_NAME="Ubuntu 22.04.5 LTS"
  NAME="Ubuntu"
  VERSION_ID="22.04"
  VERSION="22.04.5 LTS (Jammy Jellyfish)"
  VERSION_CODENAME=jammy
  ID=ubuntu
  ID_LIKE=debian
  HOME_URL="https://www.ubuntu.com/"
  SUPPORT_URL="https://help.ubuntu.com/"
  BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
  PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
  UBUNTU_CODENAME=jammy
  ```

  - Dung lượng disk
  ```
  root@14-225-220-231:~# df -h
  Filesystem      Size  Used Avail Use% Mounted on
  tmpfs           392M   41M  351M  11% /run
  /dev/sda1        39G   11G   29G  27% /
  tmpfs           2.0G     0  2.0G   0% /dev/shm
  tmpfs           5.0M     0  5.0M   0% /run/lock
  /dev/loop4      1.6G  156K  1.5G   1% /tmp
  /dev/sda15      105M  6.1M   99M   6% /boot/efi
  tmpfs           392M  4.0K  392M   1% /run/user/0
  ```

  - Kiểm tra phiên bản nhân Linux
  ```
  root@14-225-220-231:~# uname -a
  Linux 14-225-220-231.cprapid.com 5.15.0-133-generic #144-Ubuntu SMP Fri Feb 7 20:47:38 UTC 2025 x86_64 x86_64 x86_64 GNU/Linux
  ```

  - Kiểm tra CPU
  ```
  cat /proc/cpuinfo
  ```

  - Kiểm tra tốc độ đọc ghi (I/O) của ổ cứng: Sử dụng công cụ FiO và IOPing.

- Update và upgrade OS:

```
sudo apt update && sudo apt upgrade -y
```

- Cài đặt một số các loại Panel để quản lý VPS dễ dàng hơn tùy theo nhu cầu:

  - Miễn phí: aâPanel, CyberPanel, VirtualMin, FastPanel, VestaCP, HestiaCP, CloudPanel,...
  - Có phí: cPanel, DirectAdmin, Plesk,...

