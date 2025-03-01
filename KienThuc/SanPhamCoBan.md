
## Các sản phẩm cơ bản

- Hosting: là một server cung cấp dịch vụ lưu trữ website cho nhiều khách hàng, mỗi khách hàng có thể truy cập website của mình thông qua domain (tên miền)

- Domain: phân giải thành địa chỉ IP để lấy nội dung website, resources cho người dùng cuối.

- VPS: là một hoặc nhiều máy chủ ảo được tạo ra dựa trên tài nguyên máy chủ thật

- SSL: là chữ ký số xác thực mã hóa đường truyền kết nối giữa người dùng đến máy chủ web

- Email doanh nghiệp: training sau

- Firewall chống DDoS: training sau

- Tối ưu tốc độ website: training sau


## Một số câu hỏi tìm hiểu

- Cách dùng linux command để tìm kiếm error log và debug log

```
find / -name "error.log"

find / -name "debug.log"

# Xem log bằng các lệnh như cat, tail, less, head + file"

# Ngoài ra tùy theo ứng dụng mà sẽ có cách lưu log khác nhau, ta dùng thêm google tra theo từ khóa "<tên phần mềm> log location"

# Đa số log của Linux được lưu ở /var/log/

# Xem log một dịch vụ cụ thể: journalctl -u <tên dịch vụ"

# Xem tất cả các nhật ký hệ thống: journalctl
```

- Các cờ trạng thái DNS

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


