# Baitap3
## Bài tập 3   : môn Phát triển ứng dụng trên nền web
## Giảng viên  : Đỗ Duy Cốp
## Lớp học phần: 58KTPM
*Họ và tên: Nguyễn Thị Xuân Phương_MSSV:k225480106054*
--------------------------------------------------

# Yêu cầu     : LẬP TRÌNH ỨNG DỤNG WEB trên nền linux
## 1. Cài đặt môi trường linux: SV chọn 1 trong các phương án
 - enable wsl: cài đặt docker desktop
## 2. Cài đặt Docker
   Docker Desktop đã được cài đặt và hoạt động thành công 
   
   <img width="1052" height="402" alt="image" src="https://github.com/user-attachments/assets/c9136d6c-da58-4c54-b4ec-e5850443a4a5" />
   
 ## 3. Sử dụng 1 file docker-compose.yml để cài đặt các docker container sau: 
   mariadb (3306), phpmyadmin (8080), nodered/node-red (1880), influxdb (8086), grafana/grafana (3000), nginx (80,443)

<img width="931" height="335" alt="image" src="https://github.com/user-attachments/assets/5d024e19-5a8b-42c4-9705-6f984d7785f5" />

## 4. Lập trình web frontend+backend:
 ### 4.1 Web thương mại điện tử
 - Tạo web dạng Single Page Application (SPA), chỉ gồm 1 file index.html, toàn bộ giao diện do javascript sinh động.
 - Có tính năng login, lưu phiên đăng nhập vào cookie và session
   <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c6fab51e-306d-46ff-b87f-52ca6f12f02f" />

   Thông tin login lưu trong cơ sở dữ liệu của mariadb, được dev quản trị bằng phpmyadmin, yêu cầu sử dụng mã hoá khi gửi login.
   <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/36d753de-88ff-4b8c-99a1-c82078cc41df" />

   Chỉ cần login 1 lần, bao giờ logout thì mới phải login lại.
   
   Em chưa làm được.
 - Có tính năng liệt kê các sản phẩm bán chạy ra trang chủ
   <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/bc4f426d-5d16-44b2-89e5-6f113129510e" />
   
   <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f3813dd6-b77a-49de-9cc4-ec7f271b9761" />

 - Có tính năng liệt kê các nhóm sản phẩm
   <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/0d20a2fa-1d58-49f6-9d5a-d834f042e2ac" />

 - Có tính năng liệt kê sản phẩm theo nhóm
   <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/560e20b3-b2d4-4f76-b140-339dc19cd81e" />

 - Có tính năng tìm kiếm sản phẩm
   <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/3c2f4f6c-d17a-4e7e-a2ad-3ef781d31303" />

 - Có tính năng chọn sản phẩm (đưa sản phẩm vào giỏ hàng, thay đổi số lượng sản phẩm trong giỏ, cập nhật tổng tiền)
   <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1fb58195-b464-4f2e-a64e-5bcb45f83472" />
   <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5cc5da3f-0445-46df-ba5c-eb546a6e3736" />

 - Có tính năng đặt hàng, nhập thông tin giao hàng => được 1 đơn hàng.
   Chỗ này của em đang bị lỗi ạ!
   <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/6df39d03-6bd6-473a-8b5e-275c9ad3197e" />

 - Có tính năng dành cho admin: Thống kê xem có bao nhiêu đơn hàng, call để xác nhận và cập nhật thông tin đơn hàng. chuyển cho bộ phận đóng gói, gửi bưu điện, cập nhật mã COD, tình trạng giao hàng, huỷ hàng,...
 - Có tính năng dành cho admin: biểu đồ thống kê số lượng mặt hàng bán được trong từng ngày. (sử dụng grafana)
   
   2 phần này của em chưa làm được.
 - backend: sử dụng nodered xử lý request gửi lên từ javascript, phản hồi về json.
   <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b045282b-4874-425d-8c80-9c7aa4d0d114" />
   <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/513e4ed3-3829-45ce-b148-af91c210e88b" />

5. Nginx làm web-server
 - Cấu hình nginx để chạy được website qua url http://nguyenthixuanphuong.com
 - Cấu hình nginx để http://nguyenthixuanphuong.com/nodered truy cập vào nodered qua cổng 80, (dù nodered đang chạy ở port 1880)
 - Cấu hình nginx để http://nguyenthixuanphuong.com/grafana truy cập vào grafana qua cổng 80, (dù grafana đang chạy ở port 3000)
```
events {}

http {
  server {
    listen 80;
    server_name nguyenthithuphuong.com;

    # Website chính (index.html)
    location / {
      root /usr/share/nginx/html;
      index index.html;
      try_files $uri $uri/ =404;
    }

    # --- Proxy tới Node-RED ---
    location /nodered/ {
      proxy_pass http://nodered:1880/;
      proxy_http_version 1.1;
      proxy_set_header Host $host;
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header Upgrade $http_upgrade;
      proxy_set_header Connection "upgrade";
      proxy_cache_bypass $http_upgrade;

      # Xử lý redirect nội bộ để không mất /nodered/
      proxy_redirect / /nodered/;
    }

    # --- Proxy tới Grafana ---
    location /grafana/ {
      proxy_pass http://grafana:3000/;
      proxy_http_version 1.1;
      proxy_set_header Host $host;
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header Upgrade $http_upgrade;
      proxy_set_header Connection "upgrade";
      proxy_cache_bypass $http_upgrade;

      # Giữ prefix /grafana/
      proxy_redirect / /grafana/;
    }
  }
}
```
   
   

   


