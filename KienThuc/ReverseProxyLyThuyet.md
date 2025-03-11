# Reverse Proxy là gì?

=> Là một loại server trung gian giữa máy chủ và các clients gửi tới các yêu cầu. Nó kiểm soát yêu cầu của các clients, nếu hợp lệ, sẽ luân chuyển đến các servers thích ứng ở backend

Ưu điểm lớn nhất của việc sử dụng Reverse proxy là khả năng quản lý tập trung. Nó giúp kiểm soát mọi requests do clients gửi lên các servers mà được bảo vệ. 

Công dụng:
- Che giấu sự tồn tại và các đặc điểm của các servers thực sự được dùng ở backend
- Có thể tạo kết nối https đến các máy chủ chỉ sử dụng http
- Cân bằng tải, chia đều các yêu cầu của các máy khách tới các servers
- Có thể nén nội dung, làm cho việc truy cập trở nên nhanh chóng
- Có thể được dùng như là một application firewall để chống đỡ các cuộc tấn công (như Tấn công từ chối dịch vụ) vào các ứng dụng web
- Cache các nội dung tĩnh giúp giảm tải máy chủ ở backend

[Nguồn](https://vi.wikipedia.org/wiki/Reverse_proxy#cite_note-apache-forward-reverse-1)

# APACHE khác gì so với NGINX

| APACHE | NGINX |
|---|---|
| APACHE là 1 web server	| NGINX ngoài khả năng làm web server còn có thể làm reverse proxy ([Mục 1](https://www.geeksforgeeks.org/difference-between-apache-and-nginx/))|
| APACHE không thể chịu tải tốt bằng NGINX khi có lượng truy cập lơn | NGINX có thể xử lý hơn 10000 kết nối đồng thời mà chỉ tiêu tốn khoảng 2.5MB bộ nhớ ([Nguồn](https://en.wikipedia.org/wiki/Nginx#HTTP_proxy_and_Web_server_features))|
| Apache có hiệu suất cung cấp static content thấp nginx | NGINX có hiệu suất cung cấp static content nhanh hơn APACHE gấp 2 lần do có thể xử lý nhiều kết nối đồng thời ([Mục 10](https://www.geeksforgeeks.org/difference-between-apache-and-nginx/)) |
| Không rõ | NGINX có thể dùng làm mail proxy ([Nguồn](https://en.wikipedia.org/wiki/Nginx?utm_source=chatgpt.com#Mail_proxy_features)) |
| APACHE có lợi thế hơn về việc thêm module ngoài do được cung cấp Dynamic Module từ rất lâu. | Vào năm 2016, NGINX mới bắt đầu hỗ trợ cho Dynamic Module. ([Nguồn](https://viblo.asia/p/tim-hieu-tong-quan-ve-nginx-63vKjOExZ2R#_5-so-sanh-nginx-va-apache-4)) |
| Có tính bảo mật kém hơn khi được so sánh với NGINX | Bảo mật tốt hơn do có codebase nhỏ hơn ([Mục 11](https://www.geeksforgeeks.org/difference-between-apache-and-nginx/))|
| Cấu hình phức tạp hơn NGINX | Cấu hình dễ hơn so với APACHE ([Mục 13](https://www.geeksforgeeks.org/difference-between-apache-and-nginx/)) |

# Khi nào chọn APACHE và khi nào chọn NGINX

## Chọn APACHE khi
- Triển khai hệ thống hosting, người dùng có thể chỉnh sửa để chạy theo source của họ thông qua .htaccess trong phân vùng hosting của họ
- Khi cần sự linh hoạt của các modul

## Chọn NGINX khi
- Cần xử lí nhiều nội dung tĩnh hơn
- Server có lưu lượng truy cập lớn

[Nguồn](https://cloudzone.vn/so-sanh-apache-va-nginx/#Khi_nao_chon_Apache_hay_Nginx)
