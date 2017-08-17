# Git và Github là gì ? Tại sao nên sử dụng ?
## Git là gì ?
Git là tên gọi của một Hệ thống quản lý phiên bản phân tán (Distributed Version Control System – DVCS),
theo wiki thì Git là phần mềm quản lý mã nguồn phân tán được phát triển bởi [Linus Torvalds](https://vi.wikipedia.org/wiki/Linus_Torvalds) 
vào năm 2005, ban đầu dành cho việc phát triển [nhân Linux](https://vi.wikipedia.org/wiki/H%E1%BA%A1t_nh%C3%A2n_Linux). 
Hiện nay, Git trở thành một trong các phần mềm quản lý mã nguồn phổ biến nhất. Git là phần mềm mã nguồn mở 
được phân phối theo giấy phép công cộng [GPL2](https://vi.wikipedia.org/wiki/Gi%E1%BA%A5y_ph%C3%A9p_C%C3%B4ng_c%E1%BB%99ng_GNU).  
Hiểu theo 1 cách đơn giản, Git giúp chúng ta quản lý lịch sử của các files trong source code, lưu lại các phiên bản 
cho mỗi lần thay đổi file. Chúng ta có thể dễ dàng xem logs, revert, update code mới nhất của chính mình
cũng như các thành viên khác trong team. Cơ chế lưu trữ phiên bản của Git là nó sẽ tạo ra một “ảnh chụp” 
(snapshot) tương ứng với mỗi tập tin và thư mục sau khi commit, 
từ đó nó có thể cho phép chúng ta revert lại một ảnh chụp/phiên bản nào đó. 
Đây cũng chính là điểm mạnh của Git so với các DVCS khác. Git  không “lưu cứng” dữ liệu mà sẽ chỉ lưu dưới dạng ảnh chụp.
## Github là gì ?
Theo định nghĩa của wiki thì [GitHub](https://github.com/) là một dịch vụ cung cấp kho lưu trữ mã nguồn Git dựa trên nền web cho các dự án phát triển phần mềm. 
GitHub cung cấp cả phiên bản trả tiền lẫn miễn phí cho các tài khoản. 
Các dự án mã nguồn mở sẽ được cung cấp kho lưu trữ miễn phí. 
Tính đến tháng 4 năm 2016, GitHub có hơn 14 triệu người sử dụng với hơn 35 triệu kho mã nguồn, 
làm cho nó trở thành máy chủ chứa mã nguồn lớn trên thế giới.  
Giữa Git và Github, một số bạn có thể bị hiểu nhầm, Git là tên gọi của 1 Hệ thống quản lý phiên bản phân tán,
còn Github là 1 một dịch vụ cung cấp kho lưu trữ mã nguồn Git. Và Git thì có thể làm việc với bất kì máy chủ Linux nào.  
GitHub cung cấp chức năng social networking như là feeds, followers và network graph 
để các dev có thể học hỏi kinh nghiệm làm việc thông qua lịch sử mỗi lần commit.
## Tại sao nên sử dụng Git
Có rất nhiều lợi ích khi chúng ta sử dựng Git :
1. Git hoạt động theo mô hình Local và Remote repositories: Bạn có thể làm mọi thao tác trên local repository trên máy tính. 
Sau khi hoàn thành, đẩy code lên Remote repository để các thành viên trong team có thể review và lấy code của bạn về.
2. Git giúp bạn dễ dàng quản lý lịch sử thay đổi của files, bạn cũng như các thành viên trong team có thể dễ dàng thấy được những thay đổi trong code mới,
 cũng như revert lại các files code cũ nếu có vấn đề.
3. Bất cứ đâu bạn chỉ cần clone để có thể lấy code mới nhất của cả team, hoặc code bạn đang làm việc trên 1 nhánh nào về để tiếp tục công việc.
4. Dễ dàng hơn trong việc deployment trên server.