# E. Triển khai (level test) ứng dụng
## 1. Chuyển vào trong thư mục ~/myapp
```
cd ~/myapp
pwd
```

## 2. Gõ lệnh để docker compose chạy: sẽ run tất cả các service khai báo trong file docker-compose.yml
```
docker compose up -d
```
<img width="1046" height="608" alt="image" src="https://github.com/user-attachments/assets/3a7bef82-ca2d-4a83-8d1b-a193b9e4247e" />

## 3. Kiểm tra các container đang chạy trong docker
```
docker compose ps
```
<img width="1130" height="620" alt="image" src="https://github.com/user-attachments/assets/54496150-2463-4d28-93ef-05d62aa78787" />

## 4. Kiểm tra kiểm thử các service đang chạy độc lập thông qua ip và port của nó
### Xem IP
```
ip -4 addr
```
<img width="1916" height="748" alt="image" src="https://github.com/user-attachments/assets/a427cc0b-3dce-4b96-9d5e-2b3f65bfdb48" />

### Kiểm thử Nginx
```
curl -I http://localhost/
```
<img width="1921" height="930" alt="image" src="https://github.com/user-attachments/assets/df2501a2-8eeb-4977-8f2d-67181a466704" />



