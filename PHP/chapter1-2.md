## Chương 1: OOP và lập trình thủ tục
### 1.Ưu điểm của OOP:
 + Tái sử dụng mã
 + Tái cấu trúc
 + Kế thừa: 
 + Bảo trì dễ dàng
 + Hiệu quả

### 2.Bóc tách đối tượng

### 3.Một số thuật ngữ cơ bản của OO
 + Class(lớp): là khuôn mẫu của đối tượng.
 + Property(thuộc tính): 1 số thông tin trong lớp. Khác các ngôn ngữ khác như C, Java..., PHP không kiểm tra kiểu dữ liệu của biến.
 + Method(phương thức): là function trong class.
 + Encapsulation(Tính đóng gói): các thuộc tính và phương thức được gói trong lớp nên không bị bên ngoài tác động.
 + Inheritance (tính kế thừa): 1 lớp mới được tạo ra bằng cách mở rộng 1 lớp có trước đó.
 + Polymorphism (tính đa hình): các lớp con khi kế thừa lớp cha có thể thay đổi vài thuộc tính và phương thức.
 + Coupling (khớp nối): cách các lớp phụ thuộc lẫn nhau.
 + Design pattern (thiết kế mẫu): thử thuật giải quyết các vấn đề tương tự nhau.
 + Subclass (lớp con): lớp kế thừa từ lớp khác.
 + Superclass(lớp cha): Lớp được lớp khác kế thừa.
 + Instance (thể hiện): Khi tạo mới 1 đối tượng, nó được gọi là 1 thể hiện.  

### 4.Quy tắc viết code
  + giúp viết code dễ dàng và dễ đọc hơn.
  + Tên lớp, tên thuộc tính luôn dùng Camel case để đặt tên.
  + Tên phương thức bắt đầu bằng chữ cái thường, phần còn lại tuân thủ Camel case.
  
## Chương 2: OOP
### 1.Bắt đầu với đối tượng
 + tạo 1 đối tượng bằng từ khóa "class".

```
<?php
  class Emailer
  {
	private $sender;
	private $recipients;
	private $subject;
	private $body;
	function __construct($sender)
	{
	  $this->sender = $sender;
	  $this->recipients = array();
	}
	public function addRecipients($recipient)
	{
	  array_push($this->recipients, $recipient);
	}
	public function setSubject($subject)
	{
	  $this->subject = $subject;
	}
	public function setBody($body)
	{
	  $this->body = $body;
	}
	public function sendEmail()
	{
	  foreach ($this->recipients as $recipient)
	  {
	    $result = mail($recipient, $this->subject, $this->body,"From: {$this->sender}\r\n");
	    if ($result) echo "Mail successfully sent to {$recipient}<br/>";
	  }
	}
  }
?>
```
## 2.Truy cập thuộc tính và phương thức trong lớp
 + sử dụng $this->
 + không thể sử dụng $this ngoài lớp.
 
## 3.Sử dụng đối tượng
 + Phải khai báo trước khi sử dụng.
```
<?
  $emailerobject = new Emailer("hasin@pageflakes.com");
  $emailerobject->addRecipients("hasin@somewherein.net");
  $emailerobject->setSubject("Just a Test");
  $emailerobject->setBody("Hi Hasin, How are you?");
  $emailerobject->sendEmail();
?>
```
 + phải cung cấp chính xác tham số giống với phương thức construct khi khởi tạo đối tượng. Nếu không sẽ gặp lỗi.

### 4.Từ bổ nghĩa
 + private: thuộc tính và phương thức khai báo private không thế được gọi ngoài lớp chứa nó.
 + public: nếu không khai báo gì mặc định thuộc tính và phương thức là public. Khi đó có thể truy cập ở trong hay ở ngoài lớp.
 + protected: thuộc tính và phương thức khai báo protected chỉ được truy cập trong lớp đó hoặc lớp con của nó.

### 5.Constructors và destructors
 + Constructor sẽ được gọi tự động khi tạo mới 1 đối tượng, destrutor được gọi tự động khi kết thúc.
 + Có 2 cách viết phương thức constructor: dùng __construct() hoặc tạo 1 phương thức với tên giống hoàn toàn tên của lớp.
 + 1 lớp có 2 constructor được tạo bởi 2 cách trên sẽ ưu tiên gọi __construct().
 + Tạo phương thức destructor bằng cách đặt tên phương thức là __destruct().

### 6.Lớp Constants
 + Trong lớp, dùng từ khóa "const" để tạo hằng số. Không được sử dụng $ trước hằng số.
   + const ASC = 1; --> đúng
   + const $ASC = 1; --> sai
 + để truy cập hằng bên trong lớp dùng "self::" thay cho ->. 
 + để truy cập hằng bên ngoài lớp dùng toán tử "::" ngay sau tên lớp chứ không phải sau thể hiện của lớp đó.
 
### 7.Kế thừa
  + đối tượng có thể giữ lại toàn bộ chức năng trong lớp cha hoặc ghi đè.
  + Khi truy cập phương thức của lớp cha dùng từ khóa "parent" ngay trước tên phương thức.

### 8.Phương thức ghi đè
 + Các lớp kế thừa có thể ghi đè phương thức được khai báo public hoặc protect của lớp cha.
 + Khi khai báo biến đã có sẵn trong lớp cha thì biến trong lớp con sẽ được truy cập.

