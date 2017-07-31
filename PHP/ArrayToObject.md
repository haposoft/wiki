### 3.5 Array to Object

Chúng ta có thể truy cập vào bất kỳ phần tử mảng, ví dụ $array[$key]. Tuy nhiên, nếu chúng ta muốn truy
cập nó như thế này, $array->key style? Nó rất dễ dàng và chúng ta có thể làm điều đó bằng cách mở rộng ArrayObject.
Hãy xem cách sử dụng các ví dụ sau đây.
```php
<?php
    class ArrayToObject extends ArrayObject{
        public function __get($key){
            return $this[$key];
        }
        public function __set($key,$val){
            $this[$key] = $val;
        }
    }
?>
```
bạn hãy nhìn cách nó hoạt động dưới đây:
```php
<?php
    $users = new ArrayToObject(array("hasin"=>"hasin@pageflakes.com",
    "afif"=>"mayflower@phpxperts.net","ayesha"=>"florence@pageflakes.net"));
    echo $users->afif;
?>
```
và Output sẽ là *mayflower@phpxperts.net*.

Đây là cách mà bạn muốn chuyển đổi các đinh dạng mảng bất kỳ thành một đối tượng.