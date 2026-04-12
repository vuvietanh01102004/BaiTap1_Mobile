# A. Đăng ký tên miền xịn cho cá nhân
## Đăng kí domain
- Đăng kí tên miền tại: https://www.matbao.net/
- Tên miền đã đăng kí thành công: vva11004.id.vn
<img width="1919" height="863" alt="image" src="https://github.com/user-attachments/assets/1adc8e0e-30db-4926-bb5a-c031657ae4e9" />

## Đăng kí tài khoản cloudflare
- Truy cập trang đăng kí bằng đường dẫn: https://dash.cloudflare.com/login
- Sau khi truy cập vào rồi có 3 tuỳ chọn đăng nhập hoặc đăng kí
- Ở đây ta chọn đăng nhập bằng tài khoản Github
<img width="1567" height="705" alt="image" src="https://github.com/user-attachments/assets/2e5d9656-7303-4353-8948-1ae5121312e6" />

<img width="1919" height="867" alt="image" src="https://github.com/user-attachments/assets/b2f26910-165e-4dd7-93b0-d4c952dbdb77" />

## Thêm domain đã đăng ký vào trong cloudflare
- Vào Account home -> Chọn dấu "+" phần domain để thêm tên miền
<img width="1918" height="862" alt="image" src="https://github.com/user-attachments/assets/17a300b5-30f1-418c-a352-43aec50a2e38" />

- Ở mục Enter an existing domain Or register a new domain, nhập domain đã đăng kí:
  + vva11004.id.vn
- Còn lại mọi thứ để mặc định và ấn Continue
<img width="1918" height="862" alt="image" src="https://github.com/user-attachments/assets/0dc9f029-8eac-4d64-b346-55496347ee36" />

- Xác nhận DNS
- Chọn nút Continue to activation
<img width="1898" height="867" alt="image" src="https://github.com/user-attachments/assets/ff83ec01-7058-48b0-950c-d1de97614d5f" />

- Nhận 2 dòng Nameserver (Namespace) do Cloudflare cấp
  + Sau đó cloudflare sẽ hiển thị: Update your nameservers to activate Cloudflare
  + Ở mục 2 là "Replace your current nameservers with Cloudflare nameservers", có xuất hiện 2 dòng mà cloudflare cấp:
    + `leif.ns.cloudflare.com`
    + `paige.ns.cloudflare.com`
<img width="1892" height="865" alt="image" src="https://github.com/user-attachments/assets/fc9b2939-441c-445a-969b-b8e603f20da3" />

## Nhập 2 dòng namespace của cloudflare vào trong trang quản lý DNS record của tên miền đăng ký
- Đăng nhập vàp trang quản lý domain đã đăng kí
  + Ở mục "quản trị tên miền" chọn Name Server -> chọn "sử dụng Name Server tuỳ chỉnh"
  + Thêm 2 name server vừa được nhận sau đó ấn "lưu thay đổi"
<img width="1918" height="865" alt="image" src="https://github.com/user-attachments/assets/87a5e06e-e6d9-4c17-8a6b-626d93964ef7" />

- Quay lại cloudflare để xác nhận cập nhật DNS
<img width="1897" height="861" alt="image" src="https://github.com/user-attachments/assets/d767844a-3581-4be2-a704-8f72d5ca06f8" />

- Cloudflare thông báo "Your domain is now protected by Cloudflare" là đã thành công
<img width="1897" height="868" alt="Screenshot 2026-04-12 190609" src="https://github.com/user-attachments/assets/7c42d09c-65f5-4cfb-9ff0-6e1829f5a269" />

<img width="1919" height="870" alt="image" src="https://github.com/user-attachments/assets/1b29e3f9-88a4-4229-8358-2efd615859f1" />







