## Tham số của method và function
- Trong danh sách các tham số, không được có khoảng trắng ở trươc dấu phẩy, và phía sau dấu phẩy luôn phải có một khoảng trắng.

Các tham số mà có giá trị mặc định phải nằm ở các vị trí sau cùng trong danh sách các tham số.
````php
//bad
<?php

namespace Vendor\Package;

class ClassName
{
    public function foo(int $arg1 , &$arg3 = [] , $arg2)
    {
        // method body
    }
}
//good
<?php

namespace Vendor\Package;

class ClassName
{
    public function foo(int $arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
````

- Khi bạn khai báo kiểu dữ liệu trả về, thì phải có một khoảng trắng nằm giữa dấu hai chấm : và kiểu dữ liệu. Dấu hai chấm và kiểu dữ liệu phải nằm cùng dòng với dấu ngoặc đơn đóng.
````php
//bad
<?php

declare(strict_types=1);

namespace Vendor\Package;

class ReturnTypeVariations
{
    public function functionName(int $arg1, $arg2):string
    {
        return 'foo';
    }

    public function anotherFunction(
        string $foo,
        string $bar,
        int $baz
    ): string {
        return 'foo';
    }
}
// good 
<?php

declare(strict_types=1);

namespace Vendor\Package;

class ReturnTypeVariations
{
    public function functionName(int $arg1, $arg2): string
    {
        return 'foo';
    }

    public function anotherFunction(
        string $foo,
        string $bar,
        int $baz
    ): string {
        return 'foo';
    }
}
````
- Nếu khai khai bảo trả về kiểu nullable, thì không được có khoảng trắng giữa dấu hỏi chấm và kiểu dữ liệu.

Nếu sử dụng toán tử & trước các tham số, thì không được có khoảng trắng ở phía sau nó.
````php
//bad
<?php

declare(strict_types=1);

namespace Vendor\Package;

class ReturnTypeVariations
{
    public function functionName(?string $ arg1, ?int & $arg2): ? string
    {
        return 'foo';
    }
}
//good
<?php

declare(strict_types=1);

namespace Vendor\Package;

class ReturnTypeVariations
{
    public function functionName(?string $arg1, ?int &$arg2): ?string
    {
        return 'foo';
    }
}
````
- Không được có khoảng trắng giữa dấu ba chấm ... và tên tham số:
````php
//bad
public function process(string $algorithm, ... $parts)
{
    // processing
}
//good
public function process(string $algorithm, ...$parts)
{
    // processing
}
````