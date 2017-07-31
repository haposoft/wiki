## 3.1 Class Information Functions
Nếu bạn muốn tìm kiếm hoặc thông kê các thông tin liên quan đến một class bất kỳ, các function này sẽ cho bạn hầu hết các thông tin của class mà bạn muốn. Nhưng có một cách khác đó là sử dụng API nhưng tôi sẽ không đề cập tới ở đây.

### 3.1.1 Kiểm tra sự tồn tại của một Class
Khi bạn cần kiểm tra một class nào đó có tồn tại hay không thì bạn có thể sử dụng hàm `class_exists()`. Như ví dụ dưới đây:
```php
<?php
   if (class_exists('MyClass')) {
      $myclass = new MyClass();
   }
?> 
```
Hàm `class_exists()` trả về TRUE nếu MyClass là một lớp đã được định nghĩa, nếu không là  sẽ trả về FALSE.
### 3.1.2 Tìm các class đã được khai báo trong script hiện tại.
Trong một số trường hợp bạn cần kiểm tra xem class nào đó được định nghĩa chưa. Bạn có thể sử dụng hàm get_declared_classes().
Hàm get_declared_classes() trả về một mảng tên của các lớp đã được khai báo trong script hiện tại.
```php
<?php
   print_r(get_declared_classes());
?> 
```
Bạn sẽ thấy trên màn hình một danh sách các class hiện có sẵn.
### 3.1.3 Kiểm tra sự tồn tại của Methods and Properties.
Để kiểm tra sự tồn tại của một Methods hoặc Property có tồn tại trong một class, bạn có thể sử dụng hàm method_exists()
và property_exists(). Xin lưu ý rằng các hàm này thực hiện được khi các thuộc tính và phương thức được định nghĩa
là plubic.
### 3.1.4 Kiểm tra kiểu của class
Trong một số trường hợp bạn cần phải kiểm tra lớp cha hoặc lớp của một đối tượng nào đó, PHP cung cấp hàm is_a()
kết quả trả về là true/false.
```php
<?php
    is_a ( $object, $class_name )
?>
```
Trả về TRUE nếu đối tượng đã cho là của class_name này hoặc có lớp cha là lớp class_name, nếu không là trả về FALSE.
Ví dụ:
```php
<?php
    class HoangBK
       {
          var $HoangBK = 'fromatoz';
       }
       
       // tạo một đối tượng mới
       $WF = new HoangBK();
       
       if (is_a($wf, 'HoangBK')) {
          echo "\$wf vẫn là HoangBK";
       }
?>
```
Output: `$wf vẫn là HoangBK`

### 3.1.5 Tìm tên các class
Trong ví dụ trước chúng ta đã kiểm tra được các đối tượng có thuộc một class mà ta biết trước không. Nếu bạn muốn biết
tên của class của đối tượng thì phải làm sao? bạn đừng lo lắng PHP hỗ trợ cho chúng ta hàm get_class().
```php
<?php
    class ParentClass{}
    class ChildClass extends ParentClass{}
    $cc = new ChildClass();
    echo get_class($cc)
?>
```
Kết quả trả về là `ChildClass` (dĩ nhiên rồi). Tuy nhiên hàm get_class() lại có 2 cách sử dụng đó là sử dụng bên trong
lớp và bên ngoài lớp.

Nếu sử dụng bên ngoài lớp thì đối số của hàm sẽ là đối tượng cần lấy thông tin(getClass1() ở ví dụ dưới).

Nếu sử dụng bên trong lớp thì hàm có thể không cần đối số khi này hàm sẽ trả về tên lớp chứa nó, trường hợp nếu hàm sử dụng $this làm đối số thì hàm sẽ trả về tên lớp ở đối tượng nào gọi nó ví dụ ta gọi nó ở các lớp kế thừa thì hàm sẽ trả về tên lớp kế thừa (getClass2() ở ví dụ dưới). Xem ví dụ sau để hiểu rõ điều này:

```php
<?php
    class ParentClass{
        public function getClass1(){
          return get_class($this);  //using "$this"
        }
        public function getClass2(){
          return get_class();  //using "no $this"
        }
    }
    class ChildClass extends ParentClass{}
    $cc = new ChildClass();
    echo get_class($cc); // Output: ChildClass
    echo $cc->getClass1(); // Output: ChildClass
    echo $cc->getClass2(); // Output: ParentClass
?>
```


