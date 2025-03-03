## Chuẩn bị
- 1 VPS có cài docker, quản lý các container service bằng Portainer
- Tên miền, nếu triển khai local thì chỉnh file host (Linux: /etc/hosts, Windows: C:\Windows\System32\drivers\etc\hosts)
- Trỏ domain về IP của VPS

## Cài đặt

**- Update hệ thống:**

```
sudo apt update && sudo apt upgrade -y
```

**- Cài docker**

  - Cài đặt Docker vào thư viện apt

  ```
  # Add Docker's official GPG key:
  sudo apt-get update
  sudo apt-get install ca-certificates curl
  sudo install -m 0755 -d /etc/apt/keyrings
  sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
  sudo chmod a+r /etc/apt/keyrings/docker.asc

  # Add the repository to Apt sources:
  echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  sudo apt-get update
  ```

  - Cài gói Docker (bao gồm docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin)

  ``` 
  sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
  ```

  - Kiểm tra cài đặt

  ```
  docker -v
  docker-compose -v
  ```

**- Cài Portainer**

```
# Tạo volume cho Portainer

docker volume create portainer_data

# Cài đặt Portainer

docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:lts
```

Sau đó truy cập https://<ip>:9443 để hoàn tất cài đặt

![image](https://github.com/user-attachments/assets/54bd3605-5b18-4d3f-80cc-9ce50f6b444c)


**- Cài Nginx Proxy Manager**

Vào Portainer tạo stack mới >> Truy cập https://nginxproxymanager.com/setup/ để lấy file docker-compose.yml >> Copy và điều chỉnh các thông số cho phù hợp sau đó dán vào Portainer Stack

![image](https://github.com/user-attachments/assets/1c124a9e-4532-4744-815c-372f0dd951ea)

![image](https://github.com/user-attachments/assets/13559f49-1f62-41b2-ad8d-ab1e10bbd71a)

Kéo lên trên đặt tên cho Stack và cuộn xuống dưới bấm Deploy

Sau khi Deploy truy cập https://<ip>:81 với default admin@example.com và password là changeme

Đăng nhập thành công sẽ được hướng dẫn đổi tài khoản mặc định để đảm bảo bảo mật.


**- Cài 2 dịch vụ bất kỳ bằng Docker trong mục Stack giống khi cài đặt Nginx Proxy Manager (Demo là WikiJS và n8n)**

  - WikiJS sẽ chạy ở port 8080
  - n8n sẽ chạy ở port 5678


**- Cấu hình Nginx Proxy Manager**

  - SSL Certìicates >> Add SSL Certificate

  ![image](https://github.com/user-attachments/assets/4908c8cf-6eff-4382-b99a-748aa1840bd0)


  - Thêm các docker service vào nginx proxy hosts: Home >> Hosts >> Proxy Hosts >> Add Proxy Hosts
 
    - Nếu setup NAT Proxy Host để truy cập an toàn từ Public vào thì IP ghi địa chỉ local
    - Nếu setup các dịch vụ docker chung với Nginx thì ghi địa chỉ IP của VPS (không dùng được "127.0.0.1 hoặc localhost"
    - Tùy vào dịch vụ nếu có ssl thì dùng https, bật "Block common exploits" và "Websockets Support"
    - Tab SSL thì sử dụng SSL đã cài trước đó, bật "Force SSL", "HTTP/2 Support" và "HSTS enabled" >> Save
   
  ![image](https://github.com/user-attachments/assets/999d8923-1689-4ec1-ad3a-04804e930919)

- Kiểm tra kết quả

![image](https://github.com/user-attachments/assets/e8bdb5e2-a050-40f6-84c0-a6ff3cb0fa71)

![image](https://github.com/user-attachments/assets/ba86c7c1-5f58-42dd-b971-d02df40344fd)


