## 1. Composer là gì
[Composer](https://getcomposer.org/) Là công cụ để quản lý package hay library PHP.  
Composer sẽ cài đặt những libraries vào một thư mục nào đó nằm bên trong project bạn đang làm việc.  
Về cơ cản, Composer sẽ không cài đặt global, chính vì thế nó còn được gọi là Dependency Manager.  
(Những package được cài đặt được gọi là Dependency, còn Composer là công cụ quản lý các Dependency)  
Composer tương tự bundler của Ruby hay npm của NodeJS
## 2. Cách cài đặt
Composer phiên bản hiện tại yêu cầu phiên bản PHP >= 5.3.2  
Thông tin chi tiết về hướng dẫn cài đặt Composer có thể xem ở [đây](https://getcomposer.org/download/)
## 3. Composer.json và composer.lock
`composer.json` : Là nơi ta khai báo những dependencies dùng trong project, những thông tin về tên, phiên bản, licenses, source … Nội dung được viết theo JSON format.  
VD:  
 
    {
        "name": "wataridori/bphalcon",
        "type": "project",
        "description": "A small library which implement some features to phalcon",
        "license": "GPL-3.0",
        "authors": [
            {
                "name": "Phan Minh Truong",
                "email": "truongpm@haposoft.com"
            }
        ],
        "require": {
            "php": ">=5.4"
        }
    }
    
 `composer.lock` : Là nơi lưu trữ thông tin về dependencies đã được cài đặt. Ví dụ khi bạn dùng lệnh install để cài đặt lần đầu thì composer sẽ đọc thông tin về dependencies ở trong file composer.json, sau đó cài đặt và tạo ra file composer.lock để lưu thông tin cụ thể về những dependencies đó  
 ## 4. Packagist
 [Packagist]( https://packagist.org): Là repository chính để lưu những thông tin về composer package  
 Đây là nơi ta có tìm kiếm những library cần thiết và cài đặt chúng một cách nhanh chóng và dễ dàng thông qua composer
## 5. Các câu lệnh của Composer

### a. Các Global Option
`verbose (-v)` : Hiện message dài  
`help (-h)` : Hiện thông tin help  
`quiet (-q)` : Không xuất ra message gì trong khi chạy câu lệnh  
`no-interaction (-n)` : Không hỏi gì trong khi chạy câu lệnh  
`working-dir (-d)` : Thiết lập working dir chỉ định  
`profile` : Hiển thị thời gian và memory được sử dụng  
`ansi` : Xuất kết quả với encoding là ANSI  
`no-ansi` : Dừng việc xuất kết quả với encoding là ANSI  
`version (-V)` : Hiển thị version hiện tại của Composer  

### b. Các local Option
`init` : Tạo ra file composer.json nhằm khai báo các thông tin cho package  
`install` : Đọc thông tin từ file composer.json tại thư mục đang đứng, tổng hợp các package cần cài đặt, và cài đặt chúng vào một thư mục nào đó bên trong project.  
`update` : Update những dependencies đã được cài đặt lên version mới nhất, đồng thời update nội dung vào file composer.lock  
`require` : Add hoặc thay đổi nội dung một requirement vào file composer.json. Sau đó package được add vào hoặc thay đổi sẽ được cài đặt hoặc update.
`global` : Là command cho phép ta thực hiện các command khác như install, update một cách global. Tuy nhiên câu lệnh global yêu cầu ta phải chạy từ thư mục COMPOSER_HOME  
`search` : Cho phép bạn tìm kiếm một package từ trong project của mình, hoặc từ packagist.org  
`show` : Hiện ra những package khả dụng. Ngoài ra nếu đưa thêm tham số là tên package ở cuối thì sẽ hiện ra thông tin về package đó.  
`depends` : Thông tin về những package nào phụ thuộc vào package nào  
`validate` : Kiểm tra xem nội dung file composer.json có hợp hệ hay không  
`status` : Check xem có gì được thay đổi ở bên trong dependencies (do mình thực hiện) hay không.  
`self-update` : Update bản thân composer  
`config` : Chỉnh sửa các setting cơ bản  
`create-project`: Tạo ra một project từ package đã có sẵn. (chẳng hạn như bạn muốn deploy một package là một application, hay muốn develop tiếp từ một package đã có)  
`dump-autoload` : Update autoloader khi có khi có class mới tong classmap package.  
`run-script` : Dùng để chạy script một cách thủ công  
`diagnose`: Check xem có vấn đề gì với composer hay không  
`archive` : Tạo ra một file nén (zip hoặc tar) cho một package ở một version chỉ định  
