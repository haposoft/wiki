# HTML&CSS coding convention
#HTML Convention

##Tất cả các thẻ (tags) phải là chữ thường
```
<table></table>
<form></form>
```

###Sử dụng tên ý nghĩa khi đặt cho ID và các phần tử HTML
```
txtName, txtAge
```
thay vì
```
text1, text2
```

###Indent HTML code consistently (Thụt lề cho mã HTML)
```
<body>
    <form name="frmActivity" method="post" action="<?php echo $formAction;?>">
        <input type="hidden" name="sqlState" value="">
        <input type="hidden" name="delState" value="">
        <input type="hidden" name="activityId" value="">
        <label for="cmbProjectId"></label>
        <select name="cmbProjectId">
            <option value="value1"></option>
        </select>
    </form>
</body>
```

###Không sử dụng inline style attributes
Hạn chế sử dụng nó càng ít càng tốt, điều này có những lợi thế sau:
- Có thể dễ dàng chỉnh sửa giao diện cho mã HTML
- Có thể kế thừa CSS nếu bạn muốn sử dụng lại nó ở 1 nơi khác.
```
<!-- INSTEAD OF -->
<div style="width:100px;align:center;">

<!-- USE -->
<div class="message">
```

###Sử dụng 1 file CSS riêng không đặt trong trang HTML

###Tuân thủ W3C validate
- Việc này giúp website của bạn tối ưu được các đoạn mã HTML và hỗ trợ cho SEO
- Có thể check W3C validate trên trang https://validator.w3.org/

# CSS Convention

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

###Đặt tên cho class
- Khi đặt tên cho class theo cấu trúc `[Tên viết tắt của dự án]-[Chức năng của section]`

###Phân chia section rõ ràng
- Phân chia section rõ ràng với từng chức năng của nó

Đặt tên class theo chức năng và hướng tới "Đối tượng"
