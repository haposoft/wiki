## 3.3 Iterator

Iterator về bản chất là một interface chuẩn được xây dựng sẵn trong PHP để bạn giễ dàng thao tác với các bộ giá trị.
Cấu trúc của interface iterator trong PHP mặc định khai báo một số phương thức như sau:

```php
<?php
    interface Iterator{
      function rewind();
      function current();
      function key();
      function next();
      function valid();
    }
?>
```
Vậy nên lớp nào sử dụng interface interator đều phải định nghĩa các phương thức trên. Chúng ta sẽ cùng xem xét
một ví dụ về việc sử dụng interator để duyệt mảng trả về từ CSDL.
```php
<?php
    class QueryInterator implements Iterator{
        private $result;
        private $connection;
        private $key=0;
        private $valid;
        private $data;
       
        function __construct($host, $user, $password, $dbname){
            $this->connection = mysql_connect($host,$user, $password);
            mysql_selectdb($dbname,$this->connection);
        }
       
        public function exceute($query){
            $this->result = mysql_query($query,$this->connection);
            if(mysql_num_rows($this->result) > 0){
                $this->next();
            }
        }
       
        public function current(){
            return $this->data;
        }
        public function rewind(){}
        public function key(){
            return $this->key;
        }
       
        public function next(){
            if($this->data = mysql_fetch_assoc($this->result)){
                $this->valid = true;
                $this->key +=1;
            }else{
                $this->valid = false;
            }
        }
       
        public function valid(){
            return $this->valid;
        }
    }
    $q = new QueryInterator("localhost","root","","test");
    $q->exceute("SELECT name FROM ex1");
    echo '<pre>';
    while($q->valid()){
        print_r($q->current());
        $q->next();
    }
    echo '</pre>';
?>
```
### Tìm hiểu thêm ArrayIterator

ArrayIterator về bản chất nó là đối tượng được xây dựng sẵn trong thư viện PHP chuẩn và lớp này sử dụng iterface iterator.

Trong bài viết sau mình sẽ đề cập đến ArrayObject cũng là đối tượng được xây dựng sẵn trong thư viện PHP chuẩn và nó có
phương thức __construct() như sau:
```
__construct ($array, $flags=0, $iterator_class="ArrayIterator")
```
Chúng ta thấy đối số thứ 3 mặc định đã được khởi tạo là "ArrayIterator" để đối tượng dạng mảng có thể sử dụng đối
tượng ArrayIterator thông qua phương thức getIterator().

ArrayItertor định nghĩa cho chúng ta bộ phương thức theo đúng interface iterator để thao tác với mảng.
Bạn có thể xem ví dụ ở bài sau về ArrayObject với phương thức getIterator().