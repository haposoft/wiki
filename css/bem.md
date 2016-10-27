
#BEM (Block, Element, Modifier) là 1 quy tắc đặt tên cho các class trong HTML và CSS.Nó giúp cho lập trình viên hiểu rõ hơn về quan hệ giữa HTML và CSS trong 1 dự án.

##Cách đặt tên cho các thành phần: .[block-name]__[element_name]--[modifier-name]
	
1. Block được coi là thành phần lớn nhất: .btn {} .
2. Element là thành phần con của block và đằng trước tên của nó có thêm 2 dầu gạch dưới: .btn__price {} .
3. Modifier là thành phần thay đổi style của Block hoặc Element.Đằng trước tên của nó có thêm 2 dấu gạch ngang: .btn--orange {}, .btn__price--big .

````html
/* Thành phần Block, nó là class cho một nút bấm */
.btn {}
 
/* Thành phần phụ thuộc vào Block */ 
.btn__price {}
 
/* Modifier mà thay đổi style của Block */
.btn--orange {} 
.btn--big {}
.btn__price--big
````


##Quy tắc khi sử dụng vùng chọn cho CSS:

1. Chỉ sử dụng class selector.
2. Không sử dụng id và tagname.
3. Không sử dụng class selector mà bị phụ thuôc vào blocks/elements ở page đó: 


##Tại sao nên sử dụng bem:

1. Khi nhìn vào tên của 1 class thì có thể biết được nó phụ thuộc vào class nào hoặc nó định nghĩa cho thành phần HTML nào.
2. Khi tạo style mới cho 1 thành phần.Chúng ta có thể tận dụng lại các modifier có sẵn mà không cần viết mới.
   +Người thiết kế và người lập trình có thể nhất quán trong việc đặt tên các thành phần từ đó có thể giao tiếp dễ dàng hơn.
