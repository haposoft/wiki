### 3.7 Serialization

Chúng t ađã học được cách tạo ra các đối tượng và thao tác chúng. Bây giờ những gì sẽ xảy ra nếu bạn cần phải lưu bất kỳ
trạng thái của đối tượng và lấy nó sau này chính xác theo đúng format đó? Trong PHP, bạn có thể đạt được chức năng này
bằng cách tuần tự. Tuần tự hóa là một quá trình giữ trạng thái của một đối tượng trong bất kỳ format, hoặc tập tin
vật lý hoặc trong các biến. Để lấy lại trạng thái của đối tượng đó, một quá trình được sử dụng mà được gọi là
"unserialization". Bạn có thể sắp đặt bất kỳ đối tượng sử dụng hàm serialize(). Hãy xem cách chúng tôi Serialization một đối tượng:

```php
<?php
    class SampleObject{
        public $var1;
        private $var2;
        protected $var3;
        static $var4;
        public function __construct(){
            $this->var1 = "Value One";
            $this->var2 = "Value Two";
            $this->var3 = "Value Three";
            SampleObject::$var4 = "Value Four";
        }
    }
    $so = new SampleObject();
    $serializedso =serialize($so);
    file_put_contents("text.txt",$serializedso);
    echo $serializedso;
?>
```
Các kịch bản sẽ tạo ra một chuỗi, PHP hiểu làm thế nào để unserialize. ểĐ lấy đối tượng tuần tự và chuyển đổi thành một
đối tượng PHP sử dụng được. Hãy nhớ rằng các tập tin, class mà bạn unserializng phải được nạp trước.

```php
<?php
    include_once("class.sampleobject.php");
    $serializedcontent = file_get_contents("text.txt");
    $unserializedcontent = unserialize($serializedcontent);
    print_r($unserializedcontent);
?>
```
Output:
```
SampleObject Object
    (
        [var1] => Value One
        [var2:private] => Value Two
        [var3:protected] => Value Three
    )
```
Xin lưu ý rằng tất cả các biến giữ giá trị của chúng, mà đã được thiết lập trước khi Serializing, ngoại trừ static.
Bạn không thể lưu trạng thái của một biết static bằng cách Serializing
### Magic Methods in Serialization

Ở chương trước chúng ta đã làm quen với Magic Methods. Magic Methods là cách chúng ta dùng nhằm tránh quá tài các
Properties và Methods như sử dụng __get, __set, và __call. Đối với Serialization, bạn được phép sử một số Magic Methods.
PHP5 cung cấp 2 magic methods cho mục đích đặt tên __sleep và awake. Những methods này đưa ra một số quyền kiểm soát
toàn bộ quá trình.

Như các bạn đã biết bạn không thể lưu trạng thái của một biết static bằng cách Serializing. Tuy nhiên, chúng ta có thể
làm cho nó xảy ra, chúng ta hãy xem đoạn mã sau.

```php
<?php
    class SampleObject{
        public $var1;
        private $var2;
        protected $var3;
        public static $var4;
        private $staticvars = array();
        public function __construct(){
            $this->var1 = "Value One";
            $this->var2 = "Value Two";
            $this->var3 = "Value Three";
            SampleObject::$var4 = "Value Four";
        }
        public function __sleep(){
            $vars = get_class_vars(get_class($this));
            foreach($vars as $key=>$val){
                if (!empty($val))
                $this->staticvars[$key]=$val;
            }
            return array_keys( get_object_vars( $this ) );
        }
        public function __wakeup(){
            foreach ($this->staticvars as $key=>$val){
                $prop = new ReflectionProperty(get_class($this), $key);
                $prop->setValue(get_class($this), $val);
            }
            $this->staticvars=array();
        }
    }
?>
```
Điều gì xảy ra nếu chúng ta Serializing đối tượng, viết nó vào tập tin và sau đó lấy ra? Bạn sẽ tìm thấy những giá trị
static vẫn còn tồn tại những giá trị cuối. Hàm __sleep thực hiện tất cả các hoạt động cần thiết. Nó tìm kiếm các
public properties với các giá trị và lưu trữ tên biến, khi nó tìm thấy một biến private thành staticvars .
Sau này khi ai đó cố gắng để unserialize đối tượng, nó lấy mỗi giá trị từ staticvars và viết nó vào property.

__sleep() được thực thi khi đối tượng được lưu tạm thời thành chuỗi với hàm serialize(), phương thức sẽ trả về mảng các
với các phần tử là các thuộc tính sẽ được lưu vào chuỗi với hàm serialize()

__wakeup() được thực thi khi hàm unserialize được gọi, phương thức sẽ phục hồi lại đối tượng được lưu trong chuỗi
trả về từ hàm serialize()
```php
<?php
    class Student{
       private $full_name='';
       private $score = 0;
       private $grades = array();
       public function __construct($full_name, $score, $grades){
            $this->full_name = $full_name;
            $this->grades = $grades;
            $this->score = $score;
       }
       public function show(){
            echo $this->full_name;
            print_r( $this->grades);
       }
       function __sleep(){
            echo 'Going to sleep...';
            return array('full_name', 'grades', 'score');
       }
       function __wakeup(){
            echo 'Waking up ...';
       }
    }
?>
```

Ở trên __sleep() trả về mảng với 3 tham số là 3 thuộc tính sẽ được lưu tạm thời với hàm serialize()

Tạo file a.php khởi tạo đối tượng, chạy hàm serialize và lưu chuỗi thông tin vào file string.txt

```php
<?php
    include 'student.class.php';
    $student = new Student('Nguyen Huy Hoang','a',array('a'=>90,'b'=>100));
    $student->show();
    $s = serialize($student);
    file_put_contents('string.txt',$s);
?>
```

Chạy file trên trong trình duyệt chúng ta sẽ nhận được "Nguyen Huy HoangaArray ( [a] => 90 [b] => 100 ) Going to sleep...",
 ta thấy phương thức __sleep() đã được thực thi.
 
 Tạo file b.php để phục hồi phương thức từ chuỗi tạm thời
 
 ```
 include 'student.class.php';
 $s = file_get_contents('string.txt');
 $a = unserialize($s);
 $a->show();
 ```
 Chạy file trên trong trình duyệt chúng ta sẽ nhận được "Waking up ...Nguyen Huy HoangaArray ( [a] => 90 [b] => 100 )",
 ta thấy đối tượng đã được phục hồi và phương thức __wakeup đã được thực thi.

