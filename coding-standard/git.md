# Git convention

## Cơ bản:

 Tuân theo mô hình [gitflow](http://nvie.com/posts/a-successful-git-branching-model/)
 Có thể ghi nhớ nhanh mô hình này bằng [cheatsheet](https://danielkummer.github.io/git-flow-cheatsheet/index.vi_VN.html)
 
 Có thể dùng Git Client để dễ dàng hơn trong việc quản lý:

* Mac & Windows [Source Tree](https://www.sourcetreeapp.com/)
 
## Quản lý branch: 

Làm trên branch riêng, ko push trực tiếp lên master, develop. Đặt tên theo chuẩn gitflow:
* Master: branch dùng cho việc deploy lên production 
* Develop: branch dùng cho việc deploy lên staging server. Nhánh này cũng là nhánh để bắt đầu một tính năng mới (mặc định checkout từ branch develop khi dev một tính năng mới).
* feature/myfeature: với  myfeature là tên tính năng mới bạn muốn dev, tất cả các tính năng mới khi dev sẽ tạo nhánh với tiền tố `feature/`
* hotfix/myfix: với myfix là tên của sửa đổi. Hotfix branch thường checkout từ master và sẽ merge vào cả develop và master sau khi sửa đổi nếu tính năng đang gặp lỗi trên production.


## Pull Request  

Tất cả các chức năng cần được dev trên branch riêng, để merge vào develop hoặc master cần gửi pull request.
Chỉ Team leader có thể push develop/master khi thực sự cần thiết, gặp trong tình huống gấp gáp。

### Cần gửi pull-request vào những thời điểm sau: 

1. Khi kết thúc việc dev một task được assign. Chú ý không gửi sourcode của nhiều task trong cùng một pull request. 
(Gây khó khăn trong việc review, sửa đổi và merge pull request).
 
2. Kết thúc buổi làm việc.
Trong trường hợp chưa làm xong nhưng đã kết thúc buổi làm việc của mình, trước khi về, cần commit và push tất cả lên branch riêng trên remote repository ( để người khác có thể tiếp tục công việc nếu cần gấp, hoặc trong trường hợp hôm sau bạn nghỉ, bạn có sự cố về máy móc ….). 
Tạo một pull request và thêm tiền tố [WIP] có nghĩa là work in progress ( đang thực hiện) vào title của pull request để toàn bộ team member biết là bạn đang hoàn thiện chức năng đó và chưa hoàn thành, chưa cần review. 

3. Trước khi bạn ra về hoặc dừng công việc. 
Tương tự như mục 2. Kết thúc buổi làm việc. Bạn cần gửi pull-request khi bạn gặp vấn đề đột xuất không tiếp tục được công việc nữa, hoặc kết thúc làm việc (đối với parttime dev). 


### Lưu ý:

1. Trước khi gửi pull-request, nhớ merge từ develop vào branch bạn muốn gửi pull-request hoặc rebase để cập nhật code mới nhất từ develop, để giảm thiểu việc khi bạn gửi pull-request lên thì gặp conflict với develop branch mà thành viên khác phải nhắc bạn giải quyết conflict gây tốn thời gian cho các member khác.
2. Với một số tình huống, khi việc review code trong team diễn ra khá lâu, mà bạn cần làm một task có chứa nội dung bị phụ thuộc bởi 1 pull request chưa được merge thì có thể checkout từ branch của pull request phụ thuộc đó, tiếp tục làm và gửi pull request. Lưu ý khi gửi pull request có commit của pull request trước đó chưa merge vào develop hoặc master thì cần comment trong description của pull request như ví dụ dưới đây.

![](/img/dependence_pr.png)
