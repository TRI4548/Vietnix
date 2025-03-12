
# SSL

#### SSL là gì ?

SSL (Secure Socket Layer) là một tiêu chuẩn công nghệ bảo mật đường truyền giữa trình duyệt và web server
=> Đảm bảo không bị đọc trộm, cung cấp tính toàn vẹn dữ liệu

#### Cách thức hoạt động:

  B1 Xin phép kết nối an toàn
  B2 Chứng thực máy chủ
  B3 Xác thực máy khách (nếu cần)
  B4 Chia sẻ khóa bí mật
  B5 Bảo mật kết nối
  B6 Truyền dữ liệu an toàn
 
#### Các loại chứng chỉ: DV, OV, EV, ngoài ra còn có Wildcard SSL, Subject Alternative Names – SANs SSL

#### Có bao nhiêu cách chứng thực SSL ? 2 cách

 - One-way: Máy chủ được yêu cầu trình bày chứng chỉ cho máy khách nhưng máy khách không bắt buộc phải trình bày chứng chỉ cho máy chủ
 - Two-way: Máy chủ và máy khách đều phải xác thực chứng chỉ của nhau để chứng mình danh tính

#### CSR file dùng làm gì trong quá trình tạo SSL

CSR file dùng làm gì trong quá trình tạo SSL? là 1 đoạn text chứa thông tin của chủ sở hữu tên miền được mã hóa. Thông tin này được gửi đến nhà cung cấp dịch vụ SSL để xác nhận.

#### Sử dụng OpenSSL để gen file CSR sau đó request SSL cho domain tech.training.vietnix.tech

#### Pem file là gì ?

