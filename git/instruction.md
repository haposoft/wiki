# Các lệnh Git cơ bản
## Config các thông tin Git
Config tên user :  
```
git config --global user.name "James Nguyen"
```  
Config email :  
```
git config --global user.email "damnn@haposoft.con"
```  
Sư dụng `--global` khi muốn áp dụng config cho tất cả các dự án.  
Hiển thị các config đang sử dụng:  
```
git config --list
```  
## Khởi tạo hoặc clone 1 repository về máy
Khởi tạo 1 repository từ thư mục code có sẵn
```
cd your-project/
git init
```
Clone 1 repository
```
git clone https://github.com/haposoft/repository.git
```
Clone 1 repository tại thư mục hiện tại
```
git clone https://github.com/user/repository.git .
```
### Thao tác với file
Thêm file mới :
```
git add file-name  
//thêm các file trong 1 thư mục
git add folder-name/
//thêm tất cả các file mới
git add * 

```
Update code mới nhất
```
git pull origin master
```
Xem thay đổi (chưa đc add) của những file hiện tại : 
```
git diff
//đã được add, chưa commit
git diff --cached
//thay đổi giữa hai commits
git diff COMMIT_ID1 COMMIT_ID2
```
Kiểm tra status của repository : 
```
git status
```
Commit những file thay đổi
```
git commit -m "Ghi chú cho nội dung thay đổi"
```
Đổi tên, Di chuyển, Xoá files
```
git rm file-removeme folder/file
git mv file-oldname file-newname
git commit -m "remove and rename file"
```
Thay đổi message commit :
```
git commit --amend -m "Change message"
```
Push các commit ở local lên 1 nhánh của repository
```
git push origin master
//push lên nhánh đang làm việc
git push origin branch-working
```
Xem logs 
```
git log
```
Revert commit
```
git revert COMMIT_ID
git push origin master
//revert commit chưa push
git reset origin/master
//reset về trạng thái của remote
git fetch origin
git reset --hard origin/master
```
## Thao tác với nhánh
Liệt kê các nhánh
```
//trên local
git branch
//xem tất cả
git branch -a
```
Tạo một nhánh
```
//chuyển sang nhánh master
git checkout master
//lấy code mới nhất
git pull origin master
//tạo nhánh mới
git branch new-branch
//chuyển sang nhánh mới
git checkout new-branch
//Tạo nhánh mới và đồng thời chuyển nhánh
git checkout -b new-branch
```
Merge code từ nhánh khác
```
//merge các commits của branch-name vào branch hiện tại
git merge branch-name
//Merge 1 nhánh nhưng không commit
git merge branch-name --no-commit --no-ff
```
Push code lên 1 nhánh
```
git push origin branch-name
```
Get tất cả các nhánh
```
git fetch origin
```
Xóa 1 nhánh
```
git branch -d branch-name
```
Tìm các file bị conflict
```
grep -H -r "<<<" *
grep -H -r ">>>" *
grep -H -r '^=======$' *
```