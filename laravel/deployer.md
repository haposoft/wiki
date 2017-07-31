# deployer for laravel https://deployer.org
docs: https://deployer.org/docs
## Yêu cầu
+ Một Project laravel đã có trên git.
+ Một server đã cài đủ môi trường để chạy laraval
(ở hướng dẫn này mình cài trên môi trường php7.0 và nginx)
## Cài đặt
cd vào thư mục project của bạn và bắt đầu chạy 4 dòng lệnh sau:
```
curl -LO https://deployer.org/deployer.phar
mv deployer.phar /usr/local/bin/dep
chmod +x /usr/local/bin/dep
composer require deployer/deployer

```
Bây giờ chúng ta chạy lệnh
```
dep init
```
sẽ xuất hiện một số lựa chọn và chọn Laravel.

### Bây giờ ta cần config lại file deploy.php
#### 1. config server cần deploy:
```
server('production', 'domain.com')
    ->user('username')
    ->identityFile('/home/user/.ssh/id_rsa')
    ->set('deploy_path', '/var/www/domain.com');
```
- `production` : Name server.

- `domain.com` là phần domain đăng nhập ssh cũng có thể để ip vps.
- `username` là tên user đăng nhập.
- `identityFile(/home/user/.ssh/id_rsa')` đường dẫn đến thư mục ssh key. Ngoài ra có thể sử dụng password (thay `->identityFile('/home/user/.ssh/id_rsa')`  bằng `->password('pass')` )
- `->set('deploy_path', '/var/www/domain.com');` với `/var/www/domain.com` là đường dẫn đến thư mục project trên server.
để kiểm tra xem bạn kết nối được server chưa. Thêm task ở deploy.php dòng.
```
task('pwd', function () {
    $result = run('pwd');
    writeln("Current dir: $result");
});
```
và ở Terminal gõ lệnh `dep qwd` để kiếm tra kết nối của bạn với server được chưa, nếu kết quả trả về như dưới là thành công.
```
➤ Executing task pwd
Current dir: /var/www/domain.com
✔ Ok
```
#### 2. onfigure repository.
```
set('repository', 'git@domain.com:username/repository.git');
```
Sửa lại cho dúng repo của mình.
#### 3. After deploy
```
task('reload:php-fpm', function () {
    run('sudo /usr/sbin/service php7.0-fpm reload');
});

after('deploy', 'reload:php-fpm');
```
đoạn này để sau khi deploy server sẽ `reload:php-fpm`. Nếu dùng phiên bản khác `php7.0-fpm` thì thay cho phù hợp.
ngoài ra bạn có thể config thêm khi deploy thì bạn config thêm ở `MyProject/deployer/deployer/laravel.php`
