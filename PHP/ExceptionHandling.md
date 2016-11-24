
## 3.2 Xử lý ngoại lệ và lỗi (Error & Exception Handling)

Xử lý lỗi là tiến trình bắt các lỗi được tạo bởi chương trình của bạn và sau đó thực hiện các hành động thích hợp.
Nếu bạn xử lý lỗi không chính xác, thì có thể dẫn tới nhiều kết quả không mong đợi.
Trong PHP, nó là khá đơn giản để xử lý một lỗi.

### 3.2.1 Sử dụng hàm die() trong PHP

Trong khi lập trình PHP, bạn nên kiểm tra tất cả điều kiện lỗi có thể có trước khi tiếp tục và thực hiện các hành động
thích hợp khi cần thiết. Bạn thử ví dụ sau mà không có /tmp/test.txt file và với file này.
```php
<?php
   if(!file_exists("/tmp/test.txt"))
   {
      die("Không tìm thấy file này!!!");
   }
   else
   {
      $file=fopen("/tmp/test.txt","r");
      print "Mở file thành công!!!";
   }
   // phần code ....
?>
```
Theo cách này, bạn có thể viết một code hiệu quả. Sử dụng kỹ thuật trên, bạn có thể dừng chương trình của bạn bất cứ khi
nào nó xảy ra lỗi và hiển thị thông báo thân thiện và ý nghĩa hơn tới người dùng.

### 3.2.2 Tự định nghĩa hàm để xử lý lỗi trong PHP

Bạn có thể viết hàm riêng cho bạn để xử lý bất kỳ lỗi nào. PHP cung cấp cho bạn một framework để định nghĩa hàm
xử lý lỗi.

Hàm này phải có khả năng để thao thác ít nhất hai tham số (error level và error message), nhưng có thể tới 5 tham số
(tùy ý: file, line-number, và error context):

**Cú pháp**
```
error_function(error_level, error_message, error_file, error_line, error_context);
```
Bảng dưới là chi tiết về các tham số trên:

Tham số | Miên tả
------------- | -------------
error_level | Bắt buộc - Xác định cấp độ lỗi cho lỗi tự định nghĩa (user-defined). Phải là một giá trị số
error_message | Bắt buộc - Xác định error message lỗi tự định nghĩa
error_file | Tùy ý - Xác định tên file trong đó lỗi xảy ra
error_line | Tùy ý - Xác định số dòng trong đó lỗi xảy ra
error_context | Tùy ý - Xác định một mảng chứa mọi biến và giá trị của chúng, sử dụng khi lỗi xảy ra

**Cấp độ lỗi có thể có trong PHP**
Những cấp độ lỗi này là các kiểu lỗi khác nhau. Những giá trị này có thể được sử dụng kết hợp bởi sử dụng toán tử |.

Giá trị | Hằng số | Miêu tả
------------- | ------------- | -------------
1 | E_ERROR | Fatal run-time error. Các lỗi nghiêm trọng và việc thực thi script bị dừng lại
2 | E_WARNING | Non-fatal run-time error. Các lỗi không nghiêm trọng và việc thực thi script không bị dừng lại
4 | E_PARSE | Compile-time parse error. Lỗi về parse trong thời gian biên dịch. Các lỗi về parse này nên chỉ được tạo bởi parser
8 | E_NOTICE | Run-time notice. Script tìm thấy cái gì đó mà có thể là một lỗi, nhưng cũng có thể xảy ra khi đang chạy một script một cách bình thường
16 | E_CORE_ERROR | Các Fatal error mà xuất hiện trong khi cài đặt ban đầu của PHP
32 | E_CORE_WARNING | Các non-fatal runtime error, xảy ra trong khi cài đặt ban đầu của PHP
256 | E_USER_ERROR | Fatal error được tạo bởi người dùng. Nó giống như một E_ERROR được thiết lập bởi lập trình viên bởi sử dụng hàm trigger_error() trong PHP
512 | E_USER_WARNING | Non-Fatal error được tạo bởi người dùng. Nó giống như một E_WARNING được thiết lập bởi lập trình viên bởi sử dụng hàm trigger_error() trong PHP
1024 | E_USER_NOTICE | User-generated notice. Nó giống như một E_NOTICE được thiết lập bởi lập trình viên bởi sử dụng hàm trigger_error() trong PHP
2048 | E_STRICT | Run-time notice. Kích hoạt để có các thay đổi gợi ý từ PHP tới code của bạn mà sẽ đảm bảo cho tính tương hợp nhất của code
4096 | E_RECOVERABLE_ERROR | Fatal error có thể bắt. Giống một E_ERROR nhưng có thể được bắt bởi người dùng (tham khảo set_error_handler())
8191 | E_ALL | Tất cả error và warning, ngoại trừ E_STRICT (E_STRICT sẽ là bộ phận của E_ALL như của PHP 6.0)

