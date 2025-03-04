## Thực hiện allow/block port, allow ip trên window fw (Demo allow ssh tới windows server)

1. Cài OpenSSH server trên windows server 2022: 

- Start >> Settings >> Apps >> Optional features >> Add a feature >> OpenSSH server

![image](https://github.com/user-attachments/assets/73044b66-6a16-4379-9026-193b44ac66f2)

- Bật dịch vụ: Start >> services.msc >> Tìm "OpenSSH SSH Server" >> Startup Type: Automatic (Delayed Start) >> Start >> Apply

![image](https://github.com/user-attachments/assets/d0169808-4871-4074-a1b2-7c54a7dc68dc)


2. Allow port ssh (22): Start >> Windows Defender Firewall with Advanced Seurity >> Inbound Rules >> New Rule...

![image](https://github.com/user-attachments/assets/37dce92b-a7e5-4e46-8e12-81827a52c27e)

![image](https://github.com/user-attachments/assets/325fbd86-bdb0-4c02-a9a7-9c03f9de7e2d)

![image](https://github.com/user-attachments/assets/7f3b550b-bc0a-4992-8580-a1a7c07fa5ea)

![image](https://github.com/user-attachments/assets/2a3841f0-e303-460d-8cdf-d64112938f62)

![image](https://github.com/user-attachments/assets/ffff876e-9802-4706-b1a2-f27e1449eba8)

![image](https://github.com/user-attachments/assets/89c0c604-45bc-4e1a-8146-d414f3ef56b5)

![image](https://github.com/user-attachments/assets/9927621c-1bd9-4872-93d1-6a7a8fb9a124)

Check IP của Windows Server

![image](https://github.com/user-attachments/assets/fdc32893-04f5-46c7-b782-cfd91c61aff8)

Đã SSH vào Server thành công !


## Thực hiện giới hạn port, giới hạn ip trên window fw chỉ cho phép ip chỉ định truy cập

![image](https://github.com/user-attachments/assets/37dce92b-a7e5-4e46-8e12-81827a52c27e)

![image](https://github.com/user-attachments/assets/795c85f4-aeb6-4d8a-a14d-00dd7609d7b8)

![image](https://github.com/user-attachments/assets/58aa1414-5726-4729-bb00-2136141286f7)

![image](https://github.com/user-attachments/assets/1f0eea65-38e6-4c44-b667-a7977a0970b1)

![image](https://github.com/user-attachments/assets/cb6f0189-35cb-451b-87b2-3a213737a88d)

![image](https://github.com/user-attachments/assets/2583fb19-602d-41ee-a02d-a4a1fa9f46d1)

![image](https://github.com/user-attachments/assets/207a0a6c-51ea-4d31-9464-2d00a5b81c73)

![image](https://github.com/user-attachments/assets/ee70d4b9-ee3b-4a9c-b221-b94205585485)

![image](https://github.com/user-attachments/assets/eab303d4-2add-40c9-a519-50898c583566)


## Thực hành cài đặt

- Webserver IIS, trên Webserver IIS
  - Cài đặt website wordpress
  - Cài đặt plugin
  - Cài đặt SSL
 
- SQL Server: 2008, 2012, 2014, 2016, 2019, 2022 các phiên bản: Standard và Datacenter

