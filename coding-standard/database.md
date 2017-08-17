# Database Conventions

## Quy định về cách đặt tên
- Sử dung **Lowercase** cho việc đặt tên database, tên bảng, tên cột ..  
Ví dụ : `name`, `age`.
- Sử dụng dấu `_` khi nối các từ, điển hình như **[snake case](https://en.wikipedia.org/wiki/Snake_case)**.  
Ví dụ : `first_name`, `last_name`.
- Dùng tiếng anh để đặt tên, tên có tính tự giải thíc,tránh việc viết tắt gây khó hiểu cho người đọc.   
Ví dụ : nên đặt tên `middle_name` thay vì `mid_nm`.  
- Trong 1 số trường hợp từ quá dài, có thể sử dụng từ viết tắt phổ biến. 
Nếu cảm thấy chưa rõ ràng thì không nên dùng từ viết tắt.  
Ví dụ: [Internationalization và localization](https://en.wikipedia.org/wiki/Internationalization_and_localization) viết tắt thành `i18n` and `l10n`
- Không dùng [từ khóa MySql](https://dev.mysql.com/doc/refman/5.7/en/keywords.html) và kiểu dữ liệu để đặt tên.  
Ví dụ: `add`, `after`, ...
- Tên cột không cần thêm các tiền tố không cần thiết.
Ví dụ: Tên bảng `posts` không đặt `posts_title` mà chỉ cần `title`
- Khi đánh Indexes thì cần đặt tên rõ ràng, bao gồm cả tên bảng và tên cột được đánh index
- Các trường chỉ có 2 trạng thái TRUE/FALSE hoặc YES/NO thì nên thêm prefix `is_`  
Ví dụ: `is_active`, `is_admin`
- Đặt tên table bằng tiếng anh ở dạng số nhiều (thêm s, es, ...)  
Ví dụ: `users`, `categories`, `cities`
## Đặt tên cho các khóa
- Chỉ có 1 khóa chính đặt tên `id`
- Khóa ngoài được kết hợp từ tên bảng được tham chiếu đến và tên của trường được tham chiều.  
Ví dụ: `user_id` , `room_id`
- Đối với quan hệ nhiều nhiều, tạo bảng thứ 3 được đặt tên được kết hợp từ tên của bảng thứ nhất ở dạng số ít và 
tên của bảng thứ 2 ở dạng số ít. Có 2 khóa chính, khóa chính thứ nhất là `id` của bảng thứ nhất được đặt tên theo quy tắc đặt tên khóa ngoài, 
khóa chính thứ 2 là `id` của bảng thứ 2 được đặt tên theo quy tắc đặt tên khóa ngoài.  
Ví dụ: bảng `articles` và bảng `categories` được liên kết với nhau qua bảng thứ 3 `article_category` có 2 khóa chính là 
`article_id` và `category_id`.

## Thay đổi thông tin
- Khi thêm mới, sửa thì lưu thời gian thay đổi vào 2 trường `created_at` và `updated_at`
- Trong trường hợp không xóa vật lý mà chỉ xóa logic thì lưu thời gian xóa vào trường `deleted_at` 