# Composer

Trước khi Composer ra đời, chúng ta thường gặp khó với hàng chục các thư viện của bên thứ ba cần phải quản lý. Việc update rất khó khăn

## 1. Composer là gì?

- Composer không phải cài đặt global. Chính vì thế nó còn được gọi là Dependency Manager
- Composer quản lý sự phụ thuộc các tài nguyên trong dự án. Nó cho phép khai báo các thư viện mà dự án của bạn sử dụng, composer sẽ tự động tải code của các thư viện.
- Nó tạo ra các file cần thiết vào project của bạn, và cập nhật các thư viện khi có phiên bản mới

## 2. Lợi ích của composer

Ý tưởng của composer không phải là mới, nó được lấy cảm hứng từ các công cụ như npm của Node, tuy nhiên composer chỉ ở phạm vi dự án PHP

Trước đây khi bạn triển khai các dự án dựa trên các, bạn sẽ phải đối mặt một số việc sau:
- Dự án của bạn có sử dụng một số thư viện ở ngoài. Bạn phải tải chúng rồi cho vào folder của project rồi mới sử dụng được.
- Một số các thư viện đó lại sử dụng (phụ thuộc) các thư viện khác.
- Bạn sẽ gặp những khó khăn trong việc cập nhật phiên bản của các thư viện. Nếu thư viện A, có sử dụng thư viện B, thư viện B sử dụng thư viện C. Thì nếu một trong các thư viện này có update, bạn sẽ phải tự mình lần mò về phần gốc của nó để update.

Tuy nhiên, công việc sẽ thật dễ dàng với Composer, bạn sẽ làm được:
- Khai báo các thư viện mà dự án sử dụng. Quản lý tập trung các thư viện đang sử dụng cho project và cả phiên bản của chúng dễ dàng qua file `composer.json`

## 3. `composer.json` và `composer.lock`
Đây là 2 file rất quan trọng trong một package composer.
- composer.json là nơi ta khai báo những dependencies dùng trong project, những thông tin về tên, phiên bản, licenses, source … Nội dung được viết theo JSON format.

````
{
    "name": "laravel/laravel",
    "type": "project",
    "description": "The Laravel Framework.",
    "keywords": ["framework", "laravel"],
    "license": "MIT",
    "authors": [
    {
        "name": "Dinh Quoc Han",
        "email": "admin@dinhquochan.com"
    }],
    "require": {
        "php": "^7.3|^8.0",
        "ext-gd": "*",
        "laravel/cashier": "^13.13",
        "laravel/framework": "^8.40",
        "laravel/sanctum": "^2.15",
        ...
    },
    "require-dev": {
        "barryvdh/laravel-debugbar": "^3.6",
        "facade/ignition": "^2.5",
        "fakerphp/faker": "^1.9.1",
        ...
    },
    ...
}
````
- `name` tên dự án có dạng `vendor_name/package_name`.
- `type` xác định loại của dự án.
- `description` mô tả gói của bạn.
- `"keywords": ["framework", "laravel"]`: Dòng này xác định các từ khóa (keywords) liên quan đến dự án. Các từ khóa này có thể được sử dụng để tìm kiếm hoặc phân loại dự án. Khi nhìn vào từ khóa, người khác có thể nhanh chóng hiểu được bản chất và mục tiêu của dự án, và có thể dễ dàng tìm kiếm, tương tác và kết nối với cộng đồng liên quan.
- `license`: "MIT": Dòng này xác định giấy phép được sử dụng cho dự án. Trong trường hợp này, dự án được cấp giấy phép MIT. Giấy phép MIT là một giấy phép mở rộng, cho phép sử dụng, sao chép, sửa đổi, hợp nhất, công bố, phân phối, cấp giấy phép và/hoặc bán sao chép của phần mềm.
- Các package yêu cầu của dự án của bạn sẽ được liệt kê trong phần `require` và `require-dev`   