### 9.Ngăn ngừa ghi đè
 + Khi phương thức khai báo là "final" sẽ không thể bị ghi đè.

### 10.Ngăn ngừa kế thừa
 + Khi khai báo lớp bằng từ khóa "final" không cho lớp khác kế thừa.

### 11.đa hình

### 12.Interface
 + Interface là 1 lớp trống chỉ gồm các khai báo phương thức.
 + Lớp triển khai interface phải gồm các phương thức được khai báo chính xác như trong interface.
 + dùng từ khóa "implements".

### 13.Lớp abstract
 + Giống interface nhưng cho phép khai báo nội dung trong phương thức.
 + dùng từ khóa "extended".
 + có thể dùng abstract và interface đồng thời.
```
<?php
  include("interface.dbdriver.php");
  include("abstract.reportgenerator.php");
  class MySQLDriver extends ReportGenerator implements DBDriver
  {
	public function connect()
    {
    //connect to database
    }
    public function execute($query)
	{
	//execute the query and output result
	}	
  }
?>
```

 + không được khai báo lớp abstract vời từ khóa "final".
 + Khi khai báo phương thức với từ khóa abstract thì trong lớp con phải ghi đè.
 + Phương thức abstract khi khai báo phải để trống.

### 14.Phương thức và thuộc tính tĩnh
 + giống thành phần global.
 + Có thể truy cập phương thức và thuộc tính tĩnh mà không cần tạo thể hiện của lớp bằng toán tử "::"
```
<?php
  //class.dbmanager.php
  class DBManager
  {
	public static function getMySQLDriver()
    {
    //instantiate a new MySQL Driver object and return
	}
    public static function getPostgreSQLDriver()
	{
	//instantiate a new PostgreSQL Driver object and return
 	}
	public static function getSQLiteDriver()
	{
	//instantiate a new MySQL Driver object and return
	}
  }
  //test.dbmanager.php
  include_once("class.dbmanager.php");
  $dbdriver = DBManager::getMySQLDriver();
?>
?>
```

 + Lợi ích là tiết kiệm bộ nhớ khi không phải khởi tạo đối tượng.
 + Không thể sử dụng $this trong phương thức tĩnh vì khi đối tượng không được khởi tạo thì $this không tồn tại.Thay vào đó dùng "self".
```
<?php
  //class.statictester.php
  class StaticTester
  {
	private static $id=0;
 	function __construct()
    {
	  self::$id +=1;
	}
	public static function checkIdFromStaticMehod()
	{
	  echo "Current Id From Static Method is ".self::$id."\n";
	}
	public function checkIdFromNonStaticMethod()
	{
	  echo "Current Id From Non Static Method is ".self::$id."\n";
	}
  }
  $st1 = new StaticTester();
  StaticTester::checkIdFromStaticMehod();
  $st2 = new StaticTester();
  $st1->checkIdFromNonStaticMethod(); //returns the val of $id as 2 the val of $id as 2
  $st1->checkIdFromStaticMehod();
  $st2->checkIdFromNonStaticMethod();
  $st3 = new StaticTester();
  StaticTester::checkIdFromStaticMehod();
?>
```
 + Trừ khi có mục đích cụ thể, không nên dùng thành phần tĩnh.

### 15.Phương thức Accessor
 + là phương thức chỉ dùng để nhận và thiết lập giá trị thuộc tính trong lớp.
```
<?php
  class Student
  {
	private $name;
	private $roll;
	public function setName($name)
	{
	  $this->name= $name;
	}
	public function setRoll($roll)
	{
	  $this->roll =$roll;
	}
	public function getName()
	{
	  return $this->name;
	}
	public function getRoll()
	{
	  return $this->roll;
	}
  }
?>
```
 + quy tắc đặt tên cho phương thức accessor: bắt đầu bằng get hoặc set, theo sau là tên biến với chữ cái đầu tiên viết hoa.
   + VD: setName(), getEmail()...

### 16.Phương thức Magic để set/get thuộc tính
 + __get(), __set()
```
<?
//class.student.php
  class Student
  {
	private $properties = array();
	function __get($property)
	{
	  return $this->properties[$property];
	}
	function __set($property, $value)
	{
	  $this->properties[$property]="AutoSet {$property} as: ".$value;
	}
  }

  $st = new Student();
  $st->name = "Afif";
  $st->roll=16;
  echo $st->name."\n";
  echo $st->roll;
?>
```
 + Vì thuộc tính không tồn tại nên __set() sẽ được gọi và gán giá trị cho thuộc tính mới.

### 17.Phương thức Magic cho Overloading
 + dùng để truy nhập phương thức không tồn tại trong lớp.
 + __call() cung cấp hành động hoặc trả về giá trị khi gọi phương thức không tồn tại.
 + __call() nhận 2 tham số là tên của phương thức và mảng các đối số truyền cho phương thức không xác định.
```
<?php
  class Overloader
  {
	function __call($method, $arguments)
	{
	  echo "You called a method named {$method} with the following arguments <br/>";
	}
  }
  $ol = new Overloader();
  $ol->access(2,3,4);
  $ol->notAnyMethod("boo");
?>
```

