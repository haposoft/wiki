# Dependency Injection trong PHP

## 1. Khái niệm liên quan

Dependency Inversion là một nguyên lý để thiết kế và viết code trong 5 nguyên lý S.O.L.I.D do Robert C.Martin viết. Các khái niệm như Inversion of Control, Dependency Inversion, Dependency Injection Container theo đều được phát triển để thực hiện hóa nguyên lý này.

Dependency Injection là một kỹ thuật trong lập trình hướng đối tượng, được sử dụng để giảm thiểu sự phụ thuộc giữa các thành phần trong một hệ thống phần mềm. Nó cho phép chúng ta tạo ra các đối tượng phụ thuộc vào các đối tượng khác thông qua việc "cung cấp" các đối tượng này (dependencies) vào đối tượng đang được tạo ra, thay vì tạo ra các đối tượng đó trong đối tượng hiện tại.

## 2. Các cách Dependency Injection

Có 3 dạng Dependency Injection:

Constructor Injection: Các dependency sẽ được container truyền vào (inject vào) 1 class thông qua constructor của class đó. Đây là cách thông dụng nhất.

```php
<?php

class A {
    public $b;

    public function __construct(B $b)
    {
        $this->b = $b;
    }
}

```

Setter Injection: Các dependency sẽ được truyền vào 1 class thông qua các hàm Setter.

```php
<?php

class A {
   public $b;

   public function __construct()
   {

   }

   public function setB(B $b)
   {
       $this->b = $b;
   }
}

```

Interface Injection: Class cần inject sẽ implement 1 interface. Interface này chứa 1 hàm tên Inject. Container sẽ injection dependency vào 1 class thông qua việc gọi hàm Inject của interface đó. Đây là cách rườm rà và ít được sử dụng nhất.

## 3. Ưu điểm và khuyết điểm của DI

### Ưu điểm

Giảm sự kết dính giữa các module

Code dễ bảo trì, dễ thay thế module

Rất dễ test và viết Unit Test

Dễ dàng thấy quan hệ giữa các module (vì các dependecy đều được inject vào constructor)

### Khuyết điểm

Khái niệm DI khá khó cho các developer mới

Sử dụng interface nên đôi khi sẽ khó debug, do không biết chính xác module nào được gọi

Các object được khởi tạo toàn bộ ngay từ đầu, có thể làm giảm performance

Làm tăng độ phức tạp của code

## 4. Ví dụ

### Không sử dụng DI

class Member

```php
<?php

class Member {
    private $name;
    private $position;

    public function __construct($name, $position){
        $this->name = $name;
        $this->position   = $position;
    }

   public function getName()
   {
       return $this->name;
   }
}

```

class Company

```php
<?php

class Company {
    private $name;
    private $members;

    public function __construct($name){
        $this->name = $name;
    }

    public function addMember($name, $position)
    {
        $member = new Member($name, $position);
        $this->members[] = $member;
    }

    public function getMembers()
    {
        return $this->members;
    }
}

```

Add Member

```php
<?php

$company = new Company("hapo");
$company->addMember("Pham Dat", "Dev");

```

### Sử dụng DI

class Company

```php
<?php

class Company {
    private $name;
    private $members;

    public function __construct($name){
        $this->name = $name;
    }

    public function addMember(Member $member)
    {
        $this->members[] = $member;
    }

    public function getMembers()
    {
        return $this->members;
    }
}

```

Add Member

```php
<?php

$company = new Company("hapo");
$member = new Member("Pham Dat", "Dev");
$company->addMember($member);

```
