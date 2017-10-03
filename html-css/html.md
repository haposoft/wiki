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