# Kiến trúc cơ bản của Git
## Snapshot
Như đã nói trong phần giới thiệu về Git, điểm mạnh của Git so với các Distributed Version Control System – DVCS khác 
chính là việc Git lưu trữ và xử lý dữ liệu. Với các hệ thống DVCS khác, việc lưu trữ thông tin thay đổi của các tập tin 
được lưu trữ dưới dạng danh sách, thông tin được lưu trữ như là một tập hợp các tập tin và 
các thay đổi được thực hiện trên mỗi tập tin theo thời gian.  
![Deltas](../images/deltas.png)
Git không lưu dữ liệu theo cách này, Mà thay vào đó Git lưu dữ liệu dưới dạn một tập hợp các "ảnh" (snapshot). 
Mỗi lần có "commit", hoặc thay đổi trạng thái, Git "chụp một bức ảnh" ghi lại nội dung của tất cả các tập tin tại thời điểm đó và tạo ra một tham chiếu tới "ảnh" đó. 
Trong trường hợp tập tin không có sự thay đổi nào, Git sẽ không lưu trữ tập tin đó mà chỉ tạo một liên kết tới tập tin gốc đã tồn tại trước đó. 
![Snapshot](../images/snapshots.png)
Đây chính là điểm tạo ra sự khác biệt giữa Git với các DVCS khác.
## Action
Các thông tin về lịch sử thay đổi các file hoàn toàn nằm trên máy tính của bạn, các thao tác với 
các tập tin bạn gần như có thể thực hiện ngay lập tức mà không cần lo lắng đến vấn đề tốc độ internet.
Ví dụ nếu bạn cần xem lịch sử thay đổi của 1 file ở thời điểm 1 tháng trước, Git sẽ tìm kiềm file đó 
trên máy bạn và ngay lập tức so sánh sự thay đổi giữa thời điểm hiện tại và 1 tháng trước thay vì 
việc bạn phải lấy thông tin tập tin đó từ 1 máy chủ từ xa. Đồng nghĩa với việc nếu Internet chỗ bạn 
quá kém, bạn bị mất kết nốt internet thì cũng không ảnh hưởng gì. Bạn vẫn có thể xem log, commit các thay đổi 
mới nhất ở local. Đến khi Internet quay trở lại, bạn chỉ đẩy code mới nhất lên.
## Tính toàn vẹn
Các file trong Git đều được băm trước khi lưu và được tham chiếu bằng mã băm đó vậy nên việc bạn bị mất 
trong khi truyền tải hoặc nhận dữ liệu là điều không thể. Cơ chế băm mà Git sử dụng là `SHA-1`. Một mã `SHA-1`
có định dạng như sau :
```24b9da6552252987aa493b52f8696cd6d3b00373```  
Thực tế, Git không sử dụng tên của các tập để lưu trữ mà bằng các mã băm từ nội dung của tập tin vào một cơ sở dữ liệu có thể truy vấn được.  
Tất các các hành động của bạn đều được Git ghi lại vào trong cơ sở dữ liệu. Mọi hành động này đều có thể 
khôi phục được, bạn không cần lo lắng đền việc bạn đã làm code lộn xộn sau mỗi lần commit mà không 
revert lại được code trước đấy. Lưu ý là chỉ sau khi bạn đã commit nhé.
## Trạng thái
Mỗi file trong Git được quản lý với 3 trạng thái : `committed`, `modified`, `staged`
* `committed` : các file của bạn đã được Git lưu trữ thành công
* `modified` : các file đã bị thay đổi nhưng chưa `commit`
* `stage` : đánh dấu sẽ `commit` phiên bản hiện tại của 1 tập tin đã `modified` trong lần `commit` sắp tới  
Trong 1 dự án sử dụng Git sẽ có 3 phần : thư mục Git, thư mục làm việc, staging area
![Status](../images/areas.png)
1. Thư mục Git  
Nơi lưu trữ các metadata và database cho dự án. Đây là phần quan trọng nhất của Git, được sao lưu về máy tính cá nhân 
khi bạn clone code từ 1 repository.
2. Thư mục làm việc  
Nơi lưu trữ source code dự án. Dữ liệu được lấy từ database nén trong thư mục Git
3. Staging area  
Là một tập tin nằm trong thư muc Git, bao gồm các thông tin về những gì sẽ được `commit` trong lần `commit` sắp tới. 
Hay còn được gọi là `index`.