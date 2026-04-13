# B. Cài đặt Ubuntu + Docker
## Cài đặt hệ điều hành Ubuntu 24.04.4 LTS
### Tải các file cần thiết
- Tải file ISO: Ubuntu 24.04.4 LTS (Desktop) từ link tải: https://releases.ubuntu.com/24.04.4/
<img width="1894" height="870" alt="image" src="https://github.com/user-attachments/assets/38340b09-5cad-4471-84a9-a5882cea7c70" />

- Cài đặt ảo hoá VMware Workstation từ link tải: https://dl.bobpony.com/software/vmware/workstation/
- Chọn phiên bản mới nhất là VMware Workstation 17.6.4 để tải

### Tạo máy ảo Ubuntu trên VMWare
- Chọn "Create a New Virtual Machine" để tạo máy ảo mới
<img width="1919" height="1012" alt="image" src="https://github.com/user-attachments/assets/a43af90d-18c8-417f-b761-254b967bf680" />

- Chọn đến file .iso vừa mới tải về
<img width="1919" height="1012" alt="image" src="https://github.com/user-attachments/assets/3b5ee83d-e843-4fde-8890-528e84e8074a" />

- SAu khi đã tạo máy ảo tên Ubuntu 64-bit, chuột trái chọn "Settting" -> Network Adapter rồi tích chọn Bridged
<img width="1918" height="1017" alt="Screenshot 2026-04-12 210828" src="https://github.com/user-attachments/assets/a9d91d16-b424-4a76-9045-c1b5f58b7b14" />

### Bắt đầu cài đặt Ubuntu 24.04.4 Live Server
<img width="1909" height="1016" alt="image" src="https://github.com/user-attachments/assets/12b22799-6cb4-4502-a69a-2756fcfcb32c" />

<img width="1918" height="1023" alt="image" src="https://github.com/user-attachments/assets/003a04af-cb3d-44a9-8051-4be70879f24c" />

<img width="1915" height="1020" alt="image" src="https://github.com/user-attachments/assets/4437ecdf-c1bc-4c16-8c41-4a90b9a91565" />

- Ở phần Proxy Configuration có thể để trống
<img width="1919" height="1021" alt="image" src="https://github.com/user-attachments/assets/559fc17c-05d5-4226-bb09-c026a7ba4722" />

<img width="1919" height="1021" alt="image" src="https://github.com/user-attachments/assets/adda8e91-f4cd-4e8f-945d-ad55797dea0f" />

<img width="1919" height="1019" alt="image" src="https://github.com/user-attachments/assets/9ad8e75e-1db5-484d-b095-43b84b7cd5c0" />

- Chọn Install OpenSHH Server để cài đặt
<img width="1916" height="1019" alt="image" src="https://github.com/user-attachments/assets/1a83a6a7-2860-4720-8672-fd0d04d895c2" />

<img width="1919" height="1020" alt="image" src="https://github.com/user-attachments/assets/2e6d13f0-1290-4a3d-b5a9-7aa9a56050ca" />

<img width="1918" height="1021" alt="image" src="https://github.com/user-attachments/assets/16d3954d-c818-41a8-82b6-a221555bdb25" />

### Tháo ISO sau khi cài
<img width="1919" height="1021" alt="image" src="https://github.com/user-attachments/assets/47b410d1-5758-443f-8e75-aaa1d560ca96" />

- Sau đó quay lại để tiếp tục Reboot
<img width="1918" height="1022" alt="image" src="https://github.com/user-attachments/assets/012dbf19-33b4-478d-ae47-f623146a94df" />

### Đăng nhập Ubuntu Server cài SSH
<img width="1918" height="1018" alt="image" src="https://github.com/user-attachments/assets/e761ba7b-9bc9-4e89-bcc3-d9deae7af4ae" />

- chạy lệnh `sudo systemctl enable ssh --now` để tự chạy khi boot
- Kiểm tra lại bằng `sudo systemctl status ssh`
  + Nếu thấy xuất hiện dòng: `Active: active (running)` là thành công
- Tiếp tục kiểm tra IP bằng lệnh `ip -4 addr`
  + Hiển thị IPv4: 192.168.1.11
<img width="1918" height="1017" alt="image" src="https://github.com/user-attachments/assets/5ceb9630-e3a7-4745-ae55-86352c9cd718" />

### Chạy CMD để mở SSH vào Ubuntu
- Trên CMD chạy lệnh `vietanh@192.168.1.11` -> chọn Yes rồi Enter
- Sau đó nhập password rồi Enter
<img width="1239" height="834" alt="image" src="https://github.com/user-attachments/assets/6aa0f4fb-b2e9-480d-8037-b87e96e44cc8" />

## Tìm hiểu các lệnh cơ bản của ubuntu
### 1. Liệt kê các file trong thư mục
```
pwd
ls
ls -l
```
### 2. Tạo thư mục
```
mkdir -p B1/data
```
<img width="743" height="722" alt="image" src="https://github.com/user-attachments/assets/dafd9f27-867d-49af-bcf6-fbdd23a5321c" />

