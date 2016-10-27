## Gửi email dùng Sendgrid API trong Laravel 
###1. Sendgrid là gì?
**Sendgrid** là một trong những dịch vụ cung cấp transaction email theo chuẩn SMTP, dựa trên nền tảng đám mây thay thế cho hệ thống mail server.
Để sử dụng dịch vụ này cần đăng ký một tài khoản tại [Sendgrid.com](https://sendgrid.com)

###2. Cấu hình để gửi email qua Sendgrid API.
Trong file  `.env` , chỉnh sửa một số thông tin:

```
MAIL_DRIVER=smtp
MAIL_HOST=smtp.sendgrid.net
MAIL_PORT=587
MAIL_USERNAME=sendgridusername
MAIL_PASSWORD=sendgridpassword
MAIL_ENCRYPTION=tls
```

###3. Sử dụng Sendgrid API để gửi mail.
   * Tạo controller trong `routes/web.php`:
```
Route::get('mail', 'HomeController@mail');
```
 
   * Tạo method `mail` trong `app/Http/Controllers/HomeController.php`:

```
public function mail()
{
    Mail::send('emails.mailEvent', function($message) {
        $message->from('admin@gmail.com', 'Admin');
        $message->to('thanhnt@gmail.com', 'ThanhNT');
        $message->subject('Sendgrid Testing');
    });
    dd('Mail Send Successfully');
}
```

   * Tạo template mail `resources/views/emails/mailEvent.blade.php` với nội dung:
```
Hi, sendgrid testing.
```
