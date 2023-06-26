## Đặt tên biến dễ hiểu
- Tức là đặt tên biến sao cho đọc vô là hiểu nó là gì và nó dùng để làm gì. Không cần phải suy nghĩ, suy diễn.

````php
//bad
<?php

 $ymdstr = $moment->format('y-m-d');
//good
<?php

$currentDate = $moment->format('y-m-d');
````

## tránh lồng quá nhiều và nên return sớm
- Quá nhiều if else lồng nhau sẽ khiến code tăng độ phức tạp, khó debug. Giảm sự phức tạp bằng cách giảm số if else lồng nhau xuống ít nhất có thể. Return sớm chính là một cách giảm số lần lồng nhau.
````php
//bad
<?php

function isShopOpen($day): bool
{
    if ($day) {
        if (is_string($day)) {
            $day = strtolower($day);
            if ($day === 'friday') {
                return true;
            } elseif ($day === 'saturday') {
                return true;
            } elseif ($day === 'sunday') {
                return true;
            } else {
                return false;
            }
        } else {
            return false;
        }
    } else {
        return false;
    }
}
//good
<?php
function isShopOpen(string $day): bool
{
    if (empty($day)) {
        return false;
    }

    $openingDays = [
        'friday', 'saturday', 'sunday'
    ];

    return in_array(strtolower($day), $openingDays, true);
}
````
## Đừng thêm những nội dung không cần thiết
- Nếu tên của class/object đã rõ ràng, không nên lặp lại chúng trong tên biến.

````php
//bad
<?php
class Car
{
    public $carMake;
    public $carModel;
    public $carColor;

    //...
}
//good
<?php
class Car
{
    public $make;
    public $model;
    public $color;

    //...
}
````