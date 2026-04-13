# D. Bonus
## 1. tạo thư mục ./myapi
```
cd ~/myapp
mkdir -p ./myapi
```
<img width="1049" height="633" alt="image" src="https://github.com/user-attachments/assets/1e267c71-730c-40a9-bc13-00c1b336accb" />

## 2. tạo file ./myapi/app.py sử dụng Python + Flask để làm gì đó funny
- Tạo 1 file
```
nano ./myapi/app.py
```

- Nội dung
```
from flask import Flask, request, jsonify

app = Flask(__name__)

@app.route('/bmi', methods=['GET'])
def tinh_bmi():
    chieu_cao = request.args.get('chieu_cao')
    can_nang = request.args.get('can_nang')

    if chieu_cao is None or can_nang is None:
        return jsonify({"error": "Cần cung cấp 'chieu_cao' (m) và 'can_nang' (kg)"}), 400

    try:
        h = float(chieu_cao)
        w = float(can_nang)

        if h <= 0 or w <= 0:
            return jsonify({"error": "Chiều cao và cân nặng phải > 0"}), 400

        bmi = w / (h * h)

        # Phân loại BMI
        if bmi < 18.5:
            loai = "Gầy"
        elif bmi < 25:
            loai = "Bình thường"
        elif bmi < 30:
            loai = "Thừa cân"
        else:
            loai = "Béo phì"

        return jsonify({
            "chieu_cao": h,
            "can_nang": w,
            "bmi": round(bmi, 2),
            "phan_loai": loai
        })

    except ValueError:
        return jsonify({"error": "Dữ liệu nhập phải là số"}), 400

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=9630)
```
<img width="1199" height="768" alt="image" src="https://github.com/user-attachments/assets/fdd1be90-34e1-4aba-8788-52c85802e968" />

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
curl "http://localhost:9630/bmi?chieu_cao=1.7&can_nang=65"
```
- Kết quả kỳ vọng
```
{"bmi":22.49,"can_nang":65.0,"chieu_cao":1.7,"phan_loai":"B\u00ecnh th\u01b0\u1eddng"}
```
<img width="1923" height="816" alt="image" src="https://github.com/user-attachments/assets/73ef85dc-db6a-4200-aec7-60f61dd4ba9e" />

## 6. Sửa đổi nginx/nginx.conf để /api trỏ tới service myapp cổng 9630
```
nano ~/myapp/nginx/nginx.conf
```
- Thay block location /api thành:
```
location /api {
  proxy_pass http://myapi:9630/tinh-vat;
  proxy_set_header Host $host;
  proxy_set_header X-Real-IP $remote_addr;
  proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
  proxy_set_header X-Forwarded-Proto $scheme;
}
```
<img width="810" height="558" alt="image" src="https://github.com/user-attachments/assets/51785f3e-4a4f-412a-8f75-baa032005395" />

```
docker compose restart nginx
```




