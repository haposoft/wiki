# File .env
## 1. Không lấy dữ liệu trực tiếp từ tệp .env

Một số lý do để không lấy dữ liệu trực tiếp từ tệp .env là:
- Bảo mật: Tệp .env thường chứa thông tin nhạy cảm như các khóa truy cập API, thông tin đăng nhập, thông tin bảo mật khác. Nếu lấy trực tiếp dữ liệu từ tệp .env, các thông tin này có thể bị lộ ra ngoài và dẫn đến các vấn đề bảo mật.

- Quản lý môi trường: Tệp .env thường được sử dụng để lưu trữ các biến môi trường cấu hình cho ứng dụng. Việc lấy dữ liệu trực tiếp từ tệp .env có thể làm cho việc quản lý các biến môi trường trở nên khó khăn và dễ gây lỗi.

Quy trình chuẩn như vậy bao gồm các bước sau:
1. Khai báo trong tệp .env
2. Nạp vào Config
3. Lấy ra dữ liệu

````php
//Bad
public function index()
{
    $apiKey = env('API_KEY');
}
//Good
// config/api.php
<?php
return [
    ...
    'key' => env('API_KEY'),
    ...
]
// lấy API_KEY ở controller
public function index()
{
    $apiKey = config('api.key');
}
````
