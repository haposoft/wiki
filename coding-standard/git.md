# Git & Git Flow

## Cơ bản:

 Tuân theo mô hình [gitflow](http://nvie.com/posts/a-successful-git-branching-model/)
 Có thể ghi nhớ nhanh mô hình này bằng [cheatsheet](https://danielkummer.github.io/git-flow-cheatsheet/index.vi_VN.html)
 
 Có thể dùng Git Client để dễ dàng hơn trong việc quản lý:

* Mac & Windows [Source Tree](https://www.sourcetreeapp.com/)

## Quản lý các file trên git
### Các file cần ignore:
* File được tạo ra bởi IDE. Ví dụ: `.project`, `.idea` 
* File dependece của dự án mà có thể cài được bằng các phần mềm quản lý gói. Ví dụ: folder vendor trong dự án PHP có sử dụng composer, folder `node_module` trong các dự án javascript có sử dụng npm, folder `vendor` của các dự án Rails. 
* Các file biên dịch nhị phân.

### Các file không được ignore:
* File quy định version của các dependency của dự án. Ví dụ: với Composer là composer.lock, Rails là Gemfile.lock. Các file này lưu lại version chính xác của project, cần đồng bộ để khi deploy ở các thời điểm khác nhau sẽ không phát sinh lỗi khi bị thay đổi version so với thời điểm dev. 

  
## Quản lý branch: 

Làm trên branch riêng, ko push trực tiếp lên master, develop. Đặt tên theo chuẩn gitflow:
* Master: branch dùng cho việc deploy lên production 
* Develop: branch dùng cho việc deploy lên staging server. Nhánh này cũng là nhánh để bắt đầu một tính năng mới (mặc định checkout từ branch develop khi dev một tính năng mới).
* feature/myfeature: với  myfeature là tên tính năng mới bạn muốn dev, tất cả các tính năng mới khi dev sẽ tạo nhánh với tiền tố `feature/`
* hotfix/myfix: với myfix là tên của sửa đổi. Hotfix branch thường checkout từ master và sẽ merge vào cả develop và master sau khi sửa đổi nếu tính năng đang gặp lỗi trên production.


## Gửi Pull Request  

Tất cả các chức năng cần được dev trên branch riêng, để merge vào develop hoặc master cần gửi pull request.
Chỉ Team leader có thể push develop/master khi thực sự cần thiết, gặp trong tình huống gấp gáp。
###  Title của pull request:
Đặt title của Pull Request tương ứng với chức năng hoặc phần sửa chữa được thêm vào. Có thể add thêm một số tiền tố liên quan tới các hệ thống khác để dễ quản lý.

Ví dụ:

 [RM158]Create new TIL   Với RM158 có nghĩa là redmind task id 158, để member dễ hiểu.
 
### Description của pull request: 
* Mô tả về pull request.
* Lưu ý liên quan tới  cài đặt (nếu có)
* Lưu ý liên quan tới deploy (nếu có)
* Special Keyword Syntax của Github (nếu có): dùng để auto close issues khi merge pull request. [Đọc thêm tại đây](https://github.com/blog/1506-closing-issues-via-pull-requests)

### Label của pull request.

* high priority:  Thêm label có tên high priority cho pull request trong trường hợp cần review gấp.

### Thời điểm gửi pull request: 

1. Khi kết thúc việc dev một task được assign. Chú ý không gửi sourcode của nhiều task trong cùng một pull request. 
(Gây khó khăn trong việc review, sửa đổi và merge pull request).
 
2. Kết thúc buổi làm việc.
Trong trường hợp chưa làm xong nhưng đã kết thúc buổi làm việc của mình, trước khi về, cần commit và push tất cả lên branch riêng trên remote repository ( để người khác có thể tiếp tục công việc nếu cần gấp, hoặc trong trường hợp hôm sau bạn nghỉ, bạn có sự cố về máy móc ….). 
Tạo một pull request và thêm tiền tố [WIP] có nghĩa là work in progress ( đang thực hiện) vào title của pull request để toàn bộ team member biết là bạn đang hoàn thiện chức năng đó và chưa hoàn thành, chưa cần review. 

3. Trước khi bạn ra về hoặc dừng công việc. 
Tương tự như mục 2. Kết thúc buổi làm việc. Bạn cần gửi pull-request khi bạn gặp vấn đề đột xuất không tiếp tục được công việc nữa, hoặc kết thúc làm việc (đối với parttime dev). 



### Check list khi gửi pull request.

1. Trước khi gửi pull-request, nhớ merge từ develop vào branch bạn muốn gửi pull-request hoặc rebase để cập nhật code mới nhất từ develop, để giảm thiểu việc khi bạn gửi pull-request lên thì gặp conflict với develop branch mà thành viên khác phải nhắc bạn giải quyết conflict gây tốn thời gian cho các member khác.

2. Kiểm tra xem các file có trong pull request có file nào thừa thãi, chứa source code không cần thiết hay không? 

3. Kiểm tra xem các file có trong pull request còn các lệnh liên quan tới việc debug hay không?  Ví dụ: lệnh dd() trong Laravel, console.log(). Cần xoá các lệnh này đi để các chức năng hoạt động chính xác.

4. Trong trường hợp dự án có tích hợp CI server, cần kiểm tra xem kết quả chạy của CI server có success hay không, nếu có lỗi cần fix. 
5. Assign những người cần review vào phần reviewer của  pull request để họ biết mà ưu tiên review issues cho bạn.
6. Trong trường hợp, issues cần review gấp, add `high priority` label vào PR để member dễ theo dõi, và alert qua Slack cho member.


### Lưu ý:

1. Với một số tình huống, khi việc review code trong team diễn ra khá lâu, mà bạn cần làm một task có chứa nội dung bị phụ thuộc bởi 1 pull request chưa được merge thì có thể checkout từ branch của pull request phụ thuộc đó, tiếp tục làm và gửi pull request. Lưu ý khi gửi pull request có commit của pull request trước đó chưa merge vào develop hoặc master thì cần comment trong description của pull request như ví dụ dưới đây.

![](/img/dependence_pr.png)

## Review pull request: 
* Pull request phải được review không quá 24h sau khi được gửi. 
* Các pull request được gửi lên trước 16h30 (trong trường hợp giờ nghỉ là 17h30), tốt nhất cần được review trước khi kết thúc ngày làm việc hôm đó. 
Ví dụ:  1 pull request được gửi lên vào 10h sáng hay 16h chiều tốt nhất phải được team member review trước khi kết thúc ngày làm việc cùng ngày. 
* Các pull request được gửi lên khi hết giờ làm việc, tốt nhất được review vào đầu giờ sáng ngày làm việc hôm sau.
* Review bằng cách comment vào pull request, không nhắn tin qua các phương tiện chat khác. 
* Khi thấy pull request không có vấn đề gì, có thể merge, cần nhấn nút Approved để member khác biết là bạn đã đồng ý merge pull.
* Khi thấy có ý kiến review nào bạn thấy tốt, nhớ nhấn nút reaction để các member khác biết là có những người khác đồng tình với ý kiến đó.

## Merge pull request:
* Với dự án một người: vẫn làm trên branch riêng và tự merge pull request.  Lý do không push trực tiếp lên develop hoặc master vì cần track lại thay đổi theo từng pull request để có thể tiến hành code review hoặc lấy dữ liệu nâng cao chất lượng source cho công ty. 
* Với dự án 2 người: chỉ được merge pull khi người còn lại đã review và approved. Người approved sẽ merge luôn.
* Với dự án 3 người trở lên: được merge pull khi 2 người đã approved. Người thứ 2 review và approved xong sẽ merge luôn. 