### 3. Chuyển thư mục làm việc
- Tạo 1 file note.txt rồi nhập ví dụ vài dòng chữ
```
nano note.txt
```
<img width="924" height="636" alt="image" src="https://github.com/user-attachments/assets/e57b4fef-564c-4f41-bd97-a5f7cdc62bb6" />

- Kiểm tra bằng `ls -1`
<img width="921" height="605" alt="image" src="https://github.com/user-attachments/assets/81eb5b70-a7b3-4f8f-9c1c-82a54b62db7b" />

### 4. Copy file
```
cp note.txt data/note_copy.txt
```
<img width="922" height="638" alt="image" src="https://github.com/user-attachments/assets/f1837d3a-7a76-492f-925d-13aef009ffa2" />

### 5. Thay đổi quyền thao tác file
<img width="929" height="637" alt="image" src="https://github.com/user-attachments/assets/371ab591-8a51-4b32-a12d-0722dd74659c" />

### 6. Edit file
```
sudo nano data/note_copy.txt
```
- Viết thêm 1 dòng ví dụ: `Ten nguoi dung là vietanh`
<img width="928" height="635" alt="image" src="https://github.com/user-attachments/assets/5c060242-a751-4b44-bb64-40a2c2822ba5" />

### 7. Xem ip của máy ubuntu
```
ip -4 addr
```
<img width="930" height="639" alt="image" src="https://github.com/user-attachments/assets/9e641b41-4798-417e-923b-82f0ad94c8a4" />

## Cài đặt docker cho Ubuntu
### 1. Cập nhật hệ thống
```
sudo apt update
sudo apt upgrade -y
```
### 2. Cài các gói cần thiết
```
sudo apt install -y ca-certificates curl gnupg
```
### 3. Thêm GPG key của Docker
```
sudo install -m 0755 -d /etc/apt/keyrings

curl -fsSL https://download.docker.com/linux/ubuntu/gpg \
| sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

sudo chmod a+r /etc/apt/keyrings/docker.gpg
```
- Nếu xuất hiện `Overwrite? (y/N)` -> gõ y rồi Enter
### 4. Thêm repository Docker
```
echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
https://download.docker.com/linux/ubuntu \
$(. /etc/os-release && echo $VERSION_CODENAME) stable" \
| sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
- Update lại
```
sudo apt update
```
<img width="1919" height="1017" alt="image" src="https://github.com/user-attachments/assets/ceb69419-a237-4ddd-85d7-a75e4aa5484a" />

### 5. Cài Docker + Compose
```
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
- Bật Docker
```
sudo systemctl enable --now docker
```
## Kiểm tra Docker
- Kiểm tra version Docker: `docker --version`
<img width="924" height="541" alt="image" src="https://github.com/user-attachments/assets/20d7e194-2d4d-4d4e-b2db-ce23a71e73fb" />

- Kiểm tra Docker Compose: `docker compose version`
<img width="542" height="117" alt="image" src="https://github.com/user-attachments/assets/8429b865-e60d-46d0-96cd-26e4d154cf1c" />

## Chạy Docker không cần sudo
- Thêm user vào group docker
```
sudo usermod -aG docker $USER
```

- Áp dụng group mới
```
newgrp docker
```

- Chạy Docker không cần sudo
```
docker run --rm hello-world
```
<img width="1038" height="732" alt="image" src="https://github.com/user-attachments/assets/e60f98bf-1d4e-4dfc-9bd7-336ab6b4dca3" />

## Tìm hiểu tập lệnh của docker và docker compose
### 1. Docker
Kiểm tra phiên bản và thông tin Docker
```
docker --version
docker version
docker info
```
- docker --version: Hiển thị phiên bản Docker client đang cài đặt
- docker version: Hiển thị chi tiết phiên bản của cả Client và Server (Docker Engine)
- docker info: Cung cấp thông tin tổng quan hệ thống Docker như:
  + Số lượng container, image
  + Storage driver
  + Network
  + CPU, RAM Docker sử dụng


Quản lý Image
```
docker images
docker pull nginx:latest
docker rmi nginx:latest
docker image prune -a
```
- docker images: Liệt kê tất cả image hiện có trong máy
- docker pull <image>:<tag>: Tải image từ Docker Hub (mặc định là latest nếu không ghi tag)
- docker rmi <image>: Xoá image khỏi hệ thống
- docker image prune -a: Xoá toàn bộ image không còn được sử dụng


Quản lý Container
```
docker ps
docker ps -a
docker run --name web -d -p 80:80 nginx:latest
docker logs web
docker exec -it web bash
docker stop web
docker start web
docker restart web
docker rm web
```
- docker ps: Xem các container đang chạy
- docker ps -a: Xem tất cả container (kể cả đã dừng)
- docker run: Tạo và chạy container
 + --name web: đặt tên container
 + -d: chạy ở chế độ nền (detached mode)
 + -p 80:80: ánh xạ cổng (host → container)
