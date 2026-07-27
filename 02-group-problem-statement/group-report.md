# Group Report — Day 02


## Thành viên nhóm


| STT | Họ và tên       | Mã học viên | Vai trò     |
|-----|-----------------|-------------|-------------|
| 1   | Trần Tuấn Linh  | 2A202601612 | Thành viên  |
| 2   | Trần Kiên       | 2A202601598 | Thành viên  |
| 3   | Nguyễn Đại Quân | 2A202601933 | Thành viên  |
| 4   | Nguyễn Phú Quang| 2A202602017 | Nhóm trưởng |


Bài nhóm chọn: **Số hóa datasheet PDF và tự động tạo file báo giá (BOM) cho kỹ sư bán hàng thiết bị B2B.**


Người gặp vấn đề: kỹ sư sales / nhân viên mua hàng ở công ty phân phối thiết bị. Mỗi lần khách hỏi giá, họ phải tra thông số từ nhiều file PDF của hãng rồi gõ tay vào một file Excel báo giá dài mấy chục dòng.


---


# 1. Nhật ký hội tụ


Mỗi bạn mang 3 vấn đề của mình lên, cả nhóm có khoảng 12 cái. Sau khi nghe hết, nhóm gom lại thành mấy nhóm cho dễ nhìn:


- Nhóm A: trích xuất và dùng lại dữ liệu kỹ thuật (bóc tách datasheet, tra tồn kho, tra thông số cũ).
- Nhóm B: tìm kiếm tài liệu (search quyết định cũ, FAQ sản phẩm).
- Nhóm C: tổng hợp báo cáo (báo cáo doanh số tuần).


Nhóm chọn đào sâu nhóm A vì có 2 bạn từng làm mảng phân phối thiết bị nên hiểu quy trình, và vấn đề này có số đo thời gian rõ.


Trong lúc bàn, ý tưởng thay đổi mấy lần:


- Lúc đầu tính làm **chatbot hỏi đáp catalog**. Nhưng nghĩ lại thì chatbot chỉ trả lời câu hỏi lẻ, không giúp làm xong cái file báo giá Excel — mà đó mới là việc mất thời gian nhất.
- Sau đó tính làm **AI đọc thẳng PDF rồi xuất luôn Excel**. Nhưng như vậy lần sau làm báo giá cho đúng sản phẩm đó thì AI lại phải đọc lại PDF từ đầu, tốn công và không lưu lại được gì.
- Cuối cùng nhóm chốt **candidate**: tách làm 2 bước. Bước 1 đọc PDF để lưu dữ liệu vào một database dùng chung. Bước 2 lấy dữ liệu trong database ra để tạo file báo giá. Làm vậy thì lần sau khỏi đọc lại PDF, xuất báo giá rất nhanh.


Ở đây mới là candidate problem, chưa phải chốt luôn. Nhóm vẫn kiểm chứng và so sánh các phương án ở bước sau.


---


# 2. Kiểm chứng và tham khảo


Nhóm hỏi nhanh 3 người quen làm sales kỹ thuật. Cả 3 đều nói đúng là phải gõ lại thông số từ PDF, mệt nhất là dò đúng mã Part Number rồi ghép vào file mẫu. Có 1 bạn nói nếu là sản phẩm quen thì họ copy từ báo giá cũ chứ không đọc lại PDF — chỗ này càng cho thấy việc lưu dữ liệu để dùng lại là hợp lý.


Về số liệu thời gian (30 phút cho 1 datasheet, 120 phút cho 1 báo giá 30 thiết bị): đây là **ước lượng** từ trải nghiệm mấy bạn trong nhóm và 3 người phỏng vấn, chưa bấm giờ đo thật. Nhóm ghi rõ để không nói quá.


Tham khảo vài công cụ đã có:


- Adobe PDF Extract: đọc được bảng trong PDF nhưng chỉ ra text thô, không biết đâu là mã đâu là mô tả. https://developer.adobe.com/document-services/apis/pdf-extract/
- LLM trả JSON theo schema: ép AI trả dữ liệu đúng field, nhưng PDF mờ thì dễ sai nên cần người kiểm. https://platform.openai.com/docs/guides/structured-outputs
- Excel template/macro: tạo file báo giá đúng form thì ổn định, chỗ này không cần AI.


Rút ra: không cần làm một agent tự chạy hết mọi thứ. Chỗ khó (đọc PDF) mới cần AI, còn chỗ tạo file Excel thì dùng template là đủ.


---


# 3. Workflow trước và sau


## Bước 1 — Số hóa 1 datasheet


Trước (khoảng 30 phút): kỹ sư mở PDF, dò bảng thông số bằng mắt, gõ lại từng dòng vào Excel, lưu. Chỗ mất thời gian và hay sai nhất là dò và gõ lại mã.


Sau (khoảng 1-3 phút):


```
Upload PDF
→ AI đọc và trích ra dữ liệu (JSON)        [chỗ dùng AI]
→ Người kiểm lại trên màn hình rồi bấm duyệt  [người kiểm]
→ Lưu vào database


Nếu AI không chắc chắn thì để trống và đánh dấu, người tự điền.
```


## Bước 2 — Tạo 1 báo giá (khoảng 30 thiết bị)


Trước (khoảng 120 phút): tra lại PDF hoặc báo giá cũ, copy từng mã dán vào file mẫu, dò lại lỗi rồi gửi. Chỗ nghẽn là copy-paste từng dòng.


Sau (khoảng 2-5 phút):


