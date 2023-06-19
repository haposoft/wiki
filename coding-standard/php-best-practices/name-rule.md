# Name Rules

## 1. Controller

Quy tắc đặt tên:

- Tên controller phải bắt đầu bằng một danh từ tiếng Anh và viết hoa.
- Danh từ phải ở dạng số ít.
- Không chứa dấu cách.
- Luôn kết thúc bằng Controller.

```php
// Bad
UsersController, use_controller, UsersControllers
// Good
UserController
```

## 2. Route

Quy tắc đặt tên:

- route phải là một danh từ tiếng Anh.
- Danh từ phải ở dạng số nhiều.
- Không chứa dấu cách.

```php
<?php
// Import UserController class
require_once('app/Http/UserController.php');
// Bad
if ($_SERVER['REQUEST_URI'] === '/user') {
    UserController::index();
}
// Good
if ($_SERVER['REQUEST_URI'] === '/users') {
    UserController::index();
}
```

## 3. Named route

Quy tắc đặt tên:

- Tên route phải phải là một danh từ tiếng Anh.
- Không chứa dấu cách.
- Phải đặt kiểu snake_case 🐍 và dấu chấm

```php
<?php
// Import UserController class
require_once('app/Http/UserController.php');
// Bad
if ($_SERVER['REQUEST_METHOD'] === 'GET' && $_SERVER['REQUEST_URI'] === '/users') {
    UserController::index()->name('user-index');
}
// Good
if ($_SERVER['REQUEST_METHOD'] === 'GET' && $_SERVER['REQUEST_URI'] === '/users') {
    UserController::index()->name('user.index');
}
if ($_SERVER['REQUEST_METHOD'] === 'GET' && $_SERVER['REQUEST_URI'] === '/users/active') {
    UserController::showActive()->name('user.show_active');
}
```

## 4. Model

Quy tắc đặt tên:

- Tên Model phải phải là một danh từ tiếng Anh.
- Không chứa dấu cách.
- Phải là danh từ số ít

```php
<?php
namespace App\Models;
// Bad
class Users {
    ...
}
// Good
class User {
    ...
}
```

## 5. Table (Tên bảng)

Quy tắc đặt tên:

- Tên Table phải phải là một danh từ tiếng Anh.
- Không chứa dấu cách.
- Phải là số nhiều

```php
    // Bad
    user, place, tour
    // Good
    users, places, tours
```

## 6. Tên cột trong bảng

Quy tắc đặt tên:

- Tên cột phải phải là một danh từ tiếng Anh.
- Không chứa dấu cách.
- Kiểu snake_case 🐍

```php
    // Bad
    full-name, fullName
    // Good
    full_name
```

## 7. Variable

Quy tắc đặt tên:

- Tên biến phải phải là một danh từ tiếng Anh.
- Không chứa dấu cách.
- camelCase 🐫

```php
<? php
//Bad
$full_name, $FULL_NAME, $FullName
//Good
$fullName, $articlesWithAuthor
```

## 8. Config

Quy tắc đặt tên:

- Tên Config phải phải là một danh từ tiếng Anh.
- Không chứa dấu cách.
- snake_case 🐍

```php
<?php
return [
    // Bad
    "users-per-page" => 10,
    "toursPerPage" => 10,
    // Good
    "users_per_page" => 10,
    "tours_per_page" => 10,
];