- docker logs <name>: Xem log của container
- docker exec -it <name> bash: Truy cập vào bên trong container
- docker stop/start/restart: Dừng / chạy / khởi động lại container
- docker rm <name>: Xoá container (phải dừng trước hoặc dùng -f)


Quản lý Volume (lưu trữ dữ liệu)
```
docker volume ls
docker volume create mydata
docker volume inspect mydata
docker volume rm mydata
```
- docker volume ls: Liệt kê volume
- docker volume create: Tạo volume mới
- docker volume inspect: Xem chi tiết volume
- docker volume rm: Xoá volume


Quản lý Network
```
docker network ls
docker network create mynet
docker network inspect mynet
docker network rm mynet
```
- docker network ls: Liệt kê các network
- docker network create: Tạo network mới
- docker network inspect: Xem thông tin chi tiết
- docker network rm: Xoá network

### 2. Docker Compose
Kiểm tra phiên bản
```
docker compose version
```
- Dùng để kiểm tra Docker Compose đã được cài đặt và hoạt động.


Các lệnh cơ bản
```
docker compose up -d
docker compose ps
docker compose logs -f
docker compose down
```
- docker compose up -d: Tạo và chạy toàn bộ service trong file docker-compose.yml
- docker compose ps: Xem trạng thái các container
- docker compose logs -f: Xem log realtime
- docker compose down: Dừng và xoá container + network


Build Image
```
docker compose build
docker compose up -d --build
```
- build: Build image từ Dockerfile
- --build: Build lại image trước khi chạy


Quản lý vòng đời container
```
docker compose stop
docker compose start
docker compose restart
```
- Dùng để điều khiển toàn bộ hệ thống container (stack)


Kiểm tra cấu hình
```
docker compose config
```
- Hiển thị file cấu hình sau khi:
 + xử lý biến môi trường
 + gộp các cấu hình
- Giúp kiểm tra lỗi trước khi chạy.

## Đảm bảo tường lửa trên Ubuntu đã cho phép các cổng 80, 1880, 9630
### 1. Xác định trạng thái hiện tại của UFW
- Trước khi cấu hình, cần kiểm tra xem tường lửa đã được bật hay chưa:
```
sudo ufw status
```
- Nếu hiển thị inactive → UFW chưa hoạt động, hệ thống chưa áp dụng quy tắc nào
- Nếu hiển thị active → UFW đang chạy và các rule đã có hiệu lực
<img width="1040" height="695" alt="image" src="https://github.com/user-attachments/assets/fec5d3a6-5d61-4c10-b99f-fbfea71cfa64" />

### 2. Cho phép kết nối SSH trước khi bật tường lửa
- Vì hệ thống được quản lý từ xa (qua SSH), cần mở cổng SSH để tránh bị mất kết nối sau khi bật firewall:
```
sudo ufw allow OpenSSH
```
<img width="1043" height="627" alt="image" src="https://github.com/user-attachments/assets/3405f642-154e-457b-b8db-dc268df2b481" />
- Lệnh này cho phép truy cập qua cổng 22 (SSH)
- Nếu không thực hiện, bạn có thể bị “kick” khỏi server sau khi bật UFW

### 3. Cấu hình mở các cổng dịch vụ cần thiết
- Tiến hành cho phép các cổng theo yêu cầu của bài:
```
sudo ufw allow 80/tcp
sudo ufw allow 1880/tcp
sudo ufw allow 9630/tcp
```
<img width="1044" height="685" alt="image" src="https://github.com/user-attachments/assets/997c7411-8844-4c26-b835-70f81b60302a" />
- Ý nghĩa từng cổng:
 + 80/tcp: dùng cho web server (HTTP)
 + 1880/tcp: thường dùng cho Node-RED
 + 9630/tcp: dùng cho các ứng dụng/dịch vụ tùy chỉnh
- Việc chỉ định /tcp giúp kiểm soát chính xác giao thức được phép.

### 4. Kích hoạt UFW
- Sau khi đã thiết lập rule, tiến hành bật tường lửa:
```
sudo ufw enable
```
<img width="1055" height="691" alt="image" src="https://github.com/user-attachments/assets/05d9f419-1cb1-42c3-ae4d-75f8399f840c" />

### 5. Kiểm tra lại cấu hình
- Sau khi bật, cần xác nhận các rule đã được áp dụng:
```
sudo ufw status numbered
```
- Danh sách các rule cho phép các cổng 22, 80, 1880, 9630
- Trạng thái UFW là active
<img width="1050" height="737" alt="image" src="https://github.com/user-attachments/assets/570fbfa2-e360-4875-b001-f91ef2bd96a3" />


