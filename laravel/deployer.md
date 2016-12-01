# deployer for laravel https://deployer.org
docs: https://deployer.org/docs
## Yêu cầu
+ Một Project laravel đã có trên git.
+ Một server đã cài đủ môi trường để chạy laraval
(ở hướng dẫn này mình cài trên môi trường php7.0 và nginx)
## Cài đặt
cd vào thư mục project của bạn và bắt đầu chạy 3 dòng lệnh sau:
```
curl -LO https://deployer.org/deployer.phar
mv deployer.phar /usr/local/bin/dep
chmod +x /usr/local/bin/depsau
composer require deployer/deployer

```
Bây giờ chúng ta chạy lệnh
```
dep init
```
và bạn chọn Laravel nhé.

**Bây giờ ta cần config lại file deploy.php**
config server cần deploy:
```
server('production', 'domain.com')
    ->user('username')
    ->identityFile('/home/user/.ssh/id_rsa')
    ->set('deploy_path', '/var/www/domain.com');
```
- `production` là tên thôi :D

- `domain.com` là phần domain bạn đăng nhập ssh bạn cũng có thể để ip vps của bạn
- `username` là tên user mà bạn muốn đăng nhập.
- `identityFile(/home/user/.ssh/id_rsa')` đường dẫn đến thư mục ssh key. Ngoài ra bạn có thể sử dụng password thay `->identityFile('/home/user/.ssh/id_rsa')`  bằng `->password('pass')` 
- `->set('deploy_path', '/var/www/domain.com');` với `/var/www/domain.com` là đường dẫn đến thư mục project trên server của bạn.
để kiểm tra xem bạn kết nối được server chưa bạn thêm task ở deploy.php dòng
```
task('pwd', function () {
    $result = run('pwd');
    writeln("Current dir: $result");
});
```
và ở Terminal bạn gõ lệnh `dep qwd` để kiếm tra kết nối của bạn với server được chưa, nếu kết quả trả về như dưới là thành công.
```
➤ Executing task pwd
Current dir: /var/www/domain.com
✔ Ok
```
configure repository. VD:
```
set('repository', 'git@domain.com:username/repository.git');
```
bạn sửa lại cho dúng repo của mình.
bạn để ý những dòng ở cuối file deploy.php
```
task('reload:php-fpm', function () {
    run('sudo /usr/sbin/service php5-fpm reload');
});

after('deploy', 'reload:php-fpm');
```
đoạn này để sau khi deploy server sẽ `reload:php-fpm` thì code mới chạy được nhé. 
ngoài ra bạn có thể config thêm khi deploy thì bạn config thêm ở `MyProject/deployer/deployer/laravel.php`