```
Chọn các mã thiết bị đã có trong database
→ Bấm tạo báo giá
→ Hệ thống đổ dữ liệu vào file Excel mẫu     [dùng template, không cần AI]
→ Người xem lại rồi gửi                       [người kiểm]


Nếu thiếu mã thì file báo lại dòng thiếu, người bổ sung tay.
```


## So sánh nhanh


| | Trước | Sau |
|---|---|---|
| Số hóa 1 datasheet | ~30 phút | ~1-3 phút |
| Tạo 1 báo giá | ~120 phút | ~2-5 phút |
| Rủi ro | Chậm, dễ gõ sai mã | AI có thể đọc sai, nên phải có người duyệt |


Điểm nghẽn mới là bước người duyệt, nhưng nhóm thấy chấp nhận được vì đó là chỗ kiểm chất lượng.


---


# 4. Problem Statement


| Mục | Nội dung |
|---|---|
| Người gặp vấn đề | Kỹ sư sales / mua hàng B2B, người lập báo giá thiết bị. |
| Workflow | Nhận yêu cầu → tra thông số trong PDF → gõ vào Excel → ghép báo giá theo mẫu → dò lỗi → gửi. |
| Điểm nghẽn | Dò và gõ tay thông số + mã Part Number từ PDF. |
| Tác động | Số hóa ~30 phút/file, báo giá ~120 phút/30 thiết bị, hay sai mã, khách chờ lâu. |
| Success metric | Số hóa 1 datasheet: từ ~30 phút xuống dưới 5 phút. Báo giá 30 thiết bị: từ ~120 phút xuống dưới 15 phút. Sai mã: dưới 1 lỗi/báo giá sau khi duyệt. Cách đo: bấm giờ trên 10 datasheet và 5 báo giá mẫu, so với bản người tự làm. |
| Boundary | Làm: đọc PDF ra dữ liệu, gợi ý field, tạo file Excel từ database. Không làm: không tự gửi cho khách, không tự bịa mã, không tự quyết giá bán. |
| Chỗ AI tham gia | Chỉ ở bước đọc PDF ra dữ liệu, trước khi người duyệt. Bước tạo Excel không dùng AI. |


---


# 5. Rule / Workflow / Agent


| Mức | Nếu làm ở bài này | Đủ khi nào | Vấn đề |
|---|---|---|---|
| Không dùng AI | Chuẩn hóa file mẫu, dặn nhau gõ cẩn thận | Đỡ lỗi format | Vẫn phải gõ tay từ PDF, vẫn chậm |
| Rule | Template Excel tự đổ dữ liệu từ database | Đủ cho bước tạo báo giá | Không đọc được PDF nhiều layout khác nhau |
| Workflow | AI đọc PDF → người duyệt → lưu → template tạo Excel | Hợp vì các bước đi theo thứ tự cố định | AI đọc sai nên cần người kiểm |
| Agent | AI tự đọc mọi nguồn, tự quyết, tự gửi | Chỉ cần khi luồng phức tạp, nhiều nhánh | Quá mức cần thiết, khó kiểm soát, dễ sai mã mà không ai bắt |


Nhóm chọn **Workflow**.


Lý do:


- Các bước đi theo thứ tự cố định, không cần AI tự nghĩ ra bước tiếp theo.
- Chỉ có đúng 1 chỗ cần AI là đọc PDF (vì mỗi hãng một kiểu trình bày). Các chỗ khác dùng Rule/template rẻ hơn và chắc hơn.
- Mã sản phẩm sai một ký tự là sai đơn hàng, nên phải giữ người duyệt ở giữa. Để Agent tự làm hết thì mất chỗ kiểm này.


Quy tắc bắt buộc:


- Mã và thông số là dữ liệu cứng, AI không được đoán. Không chắc thì để trống và đánh dấu.
- Dữ liệu nào cũng phải hiện lên cho người xem và bấm duyệt mới được lưu.


---


# 6. Quyết định cuối


| Câu hỏi | Trả lời |
|---|---|
| Người dùng và workflow rõ chưa? | Rồi |
| Metric đo được chưa? | Có mục tiêu và cách đo, nhưng baseline còn là ước lượng |
| Có đủ dữ liệu để làm chưa? | Có, PDF và file mẫu sẵn |
| AI sai thì có sao không? | Chấp nhận được vì có người duyệt trước khi lưu |
| Có người kiểm không? | Có, kỹ sư duyệt |
| Có cách không cần AI không? | Bước tạo báo giá thì có (Rule), bước đọc PDF thì không |


**Quyết định: Go, nhưng làm nhỏ trước ở bước số hóa datasheet. Phần cam kết con số cụ thể để Not Yet cho tới khi bấm giờ đo thật.**


Lý do: vấn đề và workflow rõ, AI chỉ nằm ở đúng chỗ nó mạnh (đọc PDF lộn xộn), phần rủi ro nhất là sai mã thì đã có người duyệt chặn lại. Chưa dám hứa con số vì thời gian hiện mới là ước lượng.


Làm thử nhỏ nhất: lấy 10 datasheet thật của nhiều hãng và 5 báo giá mẫu, chạy thử rồi bấm giờ xem mất bao lâu, bao nhiêu chỗ phải sửa tay, còn lọt sai mã nào không.


Nếu chạy tệ (người vẫn phải sửa tay quá 30% dữ liệu, hoặc AI để lọt sai mã) thì bỏ phần AI đọc PDF, quay lại nhập tay nhưng vẫn giữ database và template tạo báo giá.




