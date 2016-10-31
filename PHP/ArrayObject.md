## 3.4 ArrayObject

Một đối tượng hữu ích khác được giới thiệu trong PHP5 là đối tượng mảng ArrayObject, đây là đối tượng được xây dựng sẵn
trong thư viện PHP chuẩn, điều này giúp bạn có thể truy cập mảng theo kiểu hướng đối tượng. Bạn có thể tạo ra đối tượng
dạng mảng vô cùng đơn giản với cấu trúc ArrayObject. Sau đây chúng ta sẽ tìm hiểu một số phương thức hữu ích thường dùng
cho ArrayObject:

**append()**

Phương thức này sẽ thêm phần tử vào cuối mảng

```php
<?php
    $s = new ArrayObject(array("first","second", "third"));
    $s->append("four");
    $s->append(array("five","six"));
    echo "<pre>";
    print_r($s);
    echo "</pre>";
?>
```

**getIterator()**

Phương thức getInterator sẽ tạo ra một iterator thay thế đối tượng mảng, iterator sẽ cung cấp một bộ phương thức giúp
duyệt mảng một cách giễ dàng, phương thức không có đối số

```php
<?php
    $s = new ArrayObject(array("1"=>"one", "2"=>"two", "3"=>"three"));
    $iterator = $s->getIterator();
    while($iterator->valid()){
        echo $iterator->key()," -> ",$iterator->current()," ";
        $iterator->next();
    }
?>
```

**offsetExists()**

Phương thức getInterator sẽ tạo ra một iterator thay thế đối tượng mảng, iterator sẽ cung cấp một bộ phương thức
giúp duyệt mảng một cách giễ dàng, phương thức không có đối số

```php
<?php
    $s = new ArrayObject(array("1"=>"one", "2"=>"two", "3"=>"three"));
    $iterator = $s->getIterator();
    while($iterator->valid()){
        echo $iterator->key()," -> ",$iterator->current()," ";
        $iterator->next();
    }
?>
```
**offsetGet()**

Phương thức trả về giá trị phần tử giựa theo chỉ mục
```php
<?php
    $s = new ArrayObject(array("one","two","3"=>"three"));
    var_dump($s->offsetGet(0));
    var_dump($s->offsetGet("3"));
?>
```
**offsetSet()**
Phương thức này sẽ tạo hoặc thay đổi giá trị của phần tử giựa vào chỉ mục

```php
<?php
    class ex1{
      public $property1 = 'value1';
    }
    $s = new ArrayObject(new ex1());
    $s->offsetSet("property1","value2");
    $s->offsetSet(4,"value4");
    $s->offsetSet(5,array(1=>"one",2=>"two"));
    echo '<pre>';
    print_r($s);
    echo '</pre>';
       
    $s = new ArrayObject(array("one","two"));
    $s->offsetSet(1,"four");
    $s->offsetSet(null,"three");
    echo '<pre>';
    print_r($s);
    echo '</pre>';
?>
```
**offsetUnset()**
Phương thức này sẽ gỡ một phần tử nào đó giựa theo chỉ mục
```php
<?php
    $s = new ArrayObject(array("one","two","3"=>"three","four"));
    $s->offsetUnset(3);
    echo "<pre>";
    print_r($s);
    echo "</pre>";
?>
```
Còn rất nhiều các phương thức khác để thao tác với đối tượng dạng mảng, cách thức sử dụng cũng không khác gì nhiều so
.với các hàm thao tác với mảng trong PHP bạn có thể tham khảo tại php.net.