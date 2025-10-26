# bt2_weB

#Đề_Bài 
2. NỘI DUNG BÀI TẬP:

1 Cài Apache Web Server: Tắt IIS, cài Apache vào ổ D, cấu hình httpd.conf và vhosts.conf, tạo website fullname.com, trỏ domain trong file hosts.

2 Cài Node.js và Node-RED: Cài Node.js vào D:\nodejs, cài Node-RED bằng npm, dùng NSSM tạo service a1-nodered để chạy tự động.

3 Tạo CSDL SQL Server: Tạo cơ sở dữ liệu tùy ý, ghi nhớ thông tin kết nối (IP, user, pass, db, bảng).

4 Cài thư viện Node-RED: Truy cập http://localhost:1880, cài các node cần thiết (MSSQL, moment, telegrambot, v.v.), cấu hình adminAuth bằng mật khẩu mã hóa.

5 Tạo API Backend: Dùng các node http in → function → MSSQL → http response để truy vấn và trả JSON về client.

6 Tạo giao diện Front-End: Gồm index.html, fullname.js, fullname.css đặt trong D:\Apache24\fullname, gửi request đến API và hiển thị kết quả.

7 Nhận xét: Hiểu được cách cài đặt phần mềm, tạo API bằng Node-RED, và cơ chế frontend–backend hoạt động cùng nhau.

#Bài_Làm 

#1CàiApacheWebServer: 
Tắt IIS, cài Apache vào ổ D, cấu hình httpd.conf và vhosts.conf, tạo website fullname.com, trỏ domain trong file hosts.
IIS là web server mặc định của Windows, phải tắt để tránh xung đột cổng 80.

Mở CMD (Run as Administrator)

Gõ lệnh:iisreset /stop

,Nếu hiện thông báo IIS successfully stopped là OK.

<img width="469" height="297" alt="image" src="https://github.com/user-attachments/assets/165e9c75-4591-4ae8-bee7-430292bd6f5b" />

#2DowloadApacheServer
1 Vào trang: https://www.apachelounge.com/download/

2 Tải file Apache HTTP Server (Win64) — ví dụ: httpd-2.4.58-win64-VS17.zip

3 Giải nén vào thư mục:
 D:\Apache24

<img width="634" height="267" alt="image" src="https://github.com/user-attachments/assets/2704de66-978c-4de4-8335-95d3a56a35e0" />

 <img width="999" height="223" alt="image" src="https://github.com/user-attachments/assets/3a4dc039-bf16-4d8c-9b29-736bcdc72f43" />

 + Tạo thư mục chứa file
   "D:\Apache24\nguyentienthang"
   
   <img width="1020" height="230" alt="image" src="https://github.com/user-attachments/assets/5415fdc9-4873-4ee0-bc16-c0a69e2416f5" />
 D:\Apache24\conf\httpd.conf
DocumentRoot "D:/Apache24/htdocs"

<Directory "D:/Apache24/htdocs">

<img width="1424" height="617" alt="image" src="https://github.com/user-attachments/assets/1872b2e0-c912-4f21-98fd-8e14920f44e7" />

Bỏ dấu # dòng VirtualHost

<img width="846" height="507" alt="image" src="https://github.com/user-attachments/assets/c6de1888-e701-40aa-a117-57c7c71655c9" />
 sau đó tại D:Apache24\conf\extra\httpd-vhosts.conf.

