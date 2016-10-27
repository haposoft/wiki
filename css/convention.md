# Định dạng 

* Sử dụng 4 khoảng trắng 
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

* Giữa selector và `{` phải có khoảng trắng ` `

### Không tốt 
    .selector{
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

* Khi sử dụng `@include` đặt tất cả `@include` ở sau cùng các css rules

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

# OOCSS và BEM

## OOCSS

OOSCSS là cách sử dụng CSS, tối đa việc tái sử dụng class.

Ví dụ 

    .btn-submit{
        // some styles
        padding : 10px 5px;
    }

    .btn-connect{
        // some styles
        padding : 10px 5px;
    }

nên viết thành

    .btn{
        padding : 10px 5px;
    } 

    .btn-submit{
        // some styles
    }

    .btn-connect{
        // some styles
    }

Đặt tên class theo chức năng và hướng tới "Đối tượng"

## BEM 

Là 1 cách đặt tên class theo đối tượng

Ví dụ 

    .btn--primary{
       // ...
    }

    .btn__primary{
        // ...
    }
