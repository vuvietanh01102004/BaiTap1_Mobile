# C. Cấu hình docker compose
## 1. Tạo thư mục: ~/myapp
```
mkdir -p ~/myapp
```

## 2. Chuyển vào trong thư mục ~/myapp
```
cd ~/myapp
```
## 3. Tạo thư mục: ./myweb
```
mkdir -p ./myweb
```
<img width="1050" height="702" alt="image" src="https://github.com/user-attachments/assets/4ed126d8-637a-4d16-803a-65ca2849ff8a" />

## 4. Tạo file ./myweb/index.html (với nội dung là thông tin cá nhân của em)
```
nano ./myweb/index.html
```

- Nhập nội dung cá nhân
```
<!doctype html>
<html lang="vi">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Thông tin cá nhân</title>
</head>
<body>
  <h1>Thông tin cá nhân</h1>
  <ul>
    <li>Họ và tên: Vũ Việt Anh</li>
    <li>MSSV: K225480106082</li>
    <li>Lớp: K58KTP.K01</li>
    <li>Trường: Đại học Kỹ thuật Công nghiệp Thái Nguyên</li>
    <li>Email: vuvietanh01102004@gmail.com</li>
  </ul>
</body>
</html>
```
<img width="1044" height="735" alt="image" src="https://github.com/user-attachments/assets/ebd46fe8-bc2c-45b0-85b3-b5baa79028ab" />

## 5. Tạo file docker-compose.yml
### Tạo các thư mục cần thiết
```
cd ~/myapp
mkdir -p ./nodered ./nginx
```
<img width="1051" height="697" alt="image" src="https://github.com/user-attachments/assets/307d4066-3f35-4159-9b49-9750924be5ac" />

### Edit file ./nginx/nginx.conf
```
nano ./nginx/nginx.conf
```
<img width="1045" height="693" alt="image" src="https://github.com/user-attachments/assets/c6e768b7-0501-4b81-ae6c-95c44c824b63" />

### Tạo file docker-compose.yml
```
nano docker-compose.yml
```

- Nội dung  docker-compose.yml
```
services:
  nodered:
    image: nodered/node-red:latest
    container_name: nodered
    ports:
      - "1880:1880"
    volumes:
      - ./nodered:/data
    restart: unless-stopped

  nginx:
    image: nginx:latest
    container_name: nginx
    ports:
      - "80:80"
    volumes:
      - ./myweb:/myweb:ro
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf:ro
    depends_on:
      - nodered
    restart: unless-stopped
```
<img width="1044" height="737" alt="image" src="https://github.com/user-attachments/assets/654ee03c-e9aa-4573-a3a7-aa754cfb2ced" />

## 6. file ./nginx/nginx.conf
### Mở file cấu hình Nginx
```
cd ~/myapp
nano ./nginx/nginx.conf
```

### Cấu hình nginx.conf
```
events {}

http {
  server {
    # (1) Web server cổng 80
    listen 80;

    # (2) server_name là sub-domain
    server_name vva11004.id.vn;

    # (3) location / trỏ tới root là /myweb (web tĩnh)
    location / {
      root /myweb;
      index index.html index.htm;
      try_files $uri $uri/ /index.html;
    }

    # (4) location /api proxy_pass sang Node-RED (http_in)
    # Lưu ý quan trọng: KHÔNG có dấu "/" ở cuối proxy_pass để giữ nguyên đường dẫn /api/...
    location /api/ {
      proxy_pass http://nodered:1880;

      proxy_set_header Host $host;
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header X-Forwarded-Proto $scheme;
    }
  }
}
```
<img width="1043" height="732" alt="image" src="https://github.com/user-attachments/assets/c9a68965-2dbc-4bc7-903e-6ba503e8f368" />

### Khởi động lại Docker Compose để áp dụng cấu hình
```
docker compose up -d
```
<img width="1050" height="692" alt="image" src="https://github.com/user-attachments/assets/8aed39ad-5716-4cfd-bdb2-fffa264119b5" />

```
docker compose ps
```
<img width="1922" height="935" alt="image" src="https://github.com/user-attachments/assets/0c496eef-d9b9-467a-910a-aa2625ce6922" />

### Tạo API trong Node-RED
- Truy cập NodeRED: `http://192.168.1.11:1880/`
<img width="1919" height="968" alt="image" src="https://github.com/user-attachments/assets/0df88a63-6ab1-422a-a71d-ec870a734fa4" />

<img width="1919" height="866" alt="image" src="https://github.com/user-attachments/assets/8b33720c-5185-4b99-a709-5477f0653a85" />

- http in:
<img width="1919" height="864" alt="image" src="https://github.com/user-attachments/assets/a82f32e0-143f-40fe-8e22-0f9392a64307" />

- function:
<img width="1919" height="870" alt="image" src="https://github.com/user-attachments/assets/c8c05f5a-a745-42ce-9216-9041b41aafcd" />

-> Sau đó ấn Deloy để lưu lại

### Kiểm tra kết quả
- Kiểm tra web tĩnh
```
curl -I http://localhost/
curl http://localhost/ | head -n 20
```
<img width="1922" height="1017" alt="image" src="https://github.com/user-attachments/assets/9c8b236f-b683-412e-96b1-8fa1b20ac67e" />

- Kiểm tra proxy sang Node-RED
```
curl http://localhost/api/hello
```
<img width="1923" height="797" alt="image" src="https://github.com/user-attachments/assets/17330cba-bfbc-43ae-96eb-23b5814700e9" />

## 7. Edit file ./nodered/settings.js để nodered bắt buộc đăng nhập
### Chạy docker compose lần đầu để Node-RED tự sinh cấu hình trong ./nodered
```
ls -la ./nodered | head
ls -la ./nodered/settings.js
```
<img width="1922" height="1018" alt="image" src="https://github.com/user-attachments/assets/15f398ae-caa4-4f33-8522-895cc6679409" />

### Tạo mật khẩu dạng hash (bcrypt) để dùng trong settings.js
```
docker exec -it nodered node -e "console.log(require('bcryptjs').hashSync(process.argv[1], 8));" '@12345'
```
- Sau khi chạy sẽ ra 1 chuỗi hash: `$2b$08$DNIuDjZxO1ptAqXJWDNe8eL1R.dZNyRUMLq9p9zUw5JMTzB.KaIbK`
<img width="1922" height="768" alt="image" src="https://github.com/user-attachments/assets/05ef591d-04a4-453f-b2bb-042c20c7a119" />

### Edit ./nodered/settings.js
```
nano ./nodered/settings.js
```
- Ấn `Ctrl + W` -> nhập `adminAuth` rồi Enter
- Tại block adminAuth, tiến hành:
 + xoá dấu `//` ở đầu các dòng
 + Viết `username` và `password` (chuỗi hash vừa tạo)
<img width="1918" height="1017" alt="image" src="https://github.com/user-attachments/assets/3ce7ad84-dc3d-4b25-8e92-48cef382e12c" />

### Restart Node-RED và kiểm tra kết quả
```
docker compose restart nodered
```
<img width="1921" height="970" alt="image" src="https://github.com/user-attachments/assets/00cf5283-545d-4dfd-9cad-9fdd3dc953bd" />

- Truy cập lại `http://192.168.1.11:1880/`
<img width="1919" height="869" alt="image" src="https://github.com/user-attachments/assets/baa9d8c3-978f-44b7-8491-3da9d17ef412" />




