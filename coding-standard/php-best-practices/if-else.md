# clean code cho if else 2
## 1. Giữ đơn giản, dễ đọc và sử dụng toán tử logic một cách hiệu quả:
- Tránh việc sử dụng các điều kiện lồng nhau phức tạp, có thể làm code trở nên khó hiểu
- giúp giảm số lượng câu lệnh if-else và làm cho code ngắn gọn hơn

 **bad**
```php
if ($age >= 18 && $age <= 60) {
    if ($salary > 5000) {
        if ($position == "Manager") {
            // todo something
        }
    }
}
```
**good**
```php
if ($age >= 18 && $age <= 60 && $salary > 5000 && $position == "Manager") {
    // todo something
}
```
## 2.Xử lý các trường hợp mặc định hoặc đặc biệt hiệu quả:
-  thêm một câu lệnh else để xử lý các trường hợp không khớp với bất kỳ điều kiện if nào

**bad**
```php
if ($day == "Monday") {
    // Làm việc từ 9:00 đến 17:00
} else {
    if ($day == "Tuesday") {
        // Làm việc từ 10:00 đến 18:00
    } else {
        // Nghỉ làm
    }
}
```
**good**
```php
if ($day == "Monday") {
    // Làm việc từ 9:00 đến 17:00
} elseif ($day == "Tuesday") {
    // Làm việc từ 10:00 đến 18:00
} else {
    // Nghỉ làm
}
```
## 3.Sắp xếp các điều kiện một cách cẩn thận:
- Sắp xếp các điều kiện theo một thứ tự logic
- Đặt các điều kiện thường xảy ra nhất hoặc đơn giản nhất đầu tiên để cải thiện hiệu suất thực thi của chương trình.

**bad**
```php
function calculateGrade($score) {
    if ($score >= 90) {
        return 'A';
    } elseif ($score >= 80) {
        return 'B';
    } elseif ($score >= 70) {
        return 'C';
    } elseif ($score >= 60) {
        return 'D';
    } else {
        return 'F';
    }
}
```
**good**
```php
function calculateGrade($score) {
    if ($score < 60) {
     return 'F';
    } else {
       if ($score >= 90) {
            return 'A';
        } elseif ($score >= 80) {
            return 'B';
        } elseif ($score >= 70) {
            return 'C';
        } else {
            return 'D';
        }
    }
}
```
## 4.Giảm thiểu sự trùng lặp code:
- Tránh việc trùng lặp code trong các khối if và else. 
- Nếu có các tác vụ hoặc thao tác chung, hãy tách ra thành các hàm hoặc biến riêng biệt để tránh lặp lại code

**bad**
```php
if ($isLoggedIn) {
    // Hiển thị nút "Đăng xuất"
    echo '<a href="logout.php">Đăng xuất</a>';
    // Hiển thị chào mừng người dùng đã đăng nhập
    echo 'Chào mừng ' . $username;
} else {
    // Hiển thị nút "Đăng nhập"
    echo '<a href="login.php">Đăng nhập</a>';
    // Hiển thị chào mừng khách truy cập
    echo 'Chào mừng khách truy cập';
}
```
**good**
```php
if ($isLoggedIn) {
    // Hiển thị nút "Đăng xuất"
    $buttonText = 'Đăng xuất';
    $buttonLink = 'logout.php';
    $welcomeMessage = 'Chào mừng ' . $username;
} else {
    // Hiển thị nút "Đăng nhập"
    $buttonText = 'Đăng nhập';
    $buttonLink = 'login.php';
    $welcomeMessage = 'Chào mừng khách truy cập';
}

echo '<a href="' . $buttonLink . '">' . $buttonText . '</a>';
echo $welcomeMessage;
```
## 5.early returns:
- Giảm độ sâu của khối if-else lồng nhau, làm cho code dễ đọc và hiểu hơn
- Đưa ra các xử lý đặc biệt cho các trường hợp không hợp lệ sớm hơn, giúp tránh việc thực hiện các câu lệnh không cần thiết.

**bad**
```php
function calculateDiscount($amount, $isPremiumMember) {
    if ($amount > 100) {
        if ($isPremiumMember) {
            return $amount * 0.2; // Giảm giá 20% cho thành viên Premium nếu tổng số tiền mua hàng vượt quá 100
        } else {
            return $amount * 0.1; // Giảm giá 10% cho thành viên không Premium nếu tổng số tiền mua hàng vượt quá 100
        }
    } else {
        return 0; // Không giảm giá nếu tổng số tiền mua hàng không vượt quá 100
    }
}
```
**good**
```php
function calculateDiscount($amount, $isPremiumMember) {
    if ($amount <= 100) {
        return 0; // Không giảm giá nếu tổng số tiền mua hàng không vượt quá 100
    }

    if ($isPremiumMember) {
        return $amount * 0.2; // Giảm giá 20% cho thành viên Premium nếu tổng số tiền mua hàng vượt quá 100
    }

    return $amount * 0.1; // Giảm giá 10% cho thành viên không Premium nếu tổng số tiền mua hàng vượt quá 100
}
```