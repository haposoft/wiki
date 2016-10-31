## 3.10 Medtho Chaining

Chuỗi phương thức (method chaining) là một cách viết hầu hết các framework hiện nay đang sử dụng, hôm nay mình sẽ hướng
dẫn các bạn cách để tạo ra các phương thức như thế này. Và một điều bất ngờ là việc này vô cùng, vô cùng đơn giản. Không
nói quá nhá, chúng ta chỉ cần nắm được một số khái niệm cơ bản là đủ để có thể xây dựng được các phương thức như thế này rồi.

Trước tiên chúng ta sẽ cùng nhau tìm hiểu đến phương thức __call(), đây là một trong các
phương thức ma thuật (magic method) của PHP, phương thức này là cái cốt lõi để chúng ta xây dựng nên chuỗi
phương thức (method chaining). Vậy nó là gì và nó hoạt động như thế nào? Nói một cách đơn giản và dễ hiểu
thì nó sẽ được định nghĩa một cách ngắn gọn như thế này 

- Phương thức __call() được kích hoạt khi chúng ta gọi một phương thức không có trong class. Nghĩa là khi
chúng ta gọi bất kỳ một phương thức nào mà phương thức đó không có trong class thì mặc nhiên PHP sẽ gọi đến
phương thức __call() của class đó cho chúng ta. 

Cách viết thông thường:
```php
<?php
    db = new Database();
    $db->select('username'); 
    $db->from('users'); 
    $db->where('user_id = 1'); 
    $db->order_by('id DESC'); 
    $db->excute();
?>
```
Cách viết theo chuỗi phương thức:
```php
<?php
    $db = new Database(); 
    
    $db->select('username') 
    ->from('users')->where('user_id = 1')->order_by('id DESC') 
    ->execute();
?>
```
Bạn thích cách viết nào hơn?

Cách xây dựng 
- Như mình đã nói ở trên việc xây dựng chuỗi này vô cùng dễ dàng và đây là toàn bộ class để thực hiện được một
chuỗi phương thức như trên

```php
<?php
    class Database{ 
        public $select; 
        public $from; 
        public $where; 
        public $order_by; 
    
        public function __call($name, $arguments){ 
            $this->$name = $arguments[0]; 
            return $this; 
        } 
    
        public function execute(){ 
            echo 'SELECT ' . $this->select 
            . ' FROM ' . $this->from 
            . ' WHERE ' . $this->where 
            . ' ORDER BY ' . $this->order_by; 
        } 
    }
?>
```
- Mổ xẽ class trên một chút nào: 
Các bạn có thể thấy class trên chỉ có 1 phương thức __call() và một phương thức execute() nhưng không hề có các
phương thức select, from, where... Đối chiếu lại với lý thuyết bên trên một chút, chúng ta sẽ thấy là khi gọi một trong
các phương thức select, from, where... vì các phương thức này không nằm trong class nên __call() sẽ được gọi thay thế
và sẽ được truyền vào 2 tham số $name, $arguments trong đó $name là tên phương thức và $arguments là mảng tham số.
Và công việc còn lại chỉ là xử lý các dữ liệu ở trong __call(), ở đây đơn giản là mình chỉ gán các giá trị vào các
thuộc tính của class và sau đó gọi đến execute(). 

- Đơn giản không nào, các bạn có thể dùng cách viết này ứng dụng vào xây dựng class hoặc thay đổi lại một chút
cách viết code của mình.