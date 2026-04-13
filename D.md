# D. Bonus
## 1. tạo thư mục ./myapi
```
cd ~/myapp
mkdir -p ./myapi
```
<img width="1049" height="633" alt="image" src="https://github.com/user-attachments/assets/1e267c71-730c-40a9-bc13-00c1b336accb" />

## 2. Tạo file ./myapi/app.py sử dụng Python + Flask để làm gì đó funny
- Tạo 1 file
```
nano ./myapi/app.py
```

- Nội dung
```
from flask import Flask, request, jsonify

app = Flask(__name__)
app.config['JSON_AS_ASCII'] = False  # Hiển thị tiếng Việt chuẩn

@app.route('/tinh-phi', methods=['GET'])
def tinh_phi():
    # Lấy giá trị từ tham số "gia_tri"
    gia_tri_input = request.args.get('gia_tri')

    # Kiểm tra nhập liệu
    if gia_tri_input is None:
        return jsonify({"error": "Vui lòng cung cấp tham số 'gia_tri'"}), 400

    try:
        # Chuyển sang số
        gia_tri = float(gia_tri_input)

        # Tính phí dịch vụ 5%
        phi = gia_tri * 0.05
        tong = gia_tri + phi

        return jsonify({
            "gia_tri_ban_dau": gia_tri,
            "phi_dich_vu": "5%",
            "so_tien_phi": phi,
            "tong_thanh_toan": tong
        })

    except ValueError:
        return jsonify({"error": "Giá trị 'gia_tri' phải là số hợp lệ"}), 400

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=9630)
```
<img width="971" height="619" alt="image" src="https://github.com/user-attachments/assets/1015c56a-d0e3-4434-9a51-c425718b8639" />

## 3. tạo file ./myapi/requirements.txt chứa các thư viện mà app.py sử dụng
```
nano ./myapi/requirements.txt
```
- Nội dung: `Flask`

## 4. tạo file ./myapi/Dockerfile để khai báo sử dụng Python 3.9 slim
```
nano ./myapi/Dockerfile
```
- Nội dung:
```
 # Sử dụng phiên bản Python nhẹ (alpine) để giảm dung lượng image
 FROM python:3.9-slim

 # Thiết lập thư mục làm việc bên trong container
 WORKDIR /app

 # Sao chép file requirements vào và cài đặt thư viện
 COPY requirements.txt .
 RUN pip install --no-cache-dir -r requirements.txt

 # Sao chép toàn bộ mã nguồn vào container
 COPY . .

 # Thông báo container sẽ chạy ở cổng 9630
 EXPOSE 9630

 # Lệnh khởi chạy ứng dụng
 CMD ["python", "app.py"]
```
<img width="1043" height="622" alt="image" src="https://github.com/user-attachments/assets/07c182a0-2a32-4351-b193-57c21699e280" />

## 5. Sửa đổi docker-compose để sử dụng myapp
```
nano ~/myapp/docker-compose.yml
```
- Bổ sung vào:
```
  myapi:
    build:
      context: ./myapi
      dockerfile: Dockerfile
    container_name: myapi
    ports:
      - "9630:9630"
    restart: unless-stopped
```
<img width="1044" height="654" alt="image" src="https://github.com/user-attachments/assets/3324bff4-79ee-4945-9391-f392725d423a" />

- Kiểm tra:
```
cd ~/myapp
docker compose config
```
<img width="1918" height="1020" alt="image" src="https://github.com/user-attachments/assets/67dc7614-dfd5-4fb2-a7e8-6a3db6ffaba8" />

```
docker compose up -d --build
docker compose ps
```
<img width="1918" height="1020" alt="image" src="https://github.com/user-attachments/assets/76ea12f5-c282-4825-93ae-5e52d17c2545" />

- Test myapi trực tiếp (không qua Nginx)
```
curl "http://localhost:9630/tinh-phi?gia_tri=100"
```
- Kết quả kỳ vọng
```
{"gia_tri_ban_dau":100.0,"phi_dich_vu":"5%","so_tien_phi":5.0,"tong_thanh_toan":105.0}
```
<img width="1284" height="706" alt="image" src="https://github.com/user-attachments/assets/1da823e9-1200-4cce-ba40-ce4aab738906" />

## 6. Sửa đổi nginx/nginx.conf để /api trỏ tới service myapp cổng 9630
```
nano ~/myapp/nginx/nginx.conf
```
- Thay block location /api thành:
```
        location /api/ {
            proxy_pass http://127.0.0.1:9630/;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }
}
```
<img width="865" height="542" alt="image" src="https://github.com/user-attachments/assets/9bb15bb9-8d78-4afd-b599-b4d39676c160" />

```
docker compose restart nginx
```

### Kiểm tra
- Gọi API thông qua Nginx (port 80):
```
curl -i "http://localhost/api/tinh-phi?gia_tri=100"
```
<img width="1922" height="730" alt="image" src="https://github.com/user-attachments/assets/90db118b-58d7-485c-931d-5a091394d36f" />



