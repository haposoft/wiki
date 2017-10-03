#OCSS là cách viết CSS theo kiểu hướng đối tượng,nó giúp cho chúng ta có thể tận dụng tối đa được mã nguồn và giúp phát triển cũng như bảo trì dự án tốt hơn

##2 Nguyên tắc cơ bản khi sử dụng OOCSS:

###Tách biệt giữa cấu trúc và giao diện:
1. không viết các thuộc tính liên quan tới cấu trúc (position, float, margin, padding….), giao diện(background, border, color…) vào 1 class.
2. Lên kế hoạch trước khi viết mã CSS cho 1 trang: Viết class riêng cho các yếu tố có tính chất lặp lại để có thể  tái sử dụng lại.
3. VD:
```
css.box1 {
  width: 25%;
  background: red;
  height: 150px;
  float: left;
}
.box2 {
  width: 25%;
  background: blue;
  height: 150px;
  float: left;
}
```
Như bạn thấy giữa .box1 và .box2 nó có các thuộc tính hoàn toàn giống nhau như width, height và float. Nên thay vì viết lại ở mỗi phần tử, chúng ta có thể gom nó vào một class chung nào đó rồi ở các class riêng bạn có thể chỉ cần thêm background cho nó mà thôi.Trước tiên là ta phải sửa HTML để sử dụng hai class:
```
 <div class="box box1"></div>
 <div class="box box2"></div>
```

Sau đó sử dụng CSS như sau:
```
.box {
   width: 25%;
   height: 150px;
   float: left;
}
 
.box1 { background: red }
.box2 { background: blue }
```
###Tách biệt giữa container(phần chứa nội dung) và content(nội dung):
 Giả sử bạn định dạng style như này cho thẻ h3 ở sidebar:
```
 #sidebar h3 {
   font-family: Arial, Helvetica, sans-serif;
   font-size: .8em;
   line-height: 1;
   color: #777;
   text-shadow: rgba(0, 0, 0, .3) 3px 3px 6px;
 }
```
 Bây giờ nêú bạn muốn định dạng cho 1 thẻ h3 khác ở footer
 có style giống thẻ này nhưng chỉ khác 2 thuộc tính font-size và text-shadow.Vậy chúng ta có mã CSS như sau:
```
 #sidebar h3, #footer h3 {
   font-family: Arial, Helvetica, sans-serif;
   font-size: 2em;
   line-height: 1;
   color: #777;
   text-shadow: rgba(0, 0, 0, .3) 3px 3px 6px;
}

 #footer h3 {
   font-size: 1.5em;
   text-shadow: rgba(0, 0, 0, .3) 2px 2px 4px;
}
```
 Hoặc tệ hơn là như này :
```
 #sidebar h3 {
   font-family: Arial, Helvetica, sans-serif;
   font-size: 2em;
   line-height: 1;
   color: #777;
   text-shadow: rgba(0, 0, 0, .3) 3px 3px 6px;
 }
 #footer h3 {
   font-family: Arial, Helvetica, sans-serif;
   font-size: 1.5em;
   line-height: 1;
   color: #777;
   text-shadow: rgba(0, 0, 0, .3) 2px 2px 4px;
 }
```
 Bạn thấy có khá nhiều dòng CSS bị lặp lại.Nếu chúng ta   làm theo kiểu OOCSS thì sẽ tách thẻ h3(vai trò là content)
ra khỏi sidebar và footer (vai trò là container) và tạo class riêng cho nó để tái sử dụng.

##Quy tắc sử dụng selector:
1. Tránh sử dụng ID.
2. Tránh sử dung selector hậu duệ .(VD: .footer h3)
3. Không gắn class với 1 element.(VD: div.title)
4. Trừ các trường hợp đặc biệt thì tránh dùng !important
