# PHP coding convention
Mỗi ngôn ngữ đều có những chuẩn viết code riêng, với PHP thì chúng ta có PSR - PHP Standards Recommendation.
Hiện tại thì đang có từ PSR-0 đến PSR-4 do các thành viên của nhóm [FIG(Framework Interop Group)](http://www.php-fig.org/) đề xuất. Chúng ta sẽ áp
 dụng chuẩn PSR-2 - Chuẩn viết code để áp dụng cho các project. Dưới đây là các quy tắc theo chuẩn PSR-2 :
- Code phải tuân thủ theo [PSR-1](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md)
- Sử dụng 4 khoảng trắng đê thụt đầu dòng thay vì dùng tab.
- Kí tự tối đa trên 1 dòng không được vượt quá 120 kí tự, tốt nhất nên dưới 80 kí tự.
- Phải có 1 dòng trắng khi khai báo `namespace` và sau khi khai báo `use`.
- Thẻ đóng mở 1 function `{}` phải nằm trên từng dòng riêng biệt.
- Trước thẻ đóng mở function `{}` không được có dòng trắng.
- Khi khai báo `abstract` và `final` thì phải khai báo trước visibility còn `static` phải khai báo sau : 

```php
<?php
abstract protected function foo();
  
final public static function bar()
{
    // method body
}
```

- Sau từ khóa khiển khối (`if`, `else`, `elseif`, `for`, ...) phải có 1 khoảng trắng, sau method hoặc function không được có khoảng trắng.
- Mở khối `{` cho cấu trúc điều khiển phải trên cùng một dòng và đóng khối này với `}`  ở dòng tiếp theo của thân khối.
- Tất cả các file đều phải dử sụng Unix LF khi kết thúc 1 dòng.
- Tất cả các file đều kết thúc bằng 1 dòng trắng.
- Nếu file chỉ có code `php` thì ko sử dụng thẻ đóng `?>`.
- Hằng số `true`, `false`, `null` phải viết chữ thường. 
- Từ khóa `extends` và `implements` phải cùng dòng với class
- Các visibility (`public`, `private`, `protected`) phải được khai báo cho tất cả các hàm và các thuộc tính của lớp;
- Implements nhiều class, thì mỗi class trên một dòng.
- Từ khóa `var` không được dùng để dụng khai báo property.
- Tên `property` không nên có tiền tố `_` nhằm thể hiện thuộc tính `protect` hay `private`.
- Tham số cho function, method không được thêm khoảng trắng vào trước dấu `,` và PHẢI có một khoảng trắng sau `,`. 
Nếu các tham số viết trên nhiều dòng thì mỗi dòng chỉ có 1 tham số.
- Khi dùng `switch` thì `{` cùng trên 1 dòng, các `case` phải lùi 4 khoảng trắng, các action và từ khóa `break` phải lùi tiếp 4 khoảng trắng. 
Phải comment `no break` trong trường hợp không dùng `break`

```php
<?php
switch ($expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
```

- Đối với [`Closures`](http://php.net/manual/en/class.closure.php), sau khi khai báo các tham số phải có 1 khoảng trắng.

```php
<?php
$closureWithArgs = function ($arg1, $arg2) {
    // body
};

$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // body
};
```