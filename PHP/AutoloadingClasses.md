## 3.9 Autoloading Classes

Với cách viết thông thường thì khi bạn gọi một lớp nào đó từ file khác bạn phải dùng hàm include tới từng file một sau
đó mới có thể sử dụng. Đối với những dự án lớn có một cách thực hành tốt khác trong PHP đó là bạn chỉ tải file chứa
class khi cần thiết có nghĩa là bạn không cần phải khai báo include bằng tay nữa mà nó sẽ được thực hiện tự động,  
tính năng đang được nói đến ở đây là autoloading classes được giới thiệu trong PHP5.

Chúng ta hãy cùng xem xét ví dụ sau để hiểu rõ hơn về vấn đề này:

Tạo file class.auto.php như sau:
```php
<?php
    class Auto{
     public $a ='Hoang';
     public function show(){
        echo $this->a;
     }
    }
?>
```
Tạo file class.auto2.php như sau:
```php
<?php
    class Auto{
     public $a ='Nguyen Huy Hoang';
     public function show(){
        echo $this->a;
     }
    }
?>
```
Hai file class.auto.php và class.auto2.php nằm cùng trong thư mục, giả sử ở đây là thư mục classes.

Tạo file a.php nằm cùng cấp với thư mục classes.

Với cách thông thường chúng ta sẽ làm như sau:
```php
<?php
    inlude_once 'classes/class.auto.php';
    inlude_once 'classes/class.autos.php';
    $s = new Auto();
    $s->show();
    $s2 = new Auto2();
    $s2->show2();
?>
```
Với cách sử dụng auto load chúng ta sẽ làm như sau:
```php
<?php
    function __autoload($class){
        include_once "classes/class.$class.php";
    }
    $s = new Auto();
    $s->show();
    $s2 = new Auto2();
    $s2->show2();
?>
```
Với cách thực hiện này bạn có thể gọi tùy ý một lớp bất kỳ mà không cần quan tâm file đó đã được include hay chưa.
