# Files

## php tags
## Đối với file PHP
- Nguyên tắc 1: File PHP chỉ được phép sử dụng <?php và <?=. <?php được sử dụng để mở đầu cho code PHP, và <?= là cú pháp short-echo (thay vì code là <?php echo $a ?>, bạn có thể code là <?= $a ?>)

- Nguyên tắc 2: File code PHP sử dụng encode UTF-8 without BOM.

- Nguyên tắc 3: File PHP NÊN dùng để khai báo các thành phần của PHP (class, function, const) và các hiệu ứng phụ (include, thiết lập init PHP), nhưng KHÔNG NÊN dùng cả hai trong một file. Để hiểu rõ hơn nguyên tắc này, bạn hãy xem ví dụ sau
````php
//bad

<?php
ini_set('error_reporting', E_ALL);

include "file.php";

echo "<html>\n";

// khai báo hàm
function foo()
{
    // function body
}

//good
//file functions.php
<?php
// functions.php

// khai báo hàm
function foo()
{
    // function body
}

//file index.php

<?php
// index.php

// hiệu ứng phụ: đổi thiết lập ini
ini_set('error_reporting', E_ALL);

// hiệu ứng phụ: nạp file vào
include "file.php";
include "functions.php";

// hiệu ứng phụ: xuất dữ liệu
echo "<html>\n";
````

## Đối với khai báo namespace và class
- Nguyên tắc 1: namespace và class phải thuân theo chuẩn “autoload” PSR-0, PSR-4.

Mỗi class được khai báo trên một file PHP riêng và có namespace tối thiểu một cấp, cấp đầu tiên là tên vendor (tên đơn vị phát hành)

Tên class PHẢI được viết dạng ClassName thay vì classname, Classname, class_name hay Class_Name

Từ PHP 5.3, PHẢI sử dụng namespace khi khai báo class.

````php
//bad
<?php

class Classname
{
    //
}

//good
<?php

namespace Vendor;

class ClassName
{
    //
}
````

##  Hằng, thuộc tính và phương thức của class
- Quy tắc 1: Hằng khai báo trong class phải được viết hoa và ngăn cách bằng dấu gạch dưới.

````php
//bad
<?php
namespace Vendor\Model;

class Foo
{
    const version = '1.0';
    const date_approved = '2012-06-01';
}

//good
<?php
namespace Vendor\Model;

class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
````

- Tên phương thực phải được đặt ở dang tenPhuongThuc()

````php
//bad
<?php

namespace Vendor\Model;

class Foo
{
    public function method_name()
    {
        //
    }
}

//good
<?php

namespace Vendor\Model;

class Foo
{
    public function methodName()
    {
        //
    }
}
````