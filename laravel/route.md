# Laravel Route

- [1. Cơ bản](#basics)
	- [Các file route mặc định](#default-route-files)
	- [Các route method](#route-methods)
	- [Trường CSRF Protection](#csrf-protection)
	- [Route điều hướng](#redirect-routes)
	- [Route trả về view](#view-routes)
- [2. Route Params](#route-params)
	- [Tham số tùy chọn](#optional-params)
	- [Ràng buộc](#regular-expressions)
- [3. Đặt tên route](#named-route)
- [4. Nhóm](#route-group)
	- [Nhóm chung Middleware](#middleware)
	- [Nhóm chung Namespace](#namespace)
	- [Nhóm Sub domain](#sub-domain)
	- [Nhóm chung prefix](#prefixes)
-  [5. PUT, PATCH, DELETE Form method ](#put-patch-delete-form-method )


<a name="basics"></a>
## 1. Cơ bản

Hầu hết các route cơ bản trong Laravel nhận tham số là 1 URI và 1 [`Closure`](http://php.net/manual/en/class.closure.php)

```php
Route::get('foo', function () {
    return 'Hello World';
});
```

<a name="default-route-files"></a>
#### Các file route mặc định

- `routes/web.php` : các route khai báo trong này thuộc nhóm `web` middleware, nhóm middleware này cung cấp các tính năng như `Session`, `CSRF protection` và `cookie encryption`.

- `routes/api.php` : các route khai báo trong này là stateless (không lưu session) và thuộc nhóm `api` middleware. Các route mặc định được thêm prefix `/api` vào URI. Bạn có thể thay đổi prefix bằng cách chỉnh sửa class `RouteServiceProvider`.

<a name="route-methods"></a>
#### Các route method

```php
Route::get($uri, $callback);
Route::post($uri, $callback);
Route::put($uri, $callback);
Route::patch($uri, $callback);
Route::delete($uri, $callback);
Route::options($uri, $callback);
```
Nếu bạn muốn khai báo 1 route có thể nhận nhiều resquest methods. Bạn có thể sử dụng `match` hoặc `any`:

```php
// Route xử lý get và post request

Route::match(['get', 'post'], '/', function () {
    //
});
```

```php
// Route nhận tất cả request methods

Route::any('foo', function () {
    //
});
```
<a name="csrf-protection"></a>
#### Trường CSRF Protection
Bất cứ HTML forms nào gửi `POST`, `PUT` hoặc `DELETE` request đến các route được định nghĩa trong nhóm `web` phải chứa trường `CSRF token`. Nếu không request sẽ bị Laravel từ chối.
[`CSRF documentation`](https://laravel.com/docs/5.5/csrf)

```blade
<form method="POST" action="/profile">
    {{ csrf_field() }}
    ...
</form>
```

<a name="redirect-routes"></a>
#### Route điều hướng
Chuyển hướng đến 1 URI khác:

```php
Route::redirect('/from_here', '/to_there', 301);
```

<a name="view-routes"></a>
#### Route trả về view
Trong trường hợp route chỉ cần return view.

- Tham số thứ nhất là URI của route
- Tham số thứ 2 là tên view
- Tham số thứ 3 (tùy chọn) là mảng các dữ liệu gửi đến view

```php
Route::view('/welcome', 'welcome');

Route::view('/welcome', 'welcome', ['name' => 'Taylor']);
```

<a name="route-params"></a>
## 2. Route Params

```php
// id ở đây là 1 param

Route::get('user/{id}', function ($id) {
    return 'User '.$id;
});

// Multi params

Route::get('posts/{post}/comments/{comment}', function ($postId, $commentId) {
    //
});
```

<a name="optional-params"></a>
#### Tham số tùy chọn

Thêm dấu `?` vào sau tên param để biểu thị rằng param là tham số tùy chọn :

```php
Route::get('user/{name?}', function ($name = null) {
    return $name;
});
```

<a name="regular-expressions"></a>
#### Ràng buộc

Ràng buộc bằng biểu thức chính quy

```php
// name chỉ nhận chuỗi chỉ chứa ký tự a-z hoặc A-Z

Route::get('user/{name}', function ($name) {
    //
})->where('name', '[A-Za-z]+');

```

#### Ràng buộc toàn cục

 Sử dụng `Route::pattern()` trong hàm boot của `app/Provider/RouteServiceProvider`: 

```php
public function boot()
{
    // tất cả param id chỉ nhận giá trị số
    
    Route::pattern('id', '[0-9]+');

    parent::boot();
}
```

<a name="named-route"></a>
## 3. Đặt tên route

Để đặt tên cho route. Sử dụng hàm `name()` :
```php
// Đặt tên cho route là profile

Route::get('user/profile', 'UserProfileController')->name('profile');
```

Để tạo URLs đến route đã đặt tên, sử dụng hàm `route`:
```php
route('profile');

// hoặc redirect đến 1 route
redirect()->route('profile');
```

Nếu route được đặt tên cần tham số, truyền nó vào như là tham số thứ 2 của hàm `route`, Laravel sẽ đặt tham số vào đúng vị trí giúp bạn:

```php
Route::get('user/{id}/profile', function ($id) {
    //
})->name('profile');

$url = route('profile', ['id' => 1]);
```

<a name="route-group"></a>
## 4. Route group

Route group cho phép bạn nhóm các route có chung các 
thuộc tính, ví dụ như prefix, middlewares hay namespaces mà không phải định nghĩa các thuộc tính đó cho từng route một.

<a name="middleware"></a>
### Middleware
Để gắn middlewares cho toàn bộ route ở trong 1 nhóm, sử dụng hàm `middleware` của Facade Route, các middleware được thực hiện theo thứ tự trong mảng tham số truyền vào: 

```php
Route::middleware(['first', 'second'])->group(function () {
    Route::get('/', function () {
        // Uses first & second Middleware
    });

    Route::get('user/profile', function () {
        // Uses first & second Middleware
    });
});
```
<a name="namespace"></a>
### Namespace
Một trường hợp thường gặp khác đó là gắn namespace cho toàn bộ các route trong 1 nhóm -> sử dụng hàm `namespace`:

```php
Route::namespace('Admin')->group(function () {
    // Controllers Within The "App\Http\Controllers\Admin" Namespace
});
```
Nên nhớ rằng, mặc định `RouteServiceProvider` nhóm các file route trong 1 namespace, cho phép bạn có thể khai báo Controller cho route mà không cần phải khai báo toàn bộ đường dẫn đến Controller `App\Http\Controllers\...`. Vì thế, bạn chỉ cần khai báo mỗi tên của Controller nằm trong forder `App\Http\Controllers\`.

<a name="sub-domain"></a>
### Sub-Domain

```php
Route::domain('{account}.myapp.com')->group(function () {
    Route::get('user/{id}', function ($account, $id) {
        //
    });
});
```

<a name="prefixes"></a>
### Prefixes

```php
Route::prefix('admin')->group(function () {
    Route::get('users', function () {
        // Matches The "/admin/users" URL
    });
});
```

<a name="put-patch-delete-form-method"></a>
## 5. PUT, PATCH, DELETE Form method 
Mặc định form html không hỗ trợ các method `PUT`, `PATCH`, `DELETE`. Để khai báo `PUT`, `PATCH`, `DELETE` request từ form, chỉ cần thêm 1 trường ẩn `_method` vào form đó :

```html
<form action="/foo/bar" method="POST">
    <input type="hidden" name="_method" value="PUT">
    <input type="hidden" name="_token" value="{{ csrf_token() }}">
</form>
```

Bạn cũng có thể sử dụng hàm helper `method_field` để tạo trường `_method`: 

```php
{{ method_field('PUT') }}
```









