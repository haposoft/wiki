# Laravel naming conventions

Laravel tuân thủ theo chuẩn PSR-2(coding standard) và PSR-4(autoloading standard).

Dưới đây là 1 số convention cần lưu ý:

## **1. Route**

### **a, Route name**
 
- Khai báo `route name` ở dạng số nhiều, nếu từ ghép thì sử dụng `snake_case` và phân tách với nhau bằng dấu `.` . Ví dụ:

```php
Route('/users/download-file', [
    'as' => 'users.download_file',
    'uses' => 'UserController@downloadFile'
]);
```
### **b, Group route**

- Những `route` có uri `prefix` giống nhau nên được gộp vào cùng 1 group và đặt `prefix` và `name`. Ví dụ:
```php
Route::group(['prefix' => 'projects', 'as' => 'projects.'], function () {
            Route::get('/', ['as' => 'index', 'uses' => 'ProjectController@index']);
            Route::get('/create', ['as' => 'create', 'uses' => 'ProjectController@create']);
            ...
```
Xem thêm tại:  [Route group document](https://laravel.com/docs/5.5/routing#route-groups) 

### **c, Url**

- Các `url` ở dạng số nhiều, nếu là các từ ghép thì sử dụng `kebab-case`

```php
Route::get('/users/1/download-document', ['uses' => 'UserController@downloadDocument'])->name('users.download_document');
```

### **d, Method**
- Các method của request tuân thủ theo chuẩn [RESTful](http://wiki.haposoft.com/coding-standard/RESTful.html)

## **2. Controller**

### **a, Controller name**

- Khai báo ở dạng số ít như `ArticleController`, `UserController` không khai báo ở dạng số nhiều 
 ~~ArticlesController~~, ~~UsersController~~
 
### **b, Method**

- Khai báo các method theo `camelCase` ví dụ như `getAll`, `downloadDocument`, method phải là các động từ mô tả hành động sẽ thực hiện trong method.
-  Các methods phục vụ cho `CRUD` phải đặt tên theo đúng các methods trong [Resource Controllers](https://laravel.com/docs/master/controllers#resource-controllers) 

## **3. Model**

### **a, Name**

- Đặt tên model ở dạng số ít theo dạng `PascalCase` và tên model thường phải trùng với tên bảng tương ứng trong Database.
 Ví dự: `User`, `CategoryProduct`

### **b, Property**

- Các `property` khai báo theo dạng `snake_case`. Ví dụ: `created_at`, `updated_at`

### **c, Method**
- Các methods khai báo ở dạng `camelCase`
- Các relation methods phải được đặt đúng theo convention mặc định của Laravel, 
nếu method trả về 1 đối tượng thì method có tên dạng số ít,nếu method trả về tập đối tượng thì method có tên dạng số nhiều.

Xem thêm tại [Defining Relationships](https://laravel.com/docs/master/eloquent-relationships#defining-relationships)

## **4. Database**

### **a, Tên table**

- Tên bảng phải ở dạng số nhiều. Ví dụ: users, project_budgets, processes...
- Trong quan hệ n-n, tên bảng pivot (bảng thứ 3) được ghép tên dạng số ít của 2 bảng quan hệ theo thứ tự alpha bet.
  Ví dụ: 
  > Bảng thứ nhất tên `users`, bảng thứ hai có tên `posts` thì bảng pivot có tên là `post_user`.
  Lý do bởi trong bảng chữ cái thì `p` đứng trước `u`.
  
### **b, Tên column**

- Tên column bắt buộc ở dạng `snake_case`
- Tên column bằng tiếng Anh, ngắn gọn dễ hiểu.
- Khi viết migration hay thiết kế DB nên column có comment tên hiển thị (bằng tiếng Nhật) hoặc chú thích ngắn gọn.

### **c, Khóa chính**
- Khóa chính cho tất cả các bảng luôn là `id`

### **d, Khóa ngoài**

- Khóa ngoài bắt đầu bằng tên của bảng quan hệ ở dạng số ít kết hợp với `surfix` là `id`. Ví dụ: `user_id`, `post_id`

## **5. Tên thư mục , tên file**

### **a, Thư mục**

- Đặt tên thư theo dạng `snake_case` và ở dạng số nhiều. Ví dụ: `views`, `image_files`

### **b, View**

- Đặt tên `view` theo dạng `snake_case`. Ví dụ : `show_filtered.blade.php`

### **c, Config file, Language**

- Các files khai báo thêm cho phần `config` và phần `lang` sử dụng `snake_case`. Ví dụ `google_calendar.php`

 
## **6. Tên biến**

- Tên biến bằng tiếng Anh, được đặt ngắn ngọn dễ hiểu.
- Tên biến bắt buộc phải ở dạng `camelCase`. Ví dụ: `$user`, `$projectBudget`.
- Tên biến của 1 array hay collection của các object phải đặt ở dạng số nhiều.
Ví dụ: khi query ra tất cả các user thì đặt tên biến là `$users`, nếu chỉ lấy ra 1 user thì đặt là `$user`


