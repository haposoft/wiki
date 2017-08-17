# Workflow cơ bản của Git
Để bắt đầu làm việc với Git, nếu bạn là người start project thì bạn cần tạo 1 repository mới với:
```
cd your-project/
git init
```
Trong trường hợp đã có repository, thì bạn cần clode repository đó về máy: 
```
git clone https://github.com/haposoft/repository.git
```
Nhánh hiện tại bây giờ đang là `master`, trong trường bạn cần làm 1 feature mới hay fix bug, hãy tạo 
1 nhánh mới để làm các công việc đó thay vì thao tác trên nhánh `master`. Tại sao lại như vậy ? 
Có 1 vài lý do như sau : 
- Trong quá trình bạn đang làm việc, nếu có bug, bạn có thể commit code ở nhánh bạn mới tạo, quay trở lại master để fix bug  
- Code của bạn chưa xong nhưng ở nhánh master có code của thành viên mới cần merger để bạn có thể code tiếp.
- Code của bạn cần được review trước khi các thành viêc khác của team có thể pull code mới của bạn về.
- Sau khi push code, bạn muốn thay đổi code của bạn mà không làm ảnh hưởng đến các member khác.  
- Xem lại lịch sử code theo nhánh 1 cách dễ dàng hơn.
Đó là 1 vài lý do mà tại sao bạn phải tạo 1 nhánh mới khi bạn muốn thay đổi hay thêm mới trong code.
Chúng ta sẽ tạo 1 nhánh mới và đồng thời chuyển sang nhánh đó để thực hiện code :
```
git checkout -b new-branch
```
Sau khi thực hiện code xong, kiểm tra lại status của nhánh hiện tại để xem xem có những file nào thay đổi,
file nào được thêm mới để thực hiện `add` và `commit`
```
git status
```
Add các file bạn tạo mới trước khi `commit`
```
git add file-name  
//thêm các file trong 1 thư mục
git add folder-name/
//thêm tất cả các file mới
git add * 
```
Thực hiện commit :
```
git commit -m `message for change`
```
Lưu ý trong nội dung message của commit bạn nên ghi tóm tắt những công việc hoặc thay đổi mà bạn đã làm trong commit đó  
Trước khi thực hiện push code lên, bạn cần pull code ở nhánh master để kiểm tra xem có các thay đổi mới nào 
nếu các thay đổi đó trong cùng 1 file với các file bạn đang sửa thì có thể bị conflict.
```
git pull origin master
```
Nếu gặp conflict, bạn cần fix hết tất cả các confict. Sau đó thực hiện commit lại 1 lần nữa.
```
git commit -m `fix conflict`
```
Cuối cùng thực hiện push lên nhánh hiện tại
```
git push origin new-branch
```