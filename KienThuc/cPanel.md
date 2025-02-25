
## cPanel:
### Files
- File Manager: Upload file, xóa, sửa file, nén, giải nén. Ngoài ra để hiển thị file ẩn (.htaccess, .env...).

- Directory Privacy: Cài đặt user/pass cho các thư mục trên cPanel → Tương tự htpasswd

- Disk Usage: Xem kích thước tất cả các file

- Web Disk: một phương thức giống ftp nhưng an toàn hơn, hỗ trợ giao thức webdav để truyền tải.

- FTP account: tạo, quản lý tài khoản ftp

- Backup & Backup Wizard: sao lưu và phục hồi toàn bộ hoặc một phần (Home Directory | Database | Email Forwarders | Email Filters) => Tuy nhiên không sử dụng vì có hạn chế, thay vào đó dùng JetBackup 5

- File and Directory Restoration: => Không sử dụng

- JetBackup 5: Backup và Restore toàn bộ, hoặc từng cái nhỏ hơn, chi tiết hơn Backup & Backup Wizard

### Databases
- phpMyAdmin: Đăng nhập phpMyAdmin, tài khoản login là tài khoản MySQL

- Database Wizard: hướng dẫn người dùng tạo database theo các bước (tạo database -> tạo người dùng -> gán người dùng vào database -> grant các quyền)

- Manage My Databases: quản lý database từng bước đơn lẻ

- Remote Database Access: quản lý truy cập từ xa đến database

### Domains
- Wordpress Management: quản lý, cài đặt tự động Wordpress có bao gồm các theme và plugin

- Site publisher & site builder: hỗ trợ người dùng cài đặt các mẫu website tĩnh

- Domains: quản lý các tên miền trong hosting của người dùng, có thể tạo thêm alias, add-on, sub domain (không giới hạn tạo các alias, sub domain của primary hosting domain)

- Redirects: quản lý các chuyển hướng domain

- Zone Editor: Sau khi trỏ NS về Hosting thì có thể điều chỉnh các record ở đây

### Metrics
- Visitors: quản lý các kết nối đến website (IP truy cập, URI nào đã xem, thời gian,...)

- Resource Usage: quản lý tài nguyên mà website đã sử dụng

- Raw Access: xem file log xuất ra mà chưa qua định dạng

### Security
- SSH Access: tạo key ssh để truy cập một cách an toàn hơn thay vì dùng password

- IP Blocker: khai báo các IP để chặn truy cập trên toàn bộ domain của hosting của user

- SSL/TLS & SSL/TLS status: tạo và quản lý trạng thái SSL

- Hotlink Protection: chặn website khác dẫn link từ site của mình giúp giảm băng thông không cần thiết bị lấy đi từ site khác