Tất cả cấp độ lỗi trên có thể được thiết lập bởi sử dụng hàm có sẵn trong PHP sau, với level có thể là bất kỳ giá trị nào được định nghĩa trong bảng trên.
```
int error_reporting ( [int $level] )
```
Dưới đây là cách bạn có thể tạo một hàm xử lý lỗi trong PHP:
```php
<?php
   function handleError($errno, $errstr, $error_file, $error_line)
   {
      echo "<b>Xảy ra lỗi:</b> [$errno] $errstr - $error_file:$error_line";
      echo "<br />";
      echo "Kết thúc PHP Script";
      die();
   }
?>
```
Khi bạn đã định nghĩa Error handler cho riêng bạn, bạn cần thiết lập nó bởi sử dụng hàm **set_error_handler**
có sẵn trong PHP. Bây giờ kiểm trả lại ví dụ trên bằng việc gọi một hàm mà không tồn tại.
```php
<?php
   error_reporting( E_ERROR );
   
   function handleError($errno, $errstr, $error_file, $error_line)
   {
      echo "<b>Xảy ra lỗi:</b> [$errno] $errstr - $error_file:$error_line";
      echo "<br />";
      echo "Kết thúc PHP Script";
      die();
   }
   
   //thiết lập error handler
   set_error_handler("handleError");
   
   //trigger error
   myFunction();
?>
```
### 3.2.3 Xử lý ngoại lệ (Exception Handling) trong PHP

PHP 5 có một Exception Model tương tự như trong các ngôn ngữ lập trình khác. Exception là quan trọng và cung cấp một
điều khiển tốt hơn thông qua xử lý lỗi.

Dưới đây giải thích một số từ khóa liên quan tới exception trong PHP:

- **Try** − Một hàm sử dụng một exception nên là một khối try. Nếu exception không kích hoạt, code sẽ tiếp tục như bình thường.
Tuy nhiên, nếu exception kích hoạt, một exception được "thrown".
- **Throw** − Đây là cách bạn kích hoạt một exception. Mỗi "thrown" phải có ít nhất một "catch".
- **Catch** − Mỗi khối "catch" thu nhận một exception và tạo một đối tượng chứa thông tin exception đó.

Khi một exception được ném, code theo sau lệnh đó sẽ không được thực thi, và PHP sẽ cố gắng tìm kiếm khối catch so khớp
đầu tiên. Nếu một exception không được bắt, một Fatal Error (lỗi nghiêm trọng) trong PHP sẽ được thông báo với một
"*Uncaught Exception ...*"

- Một exception có thể được ném, và bắt bên trong PHP. Code có thể được bao quanh trong một khối try.
- Mỗi khối try phải có ít nhất một khối catch tương ứng. Nhiều khối catch có thể được sử dụng để bắt các lớp exception khác nhau.
- Các exception có thể được ném (hoặc ném lại) bên trong một khối catch.

**Ví dụ:**

Dưới đây là một đoạn code, bạn sao chép và dán code này vào trong một file và kiểm tra kết quả:
```php
<?php
   try {
      $error = 'Luôn luôn ném lỗi này';
      throw new Exception($error);
      
      // Phần code mà theo sau một ngoại lệ sẽ không được thực thi.
      echo 'Phần code này không bao giờ được thực thi';
   }
   catch (Exception $e) {
      echo 'Bắt ngoại lệ: ',  $e->getMessage(), "\n";
   }
   
   // Tiếp tục tiến trình thực thi
   echo 'Hello World';
?>
```
Trong ví dụ trên, hàm $e->getMessage được sử dụng để lấy error message. Dưới đây là một số hàm có thể được sử dụng từ
lớp **Exception** trong PHP.
- getMessage() − thông báo của exception
- getCode() − code của exception
- getFile() − tên source file
- getLine() − source line
- getTrace() − n mảng của backtrace()
- getTraceAsString() − chuỗi được định dạng của trace

**Tạo Custom Exception Handler trong PHP**

Bạn có thể định nghĩa Exception Handler cho riêng bạn. Bạn sử dụng các hàm sau để thiết lập một hàm xử lý ngoại lệ tự
định nghĩa.
```
string set_exception_handler ( callback $exception_handler )
```
Ở đây, *exception_handler* là tên hàm để được gọi khi một uncaught exception xuất hiện. Hàm này phải được định nghĩa trước
khi gọi hàm set_exception_handler().

**Ví dụ**
```php
<?php
   function exception_handler($exception) {
      echo "Uncaught exception: " , $exception->getMessage(), "\n";
   }
   set_exception_handler('exception_handler');
   throw new Exception('Xuat hien Uncaught Exception');
   
   echo "Phần code không được thực thi\n";
?>
```