File PEM (Privacy Enhanced Mail) là một định dạng tệp được sử dụng để lưu trữ và truyền tải các chứng chỉ, khóa riêng tư, và các dữ liệu bảo mật khác trong các hệ thống mã hóa, được mã hóa bằng base64
[Nguồn](https://tenten.vn/tin-tuc/file-pem-la-gi/)

#### Private key ssl là gì ?

Là file mã hoá được sinh ra cùng lúc khi tạo CSR.

#### PFX file là gì ? Cách chuyển từ file crt file sang PFX file.

PFX file (Personal Exchange Information) : là một file chữ ký số chứa bao gồm public và private key được sử dụng để chứng thực cho IIS trên Windows. 
[Cách convert qua file pfx](https://www.sslshopper.com/ssl-converter.html
(https://kb.pavietnam.vn/tao-file-pfx-de-import-vao-iis.html)

# Domain

#### Domain là gì ?

Domain, hay còn được gọi là tên miền, chính là địa chỉ website của bạn trên Internet.

#### Các trạng thái của domain

- Trạng thái tên miền tại Đơn vị Cấp phát tên miền (Registry)

| Trạng thái | Ý nghĩa |
|---|---|
| OK / active	| Trạng thái thể hiện tên miền hoạt động bình thường sau khi đăng ký. |
| addPeriod | Đây là trạng thái sau khi tên miền mới vừa được đăng ký. |
| autoRenewPeriod | Thời gian đăng ký tự động gia hạn tên miền. Trạng thái này cho phép nhà đăng ký hủy việc gia hạn (duy trì) nhưng phải trả một khoản phí cho nhà cung cấp. |
| inactive | Tên miền đã được đăng ký nhưng Name Server chưa thể liên kết với tên miền của bạn. |
| pendingCreate | Đang chờ Đăng ký |
| pendingDelete | Tên miền hết hạn đăng ký. Chuẩn bị xóa. |
| pendingRenew | Đang chờ Gia hạn |
| pendingRestore | Một tên miền đã hết hạn đang được chờ khôi phục (về trạng thái Active). Nếu trong thời gian này NĐK không thực hiện yêu cầu khôi phục nào, tên miền sẽ trở về trạng thái redemptionPeriod. |
| pendingTransfer | Đang chờ Chuyển đổi nhà đăng ký. |
| pendingUpdate | Đang chờ Cập nhật |
| redemptionPeriod | Tên miền đã hết hạn và rơi vào trạng thái cần đóng phí chuộc nếu muốn tiếp tục sử dụng. Thời gian này thường sẽ kéo dài 30 ngày. |
| renewPeriod | Tên miền được gia hạn |
| serverDeleteProhibited |	Trạng thái ngăn tên miền bị xóa. |
| serverHold | Tên miền không được kích hoạt trong DNS |
| serverRenewProhibited |	Trạng thái không thể được gia hạn. Nó là trạng thái không thông dụng vì nó có hiệu lực trong quá trình tranh chấp pháp lý. |
| serverTransferProhibited |	Trạng thái không cho phép transfer tên miền. |
| serverUpdateProhibited |	Trạng thái không cho phép cập nhật tên miền |
| transferPeriod | Trạng thái cho phép sau khi tranfer tên miền thành thông thì nhà đăng ký mới có thể yêu cầu nhà cung cấp xóa tên miền |


- Trạng thái tên miền tại Đơn vị Quản lý (Nhà đăng ký) tên miền (Registrar)

| Trạng thái |	Ý nghĩa |
|---|---|
| clientDeleteProhibited |	Trạng thái không cho phép xóa tên miền (Cấm hủy domain) |
| clientHold |	Trạng thái suspend tên miền (Tạm ngừng tên miền) |
| clientRenewProhibited |	Trạng thái không cho phép gia hạn tên miền. (Cấm Gia hạn tên miền) |
| clientTransferProhibited |	Trạng thái không cho phép transfer tên miền (Cấm chuyển đổi nhà đăng ký) |
| clientUpdateProhibited |	Trạng thái không cho phép cập nhật thông tin tên miền (Cấm cập nhật thông tin) |


#### Subdomain là gì?

Là phần mở rộng, phần bổ sung xuất hiện trước của tên miền chính. Subdomain là một phần tách ra từ domain và hoạt động như một website bình thường

#### Virtual Hosts là gì?

Là một tính năng trong web server và cũng là một phương thức lưu trữ, cho phép nhiều trang web hoặc tên miền hoạt động trên cùng một máy chủ vật lý hoặc một địa chỉ IP duy nhất

# Mail Server

#### Tìm hiểu MX Record

MX Record hay còn gọi là bản ghi MX (Mail Exchange) là một loại bản ghi DNS giúp điều hướng email đến đúng máy chủ email
[Nguồn](https://vinahost.vn/mx-record-la-gi/)

#### Tìm hiểu DKIM, SPF, PTR ([Nguồn](https://vietnix.vn/cau-hinh-dkim-va-spf/#spf-la-gi))

  - DKIM là viết tắt của DomainKeys Identified Mail – một phương thức giúp xác nhận Email thông qua chữ ký số giúp tránh email giả mạo.

  - SPF (Sender Policy Framework) là một cơ chế xác thực email giúp phát hiện và ngăn chặn email giả mạo.
 
  - PTR (Pointer Record) là một loại bản ghi trong hệ thống DNS được sử dụng để ánh xạ một địa chỉ IP (IPv4 hoặc IPv6) thành một tên miền. ([Nguồn](https://helpdesk.inet.vn/kien-thuc/ban-ghi-ptr-la-gi))


# DNS

#### DNS là gì ? [Nguồn](https://vietnix.vn/dns-la-gi/)

DNS viết tắt của Domain Name System có nghĩa là hệ thống phân giải tên miền. DNS là hệ thống cho phép thiết lập tương ứng giữa địa chỉ IP và tên miền trên Internet.

#### Các loại record DNS

   - A: phân giải tên miền thành IPv4
   - AAAA: phân giải tên miền thành IPv6
   - CNAME: Là một bản ghi tên quy chuẩn (Canonical Name Record). Đây là một dạng bản ghi tài nguyên trong hệ thống tên miền.
   - MX: trỏ tên miền đến Mail Server
   - TXT: chứa các thông tin định dạng văn bản domain
   - SRV: dùng để xác định chính xác dịch vụ nào đang chạy Port nào
   - NS: chỉ định Name Server cho từng tên miền phụ và bên cạnh đó có thể tạo tên Name Server, TTL hay host mới.

#### Cách phân giải địa chỉ DNS

![image](https://github.com/user-attachments/assets/112db941-bd11-47bd-8802-06e0b15aea97)
