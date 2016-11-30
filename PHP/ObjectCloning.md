## 3.8 Object Cloning

Ta xét ví dụ sau:
```php
<?php
    class Student(){
        public $name;
        public function setName($value){
            $this->name = $value;
        }
        public function getName(){
            return $this->name;        
        }
    }
    $object1 = new Student();
    $object1->setName("Nguyen Huy Hoang");
    
    $object2 = $object1;
    $object2->setName("Nguyen Thi Huong");
    
    echo $object1->getName();
?>
```

Theo bạn kết quả echo ra giá trị nào.

Vâng kết quả echo ra: Nguyen Thi Huong. Đơn giản là như thế này: Khi các bạn sử dụng $object2 = $object1, nếu một trong
hai đối tượng này thay đổi thì đối tượng kia cũng thay đổi theo.

Để muốn sử dụng phép gán các đổi tượng thay đổi không phụ thuộc vào nhau, mà nó mang tính độc lập. Đó là sử dụng Cloning
ở PHP. Khi các bạn sử dụng clone thì các đối tượng thay đổi không phụ thuộc vào nhau, mà nó mang tính độc lập.

```php
<?php
    class Student(){
        public $name;
        public function setName($value){
            $this->name = $value;
        }
        public function getName(){
            return $this->name;        
        }
    }
    $object1 = new Student();
    $object1->setName("Nguyen Huy Hoang");
    
    $object2 = clone $object1;
    $object2->setName("Nguyen Thi Huong");
    
    echo $object1->getName();
?>
```
Output: Nguyen Thi Huong.

Qua các ví dụ trên. Cho thấy, việc sử dụng từ khóa clone trong PHP cho phép ta hoàn toàn có thể tạo ra một đối tượng mới
từ đối tượng có sẵn. Mà không ảnh hướng hay làm mất đi dữ liệu của đối tượng ban đầu. 
Việc không phải khởi tạo đối tượng, sẽ tiết kiệm bộ nhớ. Điều này giúp ứng dụng của chúng nhanh hơn.

