//TODO: write about oocss here 

-OCSS là cách viết CSS theo kiểu hướng đối tượng,nó giúp cho chúng ta có thể tận dụng tối đa được mã nguồn và giúp phát triển cũng như bảo trì dự án tốt hơn

-2 Nguyên tắc cơ bản khi sử dụng OOCSS:

1)Tách biệt giữa cấu trúc và giao diện:

-không viết các thuộc tính liên quan tới cấu trúc (position, float, margin, padding….), giao diện(background, border, color…) vào 1 class.
-Lên kế hoạch trước khi viết mã cho 1 trang: Viết class riêng cho các yếu tố có tính chất lặp lại để có thể sử dụng lại nhiều nhất có thể.

2)Tách biệt giữa container(phần chưa nội dung) và content(nội dung)


-Quy tắc sử dụng selector:
 +Tránh sử dụng ID.
 +Tránh sử dung selector hậu duệ .(VD: .footer h3)
 +Không gắn class với 1 element.(VD: div.title)
 +Trừ các trường hợp đặc biệt thì tránh dùng !important
