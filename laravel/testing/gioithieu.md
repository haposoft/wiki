

##**Giới thiệu**


* Kiểm soát lỗi là một phần vô cùng quan trọng trong quá trình phát triển một trang web. Tuy nhiên đây cũng là một phần mà các lập trình viên vô cùng ngại và thường bỏ qua nó. Tuy nhiên theo năm tháng, ứng dụng của bạn phình to quá mức. Lúc này cùng với việc tối ưu code các hàm dùng chung của bạn sẽ nhiều lên và việc thay đổi bất kỳ điều gì trong một hàm cũng có thể ảnh hưởng tới rất nhiều chức năng khác trong hệ thống. Lúc đó có khi bạn còn ngại viết các chức năng mới hơn :D . Những lúc như thế chắc bạn sẽ ước có một người hầu cận để sai sai bảo hắn kiểm tra mọi thứ cho mình. Tuy nhiên có thể bạn không để ý hoặc cố tình lơ nó đi ngay từ những ngày đầu rằng: Laravel đã hỗ trợ chúng ta việc đó ngay từ đầu rồi. Đó là Unit test.

####**Tuy nhiên tại sao lập trình viên lại thường bỏ quên unit test**

* Unit test đòi hỏi bạn phải phải viết hàm kiểm thử mọi thứ bạn viết ra trong ứng dụng từ controller, model hay các hàm trong service. Và việc này thường mất thời gian tương đương với thời gian code. Chính vì thế tâm lý ngại là một điều dễ hiểu. Tuy nhiên như đã nói ở trên sẽ đến một lúc nào đó bạn sẽ phải hối hận về điều này
* Bới lông tìm vết: Unit test cũng đưa sẽ liệt kê tất cả các lỗi trong ứng dụng của bạn dù là nhỏ nhất. Nhiều khi những lỗi đó không ảnh hưởng đến việc vận hành trang web. Hẳn bạn sẽ phải bực mình nếu unit báo app của bạn đang bị lỗi vì bạn sử dụng chữ home thay vì Home. Phải check những lỗi như thế thì không ngại sao được. Tuy nhiên những lỗi text như vậy nếu xuất hiện với tần xuất cao trên ứng dụng của bạn thì nó sẽ gây ảnh hưởng nghiêm trọng tới trải nghiệm người dùng. Chắc chắn lúc đó bạn sẽ ăn hành nhiều hơn từ khách hàng.
* Viết unit test cũng có nghĩa là bạn phải lập đi lặp lại những đoạn code tương tự nhau chỉ khác nhau giữ liệu đầu vào. Điều đó có thể sẽ gây nhàm chán vô cùng. Tuy nhiên nếu làm việc này bạn chỉ phải tạo ra giữ liệu test 1 lần thay vì phải làm đi làm lại nhiều lần nếu bạn test trực tiếp trên ứng dụng của mình. Đôi khi nó còn không đủ các trường hợp có thể phát sinh lỗi
* Sếp không yêu cầu: Đây cũng là một lý do rất chính đáng. Có thể do thời gian của dự án eo hẹp hoặc vấn đề chi phí khi bạn phải mất thêm khá nhiều thời gian để làm việc này. Tuy nhiên bạn nên đề xuất nếu có thể.

####**Viết Unit test cần chuẩn bị những gì.**

* **Môi trường**: Có lẽ đây là việc đơn giản nhất trong mọi việc đơn giản. Vì laravel đã hỗ trợ tận răng cho ta mỗi trường rồi. Cứ thế là code thôi. Phiên bản hiện tại được sử dụng trong laravel 5.3 là php unit 5.6
* **Test case**: Có lẽ đây là phần quan trọng nhất khi viết unit test. Việc chuẩn bị được một bộ test case chuẩn là vô cùng quan trọng vì nó đảm bảo cho bạn có thể lường được hết các trường hợp và đảm bảo sẽ không có lỗi nào có thể lọt qua trong quá trình chạy ứng dụng. Tuy nhiên cũng không cần phải đến mức chuẩn bị trước tất cả như các tester chuyên nghiệp. Khi nào đến chức năng nào đó ta hãy dành thời gian để chuẩn bị chúng.
* **code**: có lẽ cũng nên đọc qua một chút cách sử dụng và các hàm hỗ trợ trước khi bắt đầu. Bạn có thể tham khảo tại đây:
* * https://www.laravel.com/docs/5.3/testing
* * https://phpunit.de/

####**Viết Các hàm test đầu tiên.**

* Tại tại terminal gõ lệnh sau:
```
php artisan make:test BasicTest
```
Đoạn lệnh command trên sẽ giúp bạn tạo ra một file test trong tests/BasicTest.php như sau:
PHP
```
<?php

use Illuminate\Foundation\Testing\WithoutMiddleware;
use Illuminate\Foundation\Testing\DatabaseMigrations;
use Illuminate\Foundation\Testing\DatabaseTransactions;
​
class BasicTest extends TestCase
{
    /**
     * A basic test example.
     *
     * @return void
     */
    public function testExample()
    {
        $this->assertTrue(true);
    }
}
```
* Thấy gì từ file test này:
* * Các class test của php unit đều được mặc đinh kế thừa từ class BasicTest
* * Với mỗi test case ta có thể viết thành một hàm riêng biệt. hoặc mỗi hàm ta cũng có thể test 1 hoặc nhiều test case.
* * Tên mỗi function test đều phải được bắt đầu bằng chữ **test**. Tuy nhiên bạn cũng có thể bỏ qua chữ này nếu sử dụng annotation **@test** trước mỗi funtion.
```
<?php
​
use Illuminate\Foundation\Testing\WithoutMiddleware;
use Illuminate\Foundation\Testing\DatabaseMigrations;
use Illuminate\Foundation\Testing\DatabaseTransactions;
​
class BasicTest extends TestCase
{
    /**
     * A basic test example.
     *@test
     * @return void
     */
    public function example()
    {
        $this->assertTrue(true);
    }
}
```
* Giờ ta thử kiểm tra thành quả xem thế nào.
* Vào terminal gõ:
```
phpunit
```
* Kết quả ta thu được khá đẹp:
```
PHPUnit 5.6.1 by Sebastian Bergmann and contributors.

..                                                                 2 / 2 (100%)

Time: 267 ms, Memory: 8.00MB

OK (2 tests, 1 assertion)
```
**Tổng kết**

Trên đây là giới thiệu và một ví dụ đơn giản để ta có thể làm quen với unit test. ta sẽ đi sâu vào chi tiết cũng như những gì hay ho hơn của unit test trong những bài tiếp theo.

Nguồn:* https://viblo.asia/vi