### 1. Tổng quan
* [Blade](https://laravel.com/docs/master/blade) là một khuôn mẫu (template engine) đơn giản, mạnh mẽ được cung cấp bởi Laravel
* Không giống như những template PHP khác (Twig, etc..), blade không giới hạn việc sử dụng code PHP trong views  
* Các file Blade sử dụng phần mở rộng là `blade.php` và được đặt ở trong thư mục `resources/views`   
### 2. Thừa kế views  
* Đây là một ưu điểm lớn trong việc sử dụng Blade template  
* Khi sử dụng một template engine thì việc tái sử dụng lại layout là vô cùng quan trọng, điều này khiến chúng ta tránh được việc lặp code và có thể dễ dàng nâng cấp hoặc bảo trì
#### a. Khởi tạo layout
* Đầu tiên tạo file `layouts.blade.php`:  
```
<html>
    <body>
        <head>
              <title>App Name - @yield('title')</title>
        </head>
                @section('sidebar')
                    This is the master sidebar.
                @show
        <div class='container'>
             @yield('content')
        </div>
    </body>
</html>
```

* `@yield` sẽ khai báo nơi để hiển thị dữ liệu
* `@section` là khu vực để hiển thị dữ liệu (tức là nội dung trong `@yield`), mỗi section được bắt đầu bởi `@section('ten-section')` và kết thúc bởi `@endsection`   
#### b. Kế thừa layout  
* Để một view kế thừa một view khác, chúng ta sử dụng `@extends('ten-view')`  
* Để sử dụng một view, ta dùng `@include('ten-view')`  
VD: File `child.blade.php` sẽ kế thừa `layouts.blade.php`  
```
@extends('layouts')
@section('sidebar')
    @parent

    <p>This is appended to the master sidebar.</p>
@endsection  
@section('content')
    <p>This is my body content.</p>
@endsection
```
* Ở đây `@parent` nhằm viết tiếp section `sidebar` chứ không ghi đè nó
* Có 2 cách đóng `@section` đó là `@endsection` và `@show`, trong đó `@section`
đơn thuần là đóng section còn `@show` sẽ đóng và thực hiện đánh dấu section đó bằng `@yield`
### 3. Hiển thị dữ liệu
* Để hiển thị dữ liệu ra view, chúng ta sử dụng cặp ngoặc nhọn `{{}}`  
VD: Ta có route như sau
```
// Biến name sẽ được gửi sang welcome
Route::get('greeting', function () {
    return view('welcome', ['name' => 'Samantha']);
});
```
Để hiển thị biến name : `Hello, {{ $name }}`
* Về cơ bản `{{}}` tương đương với hàm `htmlspecialchars` của PHP, để hiển thị unescaped data ta sử dụng
`{!! $name !!}`  
* Ngoài ra ta còn có thể in ra kết quả của các hàm trong PHP
* Hiển thị dữ liệu dạng JSON:  
```
    <script>
        var app = @json($array);
    </script>
```