### Cách hoạt động
- Sử dụng terminal, trong thư mục dự án chạy lệnh `composer install`, nó sẽ tải tất cả package được định nghĩa trong file `composer.json` vào thư mục vendor của dự án
- `composer.json` chỉ liệt kê dependency, không chỉ định cụ thể version package sẽ được install, `composer.lock` là nơi chỉ định version nào được install khi chạy `composer install`
- `composer.json` được dùng để chạy `composer install` lần đầu tiên, `composer.lock` được tạo ra sau đó, lưu trữ phiên bản đã được cài đặt. Sau khi đã có `composer.lock`, composer sẽ sử dụng `composer.lock` để xác định phiên bản cài đặt mà không dùng `composer.json` nữa.
- Dùng `composer.lock` để đảm bảo version package của các thành viên trong nhóm là giống nhau.

## 4. Autoloading 
Sau khi đã cài đặt composer, mọi thứ sẽ trở nên dễ dàng hơn. Trong file chính của project, bạn nên thêm dòng lệnh này vào:
````php
include_once './vendor/autoload.php';
````

Toàn bộ package bạn cần đã được thêm vào project và chúng sẵn sàng cho bạn sử dụng. Trong Laravel framework, bạn chỉ cần gõ như sau:
````
composer dump-autoload
````
Tất cả thư viện trong composer đã sẵn sàng để sử dụng trong toàn bộ project. 

## 5. Có nên đẩy file `composer.lock` lên GIT

### Đẩy `composer.lock` lên GIT khi:
- Khi bạn bắt đầu dự án mới hoặc làm việc trên máy tính mới
- Khi bạn cập nhật các gói phụ thuộc bằng Composer, Composer sẽ cập nhật `composer.lock` với phiên bản cụ thể của từng gói. Khi bạn đẩy `composer.lock` lên Git, tất cả thành viên khác của nhóm có thể sử dụng cùng phiên bản các gói phụ thuộc.

### Không đẩy `composer.lock` lên GIT khi:
- Nếu dự án của bạn là một thư viện hoặc gói phụ thuộc được sử dụng bởi dự án khác, hãy không đẩy `composer.lock` lên Git
- Nếu dự án của bạn lớn và có nhiều thành viên, và mỗi thành viên có môi trường phát triển riêng, không đẩy `composer.lock` lên Git sẽ tốt hơn. Điều này cho phép mỗi thành viên sử dụng các phiên bản phụ thuộc phù hợp với môi trường của họ

Lưu ý, nếu bạn không đẩy `composer.lock` lên Git, hãy đảm bảo các thành viên khác trong nhóm có quyền truy cập và biết cách cài đặt các phiên bản phụ thuộc cần thiết.

## 6. Cách chỉ định phiên bản trong `composer.json`

Có 6 cách để chỉ định phiên bản trong file composer.json:

1. Các toán tử `>, <, >=, <= và !=`. Ví dụ `>2.7` có nghĩa là bất kì phiên bản vào trên 2.7, `>2.7 <=3.5` nghĩa là bất kì phiên bản nào trên 2.7 và dưới 3.5, bao gồm cả 3.5.
2. `2.3.*` sẽ bao gồm tất cả phiên bản nào lớn hơn bằng 2.3.0 và nhỏ hơn bằng 2.4.0. Nó tương đương với `>=2.3.0 <2.4`
3. `2.0.0 - 3.0.0` có nghĩa là bất kì phiên bản vào lớn hơn bằng 2.0.0 và nhỏ hơn bằng 3.0.0. Nó tương đương với `>=2.0.0 <=3.0.0`
4. `~3.6` cho phép tất cả phiên bản lớn hơn bằng 3.6, nhưng không bao gồm từ 4.0 trở lên. Nó tương đương với `>=3.6 <4.0`
5. `dev-master` là một định danh cho phiên bản phát triển chính của một gói phụ thuộc. Nó đại diện cho phiên bản mới nhất từ nhánh master trong kho lưu trữ của gói. Tuy nhiên, `dev-master` có thể không ổn định và không nên được sử dụng.
6. Toán tử `^` cho phép tất cả phiên bản ở giữa hai phiên bản chính liền kề nhau. Toán tử `^` được recommend khi dùng để viết code file `composer.json`:

