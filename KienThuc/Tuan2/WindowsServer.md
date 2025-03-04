## Thực hiện allow/block port, allow ip trên window fw (Demo allow ssh tới windows server)

1. Cài OpenSSH server trên windows server 2022: 

- Start >> Settings >> Apps >> Optional features >> Add a feature >> OpenSSH server

![image](https://github.com/user-attachments/assets/73044b66-6a16-4379-9026-193b44ac66f2)

- Bật dịch vụ: Start >> services.msc >> Tìm "OpenSSH SSH Server" >> Startup Type: Automatic (Delayed Start) >> Start >> Apply

![image](https://github.com/user-attachments/assets/d0169808-4871-4074-a1b2-7c54a7dc68dc)


2. Allow/block port ssh (22): Start >> Windows Defender Firewall with Advanced Seurity >> Inbound Rules >> New Rule...

![image](https://github.com/user-attachments/assets/37dce92b-a7e5-4e46-8e12-81827a52c27e)

![image](https://github.com/user-attachments/assets/325fbd86-bdb0-4c02-a9a7-9c03f9de7e2d)

![image](https://github.com/user-attachments/assets/7f3b550b-bc0a-4992-8580-a1a7c07fa5ea)

![image](https://github.com/user-attachments/assets/2a3841f0-e303-460d-8cdf-d64112938f62)

Nếu Block connection thì chọn option thứ 3

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

- Webserver IIS

![image](https://github.com/user-attachments/assets/14cf34fb-ff75-4757-842f-ddea095ab6c8)

![image](https://github.com/user-attachments/assets/1de98a3d-6f26-45bc-99ee-c74fe0885fe6)

![image](https://github.com/user-attachments/assets/310987bb-72d6-4e00-b7a2-3bf1de3a877d)

![image](https://github.com/user-attachments/assets/4e98f692-e4f2-4eb8-9613-ffa453ff861c)

![image](https://github.com/user-attachments/assets/4c4bdafe-cd89-4843-aec9-be708f9b5131)

![image](https://github.com/user-attachments/assets/409553ed-d6ff-4b97-9f78-76416633dba2)

![image](https://github.com/user-attachments/assets/be66dbf4-ba57-4a8d-9e66-de35eef49c59)

![image](https://github.com/user-attachments/assets/028a1b95-0702-49c5-a4ea-17a21909f14a)

![image](https://github.com/user-attachments/assets/3d229aef-bdfd-400a-951d-39adbbe7e8c4)

![image](https://github.com/user-attachments/assets/c6fb53fe-3435-409e-b963-8e868533ef71)

![image](https://github.com/user-attachments/assets/bf95444b-af39-41f9-ae08-1fde6f5c8b81)


- Trên Webserver IIS
  - Cài đặt website wordpress
    - Cài đặt PHP và PHP Manager cho IIS
   
      ![image](https://github.com/user-attachments/assets/f751706a-88ed-4b97-bd05-aa6d71237d5c)
   
      ![image](https://github.com/user-attachments/assets/8e16a624-5802-4194-9dfd-d1062041f20b)

      ![image](https://github.com/user-attachments/assets/5f8ea9ca-58b3-49b0-8b63-28a6fbf5991a)

      ![image](https://github.com/user-attachments/assets/6eb106d2-e540-4414-b394-ff3987031b04)

      ![image](https://github.com/user-attachments/assets/b9ee9db5-cb06-46f1-bbeb-f4c259b7175a)

      Cài đặt hoàn tất MySQL, trong quá trình cài đặt sẽ cần cài thêm Microsoft Visual C++ 2019 Redistributable Package (x64)

      ![image](https://github.com/user-attachments/assets/34d08e3d-98b1-43ba-a637-c9b92d7b949e)

      ![image](https://github.com/user-attachments/assets/42cf2da4-078e-4d89-87ad-66f5a67637f5)

      ```
      CREATE DATABASE wp_tringuyen DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
      CREATE USER 'wp_tringuyen'@'%' IDENTIFIED WITH mysql_native_password BY 'password';
      GRANT ALL ON wp_tringuyen.* TO 'wp_tringuyen'@'%';
      FLUSH PRIVILEGES;
      EXIT;
      ```

      ![image](https://github.com/user-attachments/assets/846134fd-1e2a-4d36-adf8-96cff6df5a6b)

      ![image](https://github.com/user-attachments/assets/3f4556b7-8695-4459-9ea3-38fb35138aba)

      ![image](https://github.com/user-attachments/assets/0204dca2-cc4c-4b40-8351-bbf1b650d03d)

      ![image](https://github.com/user-attachments/assets/a32e7aaa-87f0-4bf5-aec5-258fc98df539)

      ![image](https://github.com/user-attachments/assets/4f9f7e1e-5658-47a0-9ae3-8585c1f6674d)

      ![image](https://github.com/user-attachments/assets/c910244a-05f6-44fd-a424-2dc426c93664)


  - Cài đặt plugin: WordPress Home >> Plugin >> Add new plugin hoặc đường dẫn: docroot/wp-content/plugins
  - Cài đặt SSL
    - Chuẩn bị file cert định dạng .pfx, nếu đã có file .pem thì có thể dùng tool để chuyển đổi
    - Import vảo IIS: IIS Manager >> Server Certificates >> Import

    ![image](https://github.com/user-attachments/assets/dc63eb12-df07-4595-9c45-d2b92988e8f4)

    - Cấu hình website với SSL: IIS Manager >> Site cần cấu hình >> Edit Binding...
   
    ![image](https://github.com/user-attachments/assets/c8ecfc93-0f31-40d5-9c96-7f4a45a02a88)

 
- SQL Server: 2008, 2012, 2014, 2016, 2019, 2022 các phiên bản: Standard và Datacenter

