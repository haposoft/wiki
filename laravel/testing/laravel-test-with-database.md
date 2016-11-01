**Giới thiệu**

* Để test các hàm giao tiếp với database trong unittest ta có rất nhiều cách làm như tạo tạo các file giữ liệu giả lưu trữ dưới dạng file json, xml, hoặc cũng có thể chuẩn bị giữ liệu dưới dạng mảng. Tuy nhiên còn có một cách khác cũng khá đơn giản đó là tạo database chuyên dùng cho việc test
* Đặc điểm của phương pháp này là sử dụng khá đơn giản, không tốn thời gian chuẩn bị giữ liệu như các phương pháp tạo mock.

**Có 2 cách làm để test trực tiếp trên database là:**

* Tạo một database cùng loại với database project đang sử dụng chỉ sử dụng trong môi trường test
* * Ưu điểm: Giống hoàn toàn với môi trường thực tế
* * Nhược điểm: Khi database lớn thì việc phải migrate lại và reset cũng khá mất thời gian
* Cấu hình sử dụng sqlite
* * Ưu điểm: Mọi thao tác với database đều được thực hiện trên ram sẽ bị xóa sạch khi thao tác test được thực thi xong
* * Nhược điểm: Do thực hiện trên ram nên rất tốn bộ nhớ và khá mất thời gian khi thực hiện test các project lớn
    
   **Config**
   
* tại file config/database.php cấu hình như sau
```
//Cấu hình để lấy kết nối từ file env
'default' => env('DB_DEFAULT','mysql'),

'connections' => [
 // cấu hình data test cho sqlite
    'sqlite' => [
        'driver'   => 'sqlite',
        'database' => ':memory:',
        'prefix'   => '',
    ],
 // database product
    'mysql' => [
        'driver'    => 'mysql',
        'host'      => env('DB_HOST', 'localhost'),
        'database'  => env('DB_DATABASE', 'forge'),
        'username'  => env('DB_USERNAME', 'forge'),
        'password'  => env('DB_PASSWORD', ''),
        'charset'   => 'utf8',
        'collation' => 'utf8_unicode_ci',
        'prefix'    => '',
        'strict'    => false,
    ],

    //cấu hình kết nối data test cho 
    'mysql_test' => [
        'driver'    => 'mysql',
        'host'      => env('DB_HOST_TEST', 'localhost'),
        'database'  => env('DB_DATABASE_TEST', 'forge'),
        'username'  => env('DB_USERNAME_TEST', 'forge'),
        'password'  => env('DB_PASSWORD_TEST', ''),
        'charset'   => 'utf8',
        'collation' => 'utf8_unicode_ci',
        'prefix'    => '',
        'strict'    => false,
    ],
```
* thêm các khai báo cho data test tại file **.env**
```
DB_HOST_TEST=localhost
DB_DATABASE_TEST=datatest
DB_USERNAME_TEST=root
DB_PASSWORD_TEST=
```
* Config chuyển đổi sang sử dụng data test khi thực hiện test tại file tests/TestCase.php
```
<?php
use Illuminate\Support\Facades\Artisan;

class TestCase extends Illuminate\Foundation\Testing\TestCase
{
    public function createApplication()
    {
        putenv('DB_DEFAULT=mysql_test');

        $app = require __DIR__ . '/../bootstrap/app.php';

        $app->make('Illuminate\Contracts\Console\Kernel')->bootstrap();

        return $app;
    }
}
```
* Trong hàm createApplication() ta đã thực hiện việc đổi DB_DEFAULT từ mysql sang mysql_test hoặc ta cũng có thể đổi sang dùng sqlite bằng câu lệnh **putenv('DB_DEFAULT=sqlite')**;
* Nếu muốn reset lại toàn bộ database trước và sau khi test thì ta cần phải thêm 2 câu lệnh trên terminal với nội dung như sau
```
php artisan migrate:reset
 ```
 và 
```
php artisan migrate
 ```

**Ví dụ**

* Tạo các hàm test create,edit,delete user
```
<?php

use Illuminate\Foundation\Testing\WithoutMiddleware;
use Illuminate\Foundation\Testing\DatabaseMigrations;
use Illuminate\Foundation\Testing\DatabaseTransactions;
use App\Models\Category;
class CategoryTest extends TestCase
{
    /**
     * A basic test example.
     *
     * @return void
     */
    public function testCreate()
    {
        $category = Category::create([
            'name' => 'Category name',
            'lang_type' => 'en',
        ]);
        $this->assertEquals(1,count($category));
    }

    public function testUpdate()
    {
        $category = Category::create([
            'name' => 'Category name',
            'lang_type' => 'en',
        ]);
        $result = $category->update([
            'name' => 'Category name new',
        ]);
        $this->assertEquals(true, $result);
    }

    public function testDetele()
    {
        $category = Category::create([
            'name' => 'Category name',
            'lang_type' => 'en',
        ]);
        $result = $category->delete();
        $this->assertEquals(true, $result);
    }

    public function testDatabase()
    {
        $this->seeInDatabase('categories', [
            'name' => 'Category name'
        ]);
    }
}
```
**Tư liệu tham khảo**
* https://laravel.com/docs/5.3/testing
* https://viblo.asia/vi 