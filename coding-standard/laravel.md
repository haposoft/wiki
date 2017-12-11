# Laravel coding convention

Laravel tuân thủ theo chuẩn PSR-2(coding standard) và PSR-4(autoloading standard).

Dưới đây là 1 số convention cần lưu ý:
 

## 1. Route

### a, Route name
 
 Nếu `route name` là từ ghép  thì sử dụng `snake_case` . Ví dụ:

```
Route('/download-file', [
    'as' => 'download_file',
    'uses' => ''FileController@download
]);
```
### b, Group route

Những `route` có uri `prefix` giống nhau nên được gộp vào cùng 1 group và đặt `prefix` và `name`. Ví dụ:
```
Route::group(['prefix' => 'project_budget', 'as' => 'project_budget.'], function () {
            Route::get('/', ['as' => 'index', 'uses' => 'ProjectBudgetController@index']);
            Route::post('/create', ['as' => 'create', 'uses' => 'ProjectBudgetController@create']);
```
Xem thêm tại:  [Route group document](https://laravel.com/docs/5.5/routing#route-groups) 

## 2. Database
### a, Tên table
* Tên bảng phải ở dạng số nhiều. Ví dụ: users, project_budgets, processes...
* Trong quan hệ n-n, tên bảng pivot (bảng thứ 3) được ghép tên dạng số ít của 2 bảng quan hệ theo thứ tự alpha bet.
  Ví dụ: 
  > bảng thứ nhất tên `users`, bảng thứ hai có tên `posts` thì bảng pivot có tên là `post_user`.
  Lý do bởi trong bảng chữ cái thì `p` đứng trước `u`.
  
### b, Tên column
* Tên column bắt buộc ở dạng `snake_case`
* Tên column bằng tiếng Anh, ngắn gọn dễ hiểu.
* Khi viết migration hay thiết kế DB nên column có comment tên hiển thị (bằng tiếng Nhật) hoặc chú thích ngắn gọn.

## 3. Tên thư mục , tên file
  Tên thư mục và tên file viết theo dạng `snake` và ở dạng số .

  Ví dụ: `views`, `image_files`
 
## 4. Tên biến, method
### a, Tên biến:
* Tên biến bằng tiếng Anh, được đặt ngắn ngọn dễ hiểu.
* Tên biến bắt buộc phải ở dạng `camelCase`. Ví dụ: `$user`, `$projectBudget`.
* Tên biến của 1 array hay collection của các object nên đặt ở dạng số nhiều. Ví dụ: khi query ra tất cả các user thì đặt tên biến là `$users`, nếu chỉ lấy ra 1 user thì đặt là `$user`

### b, Tên method
* Tên biến bằng tiếng Anh, được đặt ngắn ngọn dễ hiểu.
* Tên biến bắt buộc phải ở dạng `camelCase`.
* Với những method hay xử lý phức tạp nên có comment, chú thích ở bên trên (hoặc ngay bênh cạnh dòng xử lý).
* **Chú ý:** Tên relation method của eloquent phải được đặt đúng theo convention mặc định của laravel: *nếu method trả về 1 đối tượng thì method có tên dạng số ít,nếu method trả về tập đối tượng thì method có tên dạng số nhiều*. 
Ví dụ: Quan hệ 1-n: 1 user có nhiều post:
 * Lấy user của 1 post thì dùng: `$post->user()`
 * Lấy tất cả post của 1 user: `$user->posts()`
