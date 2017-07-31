### 3.6 Truy cập vào các Object trong kiểu mảng

Trong phần trên chúng ta đã học được làm thế nào để truy cập vào bất kỳ mảng trong phong cách OO.
Vậy làm cách nào nếu chúng ta muốn truy cập vào bất kỳ đối tượng trong kiểu mảng? Vâng, PHP cung cấp cơ sở đó.
Điều mà bạn phải làm là thực hiện giao diện ArrayAccess trong class của bạn.

Giao diện ArrayAccess có bốn Methods mà bạn phải thực hiện trong class. Các Methods này là offsetExists(), offsetGet(),
offsetSet(), offsetUnset().
Hãy tạo ra một lớp mẫu thực hiện giao diện ArrayAccess.
```php
<?php
    class users implements ArrayAccess{
        private $users;
        public function __construct(){
            $this->users = array();
        }
        public function offsetExists($key){
            return isset($this->users[$key]);
        }
        public function offsetGet($key){
            return $this->users[$key];
        }
        public function offsetSet($key, $value){
            $this->users[$key] = $value;
        }
        public function offsetUnset($key){
            unset($this->users[$key]);
        }
    }
    $users = new users();
    $users['afif']="mayflower@phpxperts.net";
    $users['hasin']="hasin@pageflakes.com";
    $users['ayesha']="florence@phpxperts.net";
    echo $users['afif'];
?>
```

Output: *mayflower@phpxperts.net*.