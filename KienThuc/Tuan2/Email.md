## Các lưu ý:
- IP VN đều bị blacklist nên sẽ không gửi được mail tới đích, nếu được thì vào mục Spam
=> Khắc phục: gửi qua mail relay: là 1 loại proxy cho mail server có kèm theo filter và các chức năng khác

- Domain phải sạch (.site, .xyz sẽ không uy tín bằng .com, .org)
- Nội dung email phải sạch, không được chứa nội dung nhạy cảm hoặc các từ ngữ dễ bị cho vào spam
- Mail forward vẫn được lưu tại server mail forward
- SpamAssassin không dùng do chức năng chặn chưa phù hợp với nhu cầu
- Dúng công cụ [mail-tester](https://www.mail-tester.com/) để check mail gửi đi có bị blacklist hay không (có kèm số điểm)

- Các lỗi thường gặp:
  - Thiếu DNS record (DKIM, SPF **nhớ ktra kĩ value**, PTR)
  - Dung lượng bị full
  - Nội dung mail bị dính blacklist
  - Domain bị block
  - Email Relay bị lỗi
  - Cấu hình code gửi mail của khách bị lỗi (hiếm)
  - Outlook Client bị lỗi
  - Gửi nhận được nhưng chậm (thường do đường truyền quốc tế có sự cố), hoặc thời gian đồng bộ email server và client bị lâu, do bộ filter ở server nhận mail cấu hình filter quá gắt nên bị đánh spam hoặc bị discard


## Email Hosting
- Email Accounts: tạo và quản lý các email của hosting
- Forwarders: cấu hình chuyển tiếp email đến địa chỉ nhận email khác
- Email Routing: Chỉ chọn tùy chọn Local Mail Exchanger để nhận thư trên hosting
- Autoresponders: Cấu hình trả lời email tự động
- Default Address: Cấu hình nhận thư khi người gửi gửi đến một tài khoản không có trên mail server của hosting
- Mailing Lists: Sử dụng một địa chỉ duy nhất để đại diện một nhóm nhiều tài khoản email, khi email đại diện nhận được thư, nó gửi thư đó đến toàn bộ người trong nhóm đó
- Track Delivery: Xem lại một lộ trình gửi email. Nó hữu ích nếu cần xác định các vấn đề với gửi email
- Global Email Filters: tạo bộ lọc gửi mail cho toàn bộ tài khoản mail trong hosting.
- Email Filter: tạo bộ lọc gửi mail cho tài khoản mail trong hosting được chọn cụ thể
- Email Deliverability: tạo các bản record DKIM, SPF, DMARC để người dùng xác thực để khi gửi mail giảm thiểu tình trạng bị vào Spam
- Address Importer: Import một lúc nhiều tài khoản email có sẵn vào Email Account hoặc Forwarders
- Spam Filters: Cấu hình Apache SpamAssassin để chuyển các mail bị đánh dấu là spam vào thư mục spam hoặc xóa (không khuyến khích) luôn các email đó
- Encryption: mã hóa email
- BoxTrapper: cấu hình để Xác thực người gửi, tạo Blacklist & Whitelist, Xử lý thư rác và Quản lý danh sách liên hệ.
- Email Disk Usage: Thống kê disk của từng email.
