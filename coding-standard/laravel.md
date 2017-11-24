# Laravel coding convention

Laravel tuân thủ theo chuẩn PSR-2(coding standard) và PSR-4(autoloading standard).

Dưới đây là 1 số convention cần lưu ý:
 

### 1.  Tên Route
 Nếu `route name` là từ ghép  thì sử dụng `snake_case` . Ví dụ:
 ```
     Route('/download-file', [
         'as' => 'download_file',
         'uses' => ''FileController@download
         ])
 ```
 
### 2. Tên bảng Pivot 
  Tên bảng pivot được ghép tên dạng số ít của 2 bảng quan hệ theo thứ tự alpha bet.
  Ví dụ: 
  > bảng thứ nhất tên `users`, bảng thứ hai có tên `posts` thì bảng pivot có tên là `post_user`.
  Lý do bởi trong bảng chữ cái thì `p` đứng trước `u`.
  
### 3. Tên thư mục , tên file
  Tên thư mục và tên file viết theo dạng `snake` và ở dạng số .
  Ví dụ: `views`, `image_files`
 