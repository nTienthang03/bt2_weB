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
 thêm 
 
 <VirtualHost *:80>
    ServerAdmin admin@nguyentienthang.com
    DocumentRoot "D:/Apache24/nguyentienthang"
    ServerName nguyentienthang.com
    ErrorLog "logs/nguyentienthang-error.log"
    CustomLog "logs/nguyentienthang-access.log" common

    <Directory "D:/Apache24/nguyentienthang">
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>

<img width="1586" height="990" alt="image" src="https://github.com/user-attachments/assets/7987f05e-2db8-4f40-8cae-ab0fb9e22fb2" />

6 Thêm domain vào file hosts

 C:\Windows\System32\drivers\etc\hosts 
 -- Thêm dòng cuối : 127.0.0.1   nguyentienthang.com
 
<img width="818" height="236" alt="image" src="https://github.com/user-attachments/assets/167404f2-b3d6-4a8f-9db0-2dfa9e6a97e1" />

7 Thao tác dòng lệnh trên file D:\Apache24\bin\httpd.exe

 mở ADMIN và chạy
 
 D:\Apache24\bin\httpd.exe -k install
 
D:\Apache24\bin\httpd.exe -k start

  thêm code html -- chạy 
  
  <img width="736" height="272" alt="image" src="https://github.com/user-attachments/assets/9c6db982-7194-4ca1-98ad-0e6f760c89ff" />

  # 2. Cài đặt nodejs và nodered => Dùng làm backend.
  
 2.1 Cài Node.js
 
1️⃣ Tải file cài đặt Node.js (phiên bản ổn định được yêu cầu):

👉 https://nodejs.org/dist/v20.19.5/node-v20.19.5-x64.msi

 2.Tải NSSM
 
 Gải nén vào  "D:\nodejs\nodered" giữ lại  "D:\nodejs\nodered\nssm.exe"
 "D:\nodejs\nodered\nssm.exe"

  3 Tạo file khởi động Node-RED. run-nodered.cmd
  
  @echo off
REM fix path
set PATH=D:\nodejs;%PATH%
REM Run Node-RED
node "D:\nodejs\nodered\node_modules\node-red\red.js" -u "D:\nodejs\nodered\work" %*

  4 Cài đặt service a1-nodered

  <img width="1919" height="1008" alt="image" src="https://github.com/user-attachments/assets/48a82335-5b7f-4c08-8932-956a198e7675" />
  
  # 3 Tạo CSDL.

  Mở ứng dụng Microsoft SQL Server Management Studio

Đăng nhập bằng tài khoản của bạn, ví dụ:

Server name: localhost hoặc 127.0.0.1

Authentication: SQL Server Authentication

Login: sa

Password: (mật khẩu bạn đặt khi cài SQL Server)

1 Tạo Database bất kỳ 

<img width="949" height="363" alt="image" src="https://github.com/user-attachments/assets/129e73ec-29c1-4381-816d-1db10ef7fa5c" />

2 Check Ip config 

<img width="974" height="305" alt="image" src="https://github.com/user-attachments/assets/bf514ebc-ea5e-4ff8-a587-93c9da334d5e" />

check port 

# 4Cài đặt thư viện trên nodered.

 Nếu Node-RED đang chạy như service (bạn đã tạo bằng NSSM):
 
Mở trình duyệt → truy cập:
👉 http://localhost:1880
Giao diện 

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2b4f704d-b14f-4dde-98b6-b7b61a13973e" />

Cài đặt thư viện (node) trong Node-RED
🧭 Thao tác:

Mở trình duyệt → truy cập: http://localhost:1880

Ở góc phải trên cùng → bấm ☰ (menu)

Chọn Manage palette

Chuyển qua tab Install

Nhập tên từng gói bên dưới 

Node-red-contrib-mssql-plus

 Node-red-node-mysql

 Node-red-contrib-telegrambot

 Node-red-contrib-moment

 node-red-contrib-influxdb

 node-red-contrib-duckdns

  node-red-contrib-cron-plus
  

→ bấm Install
3 Sửa file `D:\nodejs\nodered\work\settings.js - > xoá dấu // ở 8 dòng dưới.

<img width="1149" height="391" alt="image" src="https://github.com/user-attachments/assets/9b87641b-5d5e-4c7d-ac96-e92da79f04d5" />

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/0a08ee53-5745-47ac-8a31-fa459937660d" />

  Sinh mật khẩu mã hoá mới.
  
<img width="965" height="340" alt="image" src="https://github.com/user-attachments/assets/70447854-35c0-4351-bba0-b918a5c53fc9" />

Khởi động lại Nodered
Truy cập lại Node-RED

# 5 Tạo API Backend: Dùng các node http in → function → MSSQL → http response để truy vấn và trả JSON về client.

