# Classes, Properties, and Methods

## 1. Extends và Implements

Từ khoá extends và implements phải được viết cùng dòng với tên class.

Dấu mở ngoặc nhọn của class phải đứng trên một dòng riêng. Dấu đóng ngoặc phải được viết ở dòng sau của phần body.

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements \ArrayAccess, \Countable
{
    // constants, properties, methods
}
```

Danh sách những interface được implements có thể được viết trên nhiều dòng, trong đó mỗi dòng theo sau được indent (canh lề) 1 lần. Khi thực hiện việc đó thì tên interface đầu tiên phải được đặt trên 1 dòng mới, và mỗi dòng chỉ được phép chứa tên 1 interface.

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // constants, properties, methods
}
```

## 2. Properties - thuộc tính

Tính Visibility (public, protected, private) phải được khai báo ở mọi properties.

Không được dùng từ khoá var để khai báo một property.

Trên một dòng thì không được khai báo quá một property.

Tên property không nên được prefix bởi dấu gạch dưới \_ để biểu thị tính protected hay private.

Khai báo property giống như sau.

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public $foo = null;
}
```

## 3. Method

Tương tự với property, tính Visibility phải được khao báo ở mọi methods

Tên Method không nên được prefix bởi dấu gạch dưới \_ để biểu thị tính protected hay private.

Khi khai báo tên method thì không được để một khoảng trắng ở phía sau tên method. Dấu mở ngoặc nhọn phải được nằm trên một dòng riêng, và dấu đóng ngoặc phải được nằm trên dòng ngay sau phần thân của method.

Không được có khoảng trắng sau dấu mở ngoặc tròn, và không được có khoảng trắng phía trước dấu đóng ngoặc tròn.

Khai báo một hàm giống như sau. Chú ý đến vị trí của dấu ngặc đơn, dấu phẩy, khoảng trắng và dấu ngoặc nhọn.

```php

<?php
namespace Vendor\Package;

class ClassName
{
    public function fooBarBaz($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```

## 4. Method Arguments

Trong danh sách argument (tham số - đối số) thì không được có khoảng trắng trước mỗi dấu phẩy, và phải có một khoảng trắng sau mỗi dấu phẩy. Giống y như chính tả của ta vậy.

Những tham số mà có giá trị mặc định phải được đặt ở cuối của danh sách tham số. Ví du:

```php

<?php
namespace Vendor\Package;

class ClassName
{
    public function fooBarBaz($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```

Danh sách argument có thể được tách thành nhiều dòng, trong đó mỗi dòng theo sau được indent một lần. Khi làm vậy thì argument đầu tiên trong danh sách phải được đặt ở trên một dòng mới, và mỗi dòng chỉ được phép có một argument.

Khi mà danh sách argument được chia làm nhiều dòng, thì dấu đóng ngoặc tròn và dấu mở ngoặc nhọn phải được đặt cùng nhau trên một dòng, với một khoảng trắng ở giữa.

```php

<?php
namespace Vendor\Package;

class ClassName
{
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = [],
        $arg4 = true
    ) {
        // method body
    }
}
```

## 5. Abstract, final, và static

Khi được sử dụng, abstract và final phải được đặt trước phần khai báo visibility.

Khi được sử dụng, static phải được đặt sau phần khai báo visibility.

```php

<?php
namespace Vendor\Package;

abstract class ClassName
{
    protected static $foo;

    abstract protected function zim();

    final public static function bar()
    {
        // method body
    }
}
```

## 6. Gọi Method và Function

Không được phép có khoảng trắng giữa tên của method hay function và dấu mở ngoặc tròn.

Không được phép có khoảng trắng sau dấu mở ngoặc tròn.

Và không được phép có khoảng trắng trước dấu đóng ngoặc tròn.

Trong danh sách argument, không được phép có khoảng trắng trước mỗi dấu phẩy, và phải có một khoảng trắng sau mỗi dấu phẩy.

```php

<?php
bar (); // sai cái số 1
bar() ; // sai cái số 2
bar( ); // sai cái số 3
bar($arg1 , $arg2); // sai cái số 4

// đúng phải như vầy
bar();
$foo->bar($arg1);
Foo::bar($arg2, $arg3);

```

Danh sách tham số có thể được tách ra thành nhiều dòng, trong đó mỗi dòng theo sau được indent một lần. Khi làm như vậy thì tham số đầu tiên phải được đặt trên một dòng mới, và mỗi dòng chỉ được phép chứa một tham số.

```php

<?php
$foo->bar($firstArgument // sai vì tham số đầu tiên phải ở dòng mới
$longArgument, // sai vì k có 1 canh lề
    $longerArgument, $longerArgument2, // sai vì có 2 tham số trên 1 dòng
    $muchLongerArgument
);

// chuẩn
$foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
);

```
