# clean code trong comments code
Một số hướng dẫn để clean trong comment
## 1. Giải thích mục đích và chức năng của code (todo comment)

**bad**
```php
function processData($data) {
    ...
}
```
**good**
```php
// TODO: Handle validation errors
// Hàm xử lý dữ liệu đầu vào
function processData($data) {
    ...
}
```

## 2. Chú thích các phần quan trọng hay giải thích trong mã

**good**
```php
private function filterByCompletionMonthDay(Builder $builder, string $startDate, string $endDate): Builder
    {
        //Retrieve records by start time or end time compared to current time
        //The start time or end time may be in the future
        $startTime = $startDate ? Carbon::parse($startDate) : '';
        $endTime = $endDate ? Carbon::parse($endDate) : '';
        if ($startTime && $endTime) {
            $builder->whereBetween(DB::raw("DATE_FORMAT(completion_date, '%m-%d')"), sortDatesAscending($startTime->format('m-d'), $endTime->format('m-d')));
        }

        return $builder;
    }
```

## 3. Loại bỏ các comment không cần thiết
- Chú thích chỉ những phần quan trọng và cần thiết

**bad**
```php
// Hàm tính tổng hai số nguyên
function calculateDiscount($price) {
    // Tính giảm giá
    $discount = $price * 0.2;
    // Trả về giá sau khi được giảm giá
    return $price - $discount;
}
```
**good**
```php
function calculateDiscount($price) {
    $discount = $price * 0.2;
    return $price - $discount;
}
```

## 4. Tuân thủ quy ước về đặt tên và format comment:
- viết comment sao cho dễ hiểu và tuân thủ quy ước về đặt tên biến, hàm, lớp... dùng 1 loại ngôn ngữ

**bad**
```php
//xử lý
function process_data($data) {
    // code here
    // ...
}
```
**good**
```php
// Hàm xử lý dữ liệu đầu vào
function processData($data) {
    // Code xử lý dữ liệu
    // ...
}
```
## 5. Sử dụng các công cụ hỗ trợ comment
-  có thể sử dụng các công cụ như PHPDoc để tạo ra các comment có định dạng chuẩn cho các hàm, lớp và biến

**good**
```php
 /**
 * @return string
 */
public function getModel()
{
    return User::class;
}
```