Cụ thể, toán tử `^` trong `composer.json` tuân theo quy tắc sau:
+ Nếu phiên bản được xác định là x.y.z, thì x là phiên bản chính, y là phiên bản phụ, và z là phiên bản vá lỗi (patch version).
+ Toán tử ^ sẽ tương thích với các phiên bản từ x.y.z trở lên, bao gồm cả các phiên bản mới hơn có cùng x nhưng y lớn hơn.
+ Ví dụ, khi bạn sử dụng toán tử `^` với `^1.2.3`, nó sẽ tương thích với các phiên bản từ 1.2.3 đến 2.0.0, bao gồm cả các phiên bản như 1.2.4, 1.3.0, 1.4.0, 1.9.0 và 2.0.0. Tuy nhiên, nó sẽ không bao gồm các phiên bản như 2.0.1, 2.1.0 hoặc bất kỳ phiên bản mới hơn.

## 7. Packagist
Packagist là repository chính để lưu những thông tin về composer package. Bạn có thể vào trang web của packagist để tìm kiếm những library cần thiết và cài đặt chúng một cách nhanh chóng và dễ dàng thông qua composer, hoặc bạn cũng có thể tự tạo một package và chia sẻ với cộng đồng thông qua trang https://packagist.org.

## 8. Các câu lệnh của Composer

### Các Global Option
- `–verbose (-v)`: Hiện message dài
- `–help (-h)`: Hiện thông tin help
- `–quiet (-q)`: Không xuất ra message gì trong khi chạy câu lệnh
- `–no-interaction (-n)`: Không hỏi gì trong khi chạy câu lệnh
- `–working-dir (-d)`: Thiết lập working dir chỉ định
- `–profile`: Hiển thị thời gian và memory được sử dụng
- `–ansi`: Xuất kết quả với encoding là ANSI
- `–no-ansi`: Dừng việc xuất kết quả với encoding là ANSI
- `–version (-V)`: Hiển thị version hiện tại của Composer

### Các câu lệnh
- package cần cài đặt, và cài đặt chúng vào một thư mục nào đó bên trong project.
- `update` : Update những dependencies đã được cài đặt lên version mới nhất, đồng thời update nội dung vào file composer.lock
- `require` : Add hoặc thay đổi nội dung một requirement vào file composer.json. Sau đó package được add vào hoặc thay đổi sẽ được cài đặt hoặc update.
- `global` : Là command cho phép ta thực hiện các command khác như install, update một cách global. Tuy nhiên câu lệnh global yêu cầu ta phải chạy từ thư mục COMPOSER_HOME
- `search` : Cho phép bạn tìm kiếm một package từ trong project của mình, hoặc từ packagist.org
- `show` : Hiện ra những package khả dụng. Ngoài ra nếu đưa thêm tham số là tên package ở cuối thì sẽ hiện ra thông tin về package đó.
- `depends` : Thông tin về những package nào phụ thuộc vào package nào
- `validate` : Kiểm tra xem nội dung file composer.json có hợp hệ hay không
- `status` : Check xem có gì được thay đổi ở bên trong dependencies (do mình thực hiện) hay không.
- `self-update` : Update bản thân composer
- `config` : Chỉnh sửa các setting cơ bản
- `create-project` : Tạo ra một project từ package đã có sẵn. (chẳng hạn như bạn muốn deploy một package là một application, hay muốn develop tiếp từ một package đã có …)
- `dump-autoload` : Update autoloader khi có khi có class mới tong classmap package.
- `licenses` : Hiện thị tên và version của tưng license cho từng package được install.
- `run-script` : Dùng để chạy script một cách thủ công
- `diagnose` : Check xem có vấn đề gì với composer hay không
- `archive` : Tạo ra một file nén (zip hoặc tar) cho một package ở một version chỉ định
- `help` : Hiện thị thông tin về một câu lệnh nào đó
