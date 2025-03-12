## ping/hping3 ping đến domain vietnix.vn

![image](https://github.com/user-attachments/assets/62838ddb-a478-43be-86d3-2a4580a24e9a)

Giải thích: 
- Vietnix.vn có IP là 103.90.224.90
- Số lượng byte gửi và nhận lại là 64 byte
- icmp_seq là số thứ tự gói tin

TTL (time to live): là thời gian packet được lưu hành, khi đi qua mỗi router, TTL sẽ trừ 1. Khi TTL = 0, gói tin sẽ bị loại bỏ và một thông báo ICMP sẽ được gửi lại cho người gửi

time: thời gian phản hồi trung bình hay độ  giữa máy gửi lệnh ping và máy nhận

### So sánh hping3 và ping

- Ping: Chỉ sử dụng giao thức ICMP
- hping3: Có thể gửi nhiều loại gói tin khác nhau (TCP, UDP, ICMP, RAW-IP)

![image](https://github.com/user-attachments/assets/9d84cc03-9151-4165-a971-8dcdd01748ec)


## SSH

- SSH dùng password

![image](https://github.com/user-attachments/assets/22282248-e551-4171-81f9-0fae4f3f474d)

- SSH dùng key

  - B1: Tạo RSA pair key
  - B2: Lưu key
  - B3: Sao chép đến server cần xác thực thông qua key
  - B4: Login server => vô hiệu hóa root login và cấu hình chỉ cho login thông qua key

- Đổi port SSH:
  - Chỉnh file /etc/ssh/sshd_config, loại bỏ comment và khai báo port muốn sử dụng => sau đó Save lại

  ![image](https://github.com/user-attachments/assets/9e4bab8b-c56c-4011-948e-99169f2cc148)

  - Restart dịch vụ: systemctl restart sshd
 
  - Khi sử dụng truy cập: ssh root@14.225.230.231 -p 2222
 

## SCP command: dùng để copy nội dung tử máy local đến máy remote hoặc ngược lại

- scp 1 file: scp path/to/local_file remote_host:path/to/remote_file
- scp 1 folder (copy từ máy remote về máy local): scp -r remote_host:path/to/remote_directory path/to/local_directory

## rsync command: để sao chép và đồng bộ hóa tệp tin hoặc thư mục giữa các vị trí khác nhau, có thể là trên cùng một máy hoặc giữa các máy khác nhau

- rsync file: rsync path/to/source path/to/destination

- rsync folder: rsync -r|--recursive path/to/source path/to/destination

**- rsync increamental**

## cat command: tạo một hoặc nhiều file, xem nội dung file, nối file và chuyển hướng đầu ra trong terminal hoặc file

- cat nội dung 1 file: cat path/to/file

- cat dòng thứ <n> trong file: cat text.txt | head -n 5 | tail -n 1
  => Kết hợp với lệnh head để lấy 5 dòng đầu tiên sau khi cat, sau đó lấy dòng cuối cùng bằng lệnh tail

- cat nhiều dòng vào 1 file bằng EOF: cat >> ten_file << EOF

![image](https://github.com/user-attachments/assets/b5cfe8df-3c6e-4df1-9115-6f2d41d04580)


## echo command: in text

- Dùng echo để chèn thêm 1 dòng vào cuối file: echo "Hello World" >> file.txt

- Dùng echo để overwirte nội dung của file: echo "Hello World" > file.txt

## tail/head command: xem số dòng phía cuối/đầu trang

- tail /etc/passwd: xem 10 dòng cuối của file

- head /etc/passwd: xem 10 dòng đầu của file

- tail -f /etc/passwd: xem  10 dòng cuối của file và khi có dòng mới add vào cũng sẽ được hiển thị theo thời gian thực

## sed command: Dùng sed để find and replace một string trong file

- Dùng sed để find and replace một string trong file: sed 's/Mango/Kiwi/' text.txt

- Dùng sed để find and replace toàn bộ string trong file: 's/Kiwi/Orange/g' text.txt

## traceroute/tracert command: Sau khi traceroute xong giải thích chi tiết kết quả trả về

![image](https://github.com/user-attachments/assets/73a32a5d-4666-40dc-bea1-2c60404f8ac0)

Giải thích: lộ trình của gói tin từ máy local đến vietnix.vn đi qua 11 hop, maximum cho quá trình này là 30 hop và kích thước gói là 60 byte
- Hop 1: ra khỏi mạng nội bộ
- Hop 2: đi đến router Viettel có IP là 125.235.251.181 với tgian trung bình là 9ms
- Hop 3: đi đến router Viettel có IP là 10.255.38.229 với tgian trung bình là 10ms
- Hop 4: thiết bị không phản hồi, có thể vì thiết bị này được cấu hình để không gửi packet ICMP hoặc thời gian phản hồi quá chậm.
- Hop 5: đi đến router cuối cùng của Viettel có IP là 27.68.236.240 với tgian trung bình là 9ms
- Hop 6: đi đến router của VNPT có IP là 203.113.187.98 với tgian trung bình là 10ms
- Hop 7: đi đến router của VNPT có IP là 113.171.45.66 với tgian trung bình là 6ms
- Hop 8: đi đến router của VNPT có IP là 113.171.49.2 với tgian trung bình là 7ms
- Hop 9: đi đến router có IP là 172.16.34.178 với tgian trung bình là 6ms
- Hop 10: đi đến router có IP là 172.18.19.21 với tgian trung bình là 5ms
- Hop 11: đi đến trang web của Vietnix với IP là 103.90.224.90 với tgian trung bình là 8ms


## netstat command: hiển thị các thông tin liên quan đến kết nối mạng

- Hiển thị địa chỉ IP thay vì tên miền: netstat --numeric-hosts

- Hiển thị số cổng mạng đang hoạt động dưới dạng số thay vì tên dịch vụ: netstat --numeric-ports

- Hiển thị tên / PID của process: netstat -p, --programs

- Chỉ hiển thị các kết nối tcp: netstat --tcp

- Chỉ hiển thị các kết nối udp: netstat --udp

## sort command: sắp xếp nội dung hiển thị

- sort theo thứ tự tăng dần:   sort path/to/file

- sort theo thứ tự giảm dần:   sort --reverse path/to/file

- sort theo column: -k:
  - vd: ls -l | sort -nk5
 
  ![image](https://github.com/user-attachments/assets/16d12a34-128c-4be9-bbd1-7e72898642c9)


## uniq command: xuất ra 1 dòng khi có nhiều dòng giống nhau từ input hoặc từ 1 file

- lọc ra các dòng lặp lại trong một file:    sort path/to/file | uniq -d

- lọc ra các dòng lặp lại trong file và đếm số lượng các dòng lặp lại:   sort path/to/file | uniq -dc


## wc command: đếm số từ, dòng, byte

- Đếm số dòng trong file: wc --lines path/to/file

- Đếm số kí tự trong file: wc --words path/to/file


## Phân quyền

- Bằng số: chmod 755 text.text
  - read || r = 4
  - write || w = 2
  - execute || x = 1

- Bằng chữ: chmod u=rwx,g=rw,o=r text.txt
  - u = user
  - g = group
  - o = other
 
- Đổi owner user: sudo chown <username> <filename>

- Đổi group owner: sudo chgrp <groupname> <filename>


## find command: tìm kiếm

- find các file có đuôi .log: find root_path -name '*.log'

- find các folder có tên abc: find root_path -type d -iname '*abc*'

- find các file có tên abc: find root_path -name 'abc'

- find các file có tên abc và thực hiện phần quyền read only cho file: find / -type f -name "abc" | xarg chmod


## cp command: sao chép

- cp file: cp path/to/source_file.ext path/to/target_file.ext

- cp folder: cp -R path/to/source_directory path/to/target_directory

## mv command: di chuyển hoặc đổi tên

- mv file, folder: mv path/to/source path/to/existing_directory

- Đổi tên file: mv <old_file_name> <new_file_name>

## cut command: in ra 1 hoặc 1 dãy kí tự được đánh dấu

- cut kí tự thứ <n> trong string:  
  - vd: echo “Hello World” | cut -c 1  => KQ: H

- cut từ kí tự thứ <n> trở về trước trong string
  - vd: echo "Hello World" | cut -c -6 => KQ: Hello

- cut từ kí tự thứ <n> trở về sau trong string
  - vd: echo "Hello World" | cut -c 6- => KQ: o World
 

## dig command: công cụ DNS lookup

Dùng Dig command để kiểm tra resolv record A, MX, NS
- Record A: dig a tringuyen.space

  ![image](https://github.com/user-attachments/assets/daae2f13-f7fc-443b-984a-ad4967041eab)

- Record MX: dig mx tringuyen.space

  ![image](https://github.com/user-attachments/assets/2b727110-2060-4dc1-bbc8-6d825023fc6d)

- Record NS: dig ns tringuyen.space

  ![image](https://github.com/user-attachments/assets/37db9508-9566-4063-9581-41898b0c9bb0)


## tar/zip/unzip command: nén/giải nén tập tin/thư mục

- Nén file tar.gz 1 thư mục: tar czf path/to/target.tar.gz –directory=path/to/directory

- Giải nén file tar.gz: tar xf path/to/source.tar[.gz|.bz2|.xz] –directory=path/to/directory

- Nén file zip (nhiều file hoặc thư mục): zip -r path/to/compressed.zip path/to/file_or_directory1 path/to/file_or_directory2 …

- Giải nén file zip: unzip path/to/archive1.zip path/to/archive.zip2

## mount/umount command

- Add thêm một ổ cứng sdb ~ 5gb

- Kiểm tra được có bao nhiêu ổ cứng trên máy chủ

- Mount ổ cứng vào /mnt/test

- Umount /mnt/test

## Sym link và Hard link

- Định nghĩ Sym Link: Là liên kết không dùng đến inode entry mà chỉ đơn thuần là một shortcut. Nó sẽ tạo ra một inode mới và nội dung của inode này trỏ đến tên tập tin gốc.

- Định nghĩ Hard Link: Là một liên kết trong cùng hệ thống tập tin với 2 inode entry tương ứng trỏ đến cùng một nội dung vật lý (cùng số inode vì chúng trỏ đến cùng dữ liệu).

- Ví dụ về Sym Link và Hard Link:
  - Hard Link: giả sử có tệp file1.txt và file2.txt trỏ đến file1.txt => nếu thay đổi nội dung của file1 thì file2 cũng thay đổi theo; nếu xóa file1 thì file2 vẫn còn dữ liệu
  - Sym Link: lấy vd giống Hard Link, thì file2 là shortcut của file1 => nếu xóa file1 thì liên kết sẽ bị hỏng
 
## ls command: liệt kê

- Liệt kê danh sách file/thư mục: ls

- Liệt kê danh sách file/thư mục và thuộc tính: ls -l

- Show file ẩn: ls -la


## ps command: quản lý tiến trình

- show tất cả tiến trình đang chạy: ps aux

- kill tiến trình: kill -9|KILL process_id

## top command: quản lý resource của server theo thời gian thực

- Kiểm tra tài nguyên cpu đang sử dụng của một vài process đang chạy

  ![image](https://github.com/user-attachments/assets/efa702b6-4098-416e-9531-dcc69dfd5154)

- Giải thích về Load average, us, sy, ni, id, wa, hi, si, st, zombie process, sleeping process
  - Load average (1, 5, 15 phút): Trung bình tải hiển thị thời gian load hệ thống trong 1 phút, 5 phút và 15 phút cuối.

  - us (user space): phần trăm do tiến trình của người dùng (non root) sử dụng

  - sy (system space): phần trăm do tiến trình của hệ thống (root) sử dụng

  - ni (nice): phần trăm do các tiến trình có mức độ ưu tiên thấp sử dụng

  - id (idle): phần trăm CPU đang rảnh

  - wa (I/O wait): phần trăm CPU để đợi trong khi các tiến trình I/O đang xử lý

  - hi (hardware interrupt): phần trăm để xử lý gián đoạn phần cứng

  - si (software interrupt): phần trăm để xử lý gián đoạn phần mềm

  - st (steal time): phần trăm do máy ảo sử dụng

## free command: quản lý RAM của server

![image](https://github.com/user-attachments/assets/c75bb356-5987-4b07-8d44-f92790326050)

- Giải thích ram used, free, shared, buff/cache, free

  - used: lượng ram đã sử dụng
  - free: lượng ram chưa còn trống
  - shared: là tổng số bộ nhớ được sử dụng bởi các tiến trình khác nhau trong hệ thống, chia sẻ với tiến trình hiện tại
  - buff/cache: là tổng số bộ nhớ được sử dụng bởi bộ đệm và bộ nhớ cache. Bộ nhớ cache được sử dụng để lưu trữ các tài nguyên được sử dụng thường xuyên trong bộ nhớ để tăng tốc độ truy cập đến chúng
  - available: là tổng số bộ nhớ có thể sử dụng. Nó được tính bằng cách lấy tổng số bộ nhớ chưa sử dụng và thêm bộ nhớ được sử dụng bởi bộ đệm và bộ nhớ cache
  - swap: là tổng số bộ nhớ trên đĩa cứng được sử dụng như bộ nhớ phụ khi bộ nhớ RAM đã đầy
 
- df command: Xem tổng quan dung lượng đã sử dụng

Xem dung lượng disk: df -h

![image](https://github.com/user-attachments/assets/229245fb-ca0a-4cbf-9414-387d2e3846fc)


Phân vùng / là gì? Đây là phân vùng root, là nơi quan trong nhất, chứa các thư mục hệ thống
