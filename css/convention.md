# Định dạng 

* Sử dụng 2 khoảng trắng 
* Dùng OOCSS và BEM
* Không dùng ID làm selector

### Không tốt 
    #some-body {
      // ...
    }
 
### Tốt
    .some-body {
      // ...
    }

* Khi sử dụng multiple selectors , giữa các selector phải xuống dòng.

### Không tốt 
    .logo, .navigation, .title{
      // ...
    }

### Tốt 
    .logo, 
    .navigation, 
    .title {
      // ...
    }

* Giữa selector và `{` phải có khoảng trắng (1 space) ` `

### Không tốt 
    .selector{
      // ...
    }
    
    .selector       {
      // ...
    }

### Tốt 
    .selector {
      // ...
    }

* Sau `:` phải có khoảng trắng ` `

### Không tốt 
    .selector{
      width:100%;
    }

### Tốt 
    .selector {
      width: 100%;
    }

* Phải có dòng ngăn cách giữa các selector

### Không tốt 
    .selector{
      width:100%;
    }
    .bar{
      width:100%;
    }

### Tốt 
    .selector{
      width:100%;
    }

    .bar{
      width:100%;
    }

* Khi comment code nên dùng `//`
* Đặt class riêng cho JS, sử dụng tiền tố `js-`
* Khi sử dụng Border `0` thay vì `none`

### Không tốt 
    .foo {
      border: none;
    }

### Tốt 
    .foo {
      border: 0;
    }

# SCSS 

* SCSS selector tối đa 3 lever 

### Tốt 

    .lever-1{
      .lever-2{
        .lever-3{
          // Done
        }
      }
    }

* Khi sử dụng `@include` và `@extend` đặt tất cả `@include` ở sau cùng các css rules

### Tốt 

    .btn-green {
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);
      // ...
    }
* Giữa các selector phải có khoảng trống

### Tốt 

    .btn {
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);
      
      .icon {
        margin-right: 10px;
      }
    }

#Đặt tên cho class
- Khi đặt tên cho class theo cấu trúc `[Tên viết tắt của dự án]-[Chức năng của section]`

#Phân chia section rõ ràng
- Phân chia section rõ ràng với từng chức năng của nó

Đặt tên class theo chức năng và hướng tới "Đối tượng"
