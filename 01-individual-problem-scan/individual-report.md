# Individual Problem Scan — Day 02

## Thông tin học viên

| Họ và tên | Mã học viên |
|---|---|
| Nguyễn Đại Quân | 2A202601933 |

## 1. Scan rộng các vấn đề

Ý tưởng xuất phát từ trải nghiệm thanh toán hằng ngày qua mobile banking và ví điện tử. Các khoản chi nhỏ diễn ra nhanh, nhiều lần và riêng lẻ nên người dùng khó nhìn thấy tác động cộng dồn lên ngân sách.

| # | Lăng kính | Problem quan sát được | Ai chịu ảnh hưởng? | Dấu hiệu thật / điều cần kiểm chứng |
|---:|---|---|---|---|
| 1 | Lặp lại | Nhiều khoản chi nhỏ từ 20.000–100.000 VNĐ phát sinh gần như mỗi ngày nhưng người dùng không nhận ra tổng tiền đã tăng nhanh đến mức nào. | Sinh viên và người trẻ thường xuyên thanh toán không tiền mặt. | Quan sát cá nhân: giao dịch nhỏ xuất hiện gần như mỗi ngày; cần ghi log 14 ngày để có baseline chính xác. |
| 2 | Tốn thời gian | Cuối tháng phải xem lại lịch sử giao dịch để nhớ tiền đã dùng vào đâu, nhưng số lượng giao dịch nhỏ khiến việc tổng hợp thủ công khó và mất thời gian. | Người dùng nhiều mobile banking/ví điện tử. | Đến cuối tháng số dư còn ít nhưng khó nhớ mục đích của từng khoản; cần đo thời gian tổng hợp thực tế. |
| 3 | AI có thể hỗ trợ tốt hơn | Thông báo giao dịch chỉ cho biết một khoản tiền vừa được trừ, chưa đặt khoản chi vào bối cảnh ngân sách theo danh mục và xu hướng cả tháng. | Người đã đặt ngân sách nhưng không theo dõi liên tục. | Người dùng thường chỉ nhận ra mình vượt ngân sách sau khi số dư giảm đáng kể. |
| 4 | Pain từ tác động bên ngoài | Khuyến mãi, voucher và quảng cáo từ ứng dụng mua sắm/giao đồ ăn kích thích quyết định mua nhanh theo cảm xúc. | Người thường xuyên dùng ứng dụng thương mại điện tử và giao đồ ăn. | Có nhiều thông báo tạo cảm giác phải mua ngay; cần kiểm chứng mối liên hệ giữa thông báo và giao dịch phát sinh. |
| 5 | Lặp lại + tốn thời gian | Cùng một merchant có thể xuất hiện với mô tả giao dịch khó hiểu hoặc không đồng nhất, khiến người dùng phải tự phân loại lại. | Người muốn quản lý chi tiêu theo danh mục. | Có thể kiểm tra bằng lịch sử giao dịch thực tế và tỷ lệ giao dịch không tự nhận diện được. |
| 6 | Workflow | Dữ liệu chi tiêu có thể nằm ở nhiều nguồn nên người dùng không có một góc nhìn tổng hợp về ngân sách. | Người sử dụng đồng thời tài khoản ngân hàng và ví điện tử. | Đây là giả thuyết cần kiểm chứng: đếm số nguồn thanh toán và mức độ thiếu hụt dữ liệu khi chỉ xem một ứng dụng. |

Lưu ý: các con số chưa được đo được ghi rõ là giả thuyết hoặc mục tiêu pilot, không được xem là kết quả thực tế.

## 2. Top 3 Problem Cards

| Rank | Problem | Vì sao chọn | Điều còn chưa chắc |
|---:|---|---|---|
| 1 | Không có cảnh báo ngân sách theo ngữ cảnh khi phát sinh khoản chi nhỏ. | Pain lặp lại hằng ngày, workflow rõ và có thể đo bằng số giao dịch, tổng tiền và tỷ lệ vượt ngân sách. | Khả năng nhận dữ liệu đủ sớm để cảnh báo trước giao dịch phụ thuộc vào tích hợp với ngân hàng/ví. |
| 2 | Phân loại và tổng hợp lịch sử giao dịch cuối tháng mất thời gian. | Có đầu vào/đầu ra rõ, phù hợp để kết hợp rule với AI và dễ làm MVP bằng dữ liệu CSV. | Độ chính xác phân loại trên mô tả giao dịch tiếng Việt và tên merchant không đồng nhất. |
| 3 | Khuyến mãi và voucher thúc đẩy giao dịch bốc đồng. | Tác động trực tiếp đến hành vi chi tiêu và có non-AI alternative rõ ràng. | Khó chứng minh quan hệ nhân quả; cần nhật ký hành vi hoặc phỏng vấn người dùng. |

---

## 3. Problem Card #1 — Cảnh báo chi tiêu theo ngữ cảnh

### Problem một câu

Người dùng trẻ thanh toán nhiều khoản nhỏ từ 20.000–100.000 VNĐ gần như mỗi ngày nhưng không nhìn thấy tác động cộng dồn lên ngân sách tại thời điểm ra quyết định, nên dễ chi vượt kế hoạch và chỉ phát hiện khi số dư đã giảm mạnh.

### Actor

Nguyễn Đại Quân và những sinh viên/người trẻ thường xuyên sử dụng mobile banking, ví điện tử, ứng dụng mua sắm và giao đồ ăn.

### Thời điểm / bối cảnh

Khi người dùng chuẩn bị hoặc vừa hoàn tất một giao dịch chi tiêu không thiết yếu như cà phê, đồ ăn giao tận nơi, mua sắm hoặc giải trí.

### Current workflow

1. Người dùng nhận nhu cầu hoặc bị kích thích bởi khuyến mãi/voucher.
2. Người dùng mở ứng dụng và chọn sản phẩm.
3. Người dùng thanh toán nhanh qua mobile banking hoặc ví điện tử.
4. Ứng dụng gửi thông báo cho một giao dịch riêng lẻ.
5. Người dùng tiếp tục các khoản chi khác mà không thấy tổng chi theo danh mục.
6. Cuối tháng người dùng kiểm tra số dư và xem lại lịch sử giao dịch.

### Bottleneck

Bước 3–4: tại thời điểm quyết định, người dùng thiếu thông tin như đã dùng bao nhiêu phần trăm ngân sách, đây là lần chi thứ mấy trong tuần và tốc độ chi hiện tại có dẫn đến vượt ngân sách hay không.

### Impact

- Khó kiểm soát tổng chi tiêu không thiết yếu.
- Khó duy trì mục tiêu tiết kiệm.
- Mất thời gian truy ngược lịch sử giao dịch vào cuối tháng.
- Cảm giác hối tiếc hoặc bất ngờ khi số dư còn ít nhưng không nhớ rõ tiền đã được dùng vào đâu.

### Success metric

Baseline cần đo trong 14 ngày:

- Số lượng và tổng giá trị giao dịch 20.000–100.000 VNĐ.
- Ngân sách theo từng danh mục và số lần vượt ngân sách.
- Số giao dịch người dùng tự đánh dấu là “không có kế hoạch”.
- Thời gian cần để tổng hợp chi tiêu cuối tuần/cuối tháng.

Mục tiêu cho pilot 4 tuần:

- Tự phân loại đúng ít nhất 85% giao dịch trên tập dữ liệu người dùng đã xác nhận.
- Hiển thị được trạng thái ngân sách cho ít nhất 90% giao dịch có dữ liệu đầu vào hợp lệ.
- Giảm ít nhất 20% tổng giá trị các giao dịch không có kế hoạch so với baseline cá nhân.
- Giảm ít nhất 50% thời gian tổng hợp chi tiêu cuối kỳ.
- Tỷ lệ cảnh báo bị người dùng đánh dấu “không hữu ích” dưới 20%.

Các mục tiêu trên là giả thuyết pilot và phải được điều chỉnh sau khi có baseline.

### Non-AI alternative

- Đặt hạn mức chi tiêu theo danh mục.
- Dùng phương pháp phong bì ngân sách.
- Tắt thông báo khuyến mãi.
- Dùng checklist “chờ 10 phút trước khi mua”.
- Dùng rule cố định, ví dụ cảnh báo khi ngân sách còn dưới 20%.

Rule có thể giải quyết phần lớn trường hợp cơ bản; AI chỉ nên được dùng cho phân loại mô tả khó, phát hiện xu hướng và tạo thông điệp theo ngữ cảnh.

### AI hypothesis

Một workflow có AI hỗ trợ có thể:

1. Chuẩn hóa và phân loại giao dịch.
2. Nhận biết chi tiêu lặp lại hoặc tăng bất thường so với baseline cá nhân.
3. Dự báo thời điểm có thể vượt ngân sách theo tốc độ chi hiện tại.
4. Tạo cảnh báo ngắn, trung lập và có bằng chứng, ví dụ:
   - “Đây là lần mua cà phê thứ 5 trong tuần.”
   - “Bạn đã dùng 85% ngân sách ăn uống tháng này.”
   - “Nếu giữ mức chi trung bình 4 ngày gần đây, ngân sách ăn uống có thể hết sau khoảng 4 ngày.”

### Quick gut

Chọn: **Workflow**, chưa cần Agent.

Lý do: luồng xử lý tuyến tính và dễ kiểm soát: nhận giao dịch → phân loại → cập nhật ngân sách → tính rule/dự báo → gửi cảnh báo. Hệ thống không cần tự lập kế hoạch hoặc tự quyết định gọi nhiều công cụ như một Agent.

### Draft current workflow

~~~text
CURRENT STATE

[Nhận nhu cầu/khuyến mãi]
→ [Chọn sản phẩm]
→ [Thanh toán rất nhanh]
→ [Nhận thông báo của một giao dịch]
→ [Không thấy tác động cộng dồn]
→ [Cuối tháng xem lại lịch sử]  <-- bottleneck
~~~

### Draft future workflow

~~~text
FUTURE STATE — MVP

[Nhận dữ liệu giao dịch hợp lệ]
→ [Rule chuẩn hóa merchant]
→ [Rule/AI phân loại danh mục]
→ [Budget engine tính tỷ lệ đã dùng]
→ [Rule phát hiện ngưỡng hoặc xu hướng bất thường]
→ [Gửi cảnh báo có số liệu]
→ [Người dùng xác nhận/sửa danh mục]
→ [Báo cáo tuần]

Human boundary:
- Người dùng đặt ngân sách và quyết định có mua hay không.
- Người dùng có thể tắt cảnh báo hoặc sửa phân loại.

Fallback:
- AI có độ tin cậy thấp → gắn “Chưa phân loại”, không đưa kết luận mạnh.
- Không có dữ liệu thời gian thực → cập nhật sau giao dịch hoặc cho phép
  người dùng nhập số tiền để kiểm tra trước khi mua.
~~~

### Boundary

- Không tự chặn, hủy hoặc thực hiện giao dịch.
- Không yêu cầu hay lưu mật khẩu, mã PIN hoặc OTP ngân hàng.
- Không đưa ra lời khuyên đầu tư/tín dụng.
- Không dùng giọng điệu phán xét người dùng.
- Không khẳng định dự báo là chắc chắn.
- Cảnh báo “trước thanh toán” chỉ được triển khai khi có API/tích hợp chính thức; MVP không giả định có quyền can thiệp vào ứng dụng ngân hàng.

---

## 4. Problem Card #2 — Phân loại và tổng hợp giao dịch cuối kỳ

### Problem một câu

Người dùng mất thời gian xem lại nhiều giao dịch nhỏ vào cuối tháng vì mô tả giao dịch rời rạc và không được tự động gom theo danh mục dễ hiểu.

### Actor

Người dùng cá nhân có nhiều giao dịch qua ngân hàng và ví điện tử, muốn biết tiền đã được dùng vào đâu.

### Thời điểm / bối cảnh

Cuối tuần hoặc cuối tháng, khi người dùng kiểm tra ngân sách và mục tiêu tiết kiệm.

### Current workflow

1. Mở lịch sử của từng ứng dụng thanh toán.
2. Đọc từng dòng mô tả giao dịch.
3. Cố nhớ merchant và mục đích chi.
4. Tự ghi vào ghi chú hoặc bảng tính.
5. Cộng tổng theo nhóm.
6. Đối chiếu với số dư hiện tại.

### Bottleneck

Bước 2–4: mô tả merchant không đồng nhất, số lượng giao dịch lớn và người dùng không còn nhớ bối cảnh của từng khoản.

### Impact

Người dùng mất thời gian tổng hợp, có thể phân loại sai và khó rút ra thói quen chi tiêu đủ sớm để điều chỉnh.

### Success metric

- Đo thời gian tổng hợp hiện tại trên lịch sử giao dịch 30 ngày.
- Độ chính xác phân loại mục tiêu từ 85% trở lên sau khi người dùng xác nhận.
- Giảm ít nhất 50% thời gian tạo báo cáo tháng.
- 100% giao dịch có thể được người dùng sửa danh mục và lưu feedback.

### Non-AI alternative

Dùng bảng mapping merchant cố định, regex theo nội dung chuyển khoản, hoặc yêu cầu người dùng chọn danh mục ngay sau mỗi giao dịch.

### AI hypothesis

Rule xử lý merchant quen thuộc; mô hình phân loại hoặc LLM chỉ xử lý mô tả chưa biết. Feedback của người dùng được lưu thành rule cá nhân cho lần sau, nhờ đó giảm chi phí và tăng tính nhất quán.

### Quick gut

Chọn: **Workflow kết hợp Rule + AI fallback**.

### Draft workflow trước/sau

~~~text
CURRENT
[Mở nhiều lịch sử] → [Đọc từng dòng] → [Tự nhớ mục đích]
→ [Tự phân loại] → [Cộng tổng] → [Rút ra kết luận]

FUTURE
[Import CSV/API được cấp phép] → [Chuẩn hóa dữ liệu]
→ [Rule phân loại merchant quen] → [AI xử lý trường hợp mơ hồ]
→ [Người dùng duyệt/sửa] → [Tổng hợp dashboard]
~~~

---

## 5. Problem Card #3 — Khuyến mãi kích thích mua hàng bốc đồng

### Problem một câu

Thông báo khuyến mãi và voucher tạo cảm giác cần mua ngay nhưng không cung cấp bối cảnh ngân sách, khiến người dùng dễ thực hiện giao dịch không nằm trong kế hoạch.

### Actor

Người dùng trẻ thường xuyên nhận thông báo từ ứng dụng mua sắm, giao đồ ăn và ví điện tử.

### Thời điểm / bối cảnh

Khi nhận flash sale, voucher có thời hạn hoặc miễn phí vận chuyển.

### Current workflow

1. Nhận thông báo khuyến mãi.
2. Mở ứng dụng vì sợ bỏ lỡ ưu đãi.
3. Chọn sản phẩm để đủ điều kiện dùng voucher.
4. Thanh toán nhanh.
5. Sau đó mới cân nhắc mức độ cần thiết của giao dịch.

### Bottleneck

Giữa bước 2 và 4 không có khoảng dừng để người dùng đối chiếu nhu cầu thật, ngân sách còn lại và các khoản tương tự đã mua.

### Impact

Tăng số giao dịch không có kế hoạch và có thể khiến người dùng mua thêm chỉ để đạt điều kiện khuyến mãi.

### Success metric

- Trong 14 ngày, ghi lại số lần mở ứng dụng sau thông báo khuyến mãi và số giao dịch phát sinh trong vòng 30 phút.
- Đo số giao dịch người dùng tự đánh dấu là bốc đồng.
- Pilot mục tiêu giảm 20% số giao dịch bốc đồng mà không tăng tỷ lệ tắt toàn bộ cảnh báo ngân sách.

### Non-AI alternative

Tắt thông báo marketing, đặt chế độ focus, áp dụng quy tắc chờ 10 phút hoặc danh sách mua sắm có sẵn. Đây có thể là giải pháp đủ tốt và ít rủi ro hơn AI.

### AI hypothesis

Nếu người dùng chủ động cấp dữ liệu, hệ thống có thể so sánh giao dịch dự kiến với ngân sách và lịch sử để tạo một câu hỏi ngắn: “Khoản này chưa nằm trong kế hoạch và ngân sách mua sắm chỉ còn 120.000 VNĐ. Bạn vẫn muốn tiếp tục chứ?”

### Quick gut

Chọn: **Rule trước, Workflow nếu cần cá nhân hóa**. Không cần Agent.

### Draft workflow trước/sau

~~~text
CURRENT
[Nhận khuyến mãi] → [Mở app] → [Chọn hàng] → [Thanh toán] → [Hối tiếc]

FUTURE
[Nhận ý định mua/manual check] → [Đọc ngân sách còn lại]
→ [Rule kiểm tra ngưỡng] → [Hiển thị khoảng dừng 10 phút]
→ [Người dùng tự quyết định]
~~~

---

## 6. Card muốn pitch nhất

**Card được chọn:** Problem Card #1 — Cảnh báo chi tiêu theo ngữ cảnh.

### Pitch ngắn

Tôi thường phát sinh nhiều khoản thanh toán nhỏ từ 20.000–100.000 VNĐ qua mobile banking hoặc ví điện tử. Vì mỗi giao dịch diễn ra rất nhanh và thông báo chỉ hiển thị từng khoản riêng lẻ, tôi không nhận ra tác động cộng dồn lên ngân sách. Đến cuối tháng số dư còn ít, nhưng việc xem lại hàng loạt giao dịch khiến tôi khó biết mình đã tiêu quá tay ở đâu. Tôi muốn kiểm chứng một workflow kết hợp rule và AI để phân loại giao dịch, theo dõi ngân sách và đưa ra cảnh báo có ngữ cảnh, trong khi quyết định chi tiêu vẫn hoàn toàn thuộc về người dùng.

### Vì sao chọn

- Đây là pain xuất hiện gần như mỗi ngày.
- Có workflow và điểm can thiệp cụ thể.
- Có thể bắt đầu bằng rule thay vì xây Agent quá sớm.
- Có metric hành vi và thời gian để kiểm chứng.
- Có thể thử bằng dữ liệu cá nhân đã ẩn thông tin nhạy cảm mà chưa cần tích hợp ngân hàng thật.

### Câu hỏi muốn nhóm challenge

1. Cảnh báo sau giao dịch có còn tạo đủ giá trị nếu chưa thể tích hợp để cảnh báo trước thanh toán?
2. Làm sao phân biệt “chi tiêu bốc đồng” với một khoản chi nhỏ nhưng cần thiết mà không phán xét người dùng?
3. Rule cố định có giải quyết 70–80% nhu cầu mà không cần AI không?
4. Người dùng có sẵn sàng cung cấp lịch sử giao dịch để đổi lấy cảnh báo cá nhân hóa không?
5. Metric nào phản ánh thay đổi hành vi tốt hơn: số giao dịch, tổng tiền không có kế hoạch hay tỷ lệ tuân thủ ngân sách?

---

## 7. Đề xuất MVP và tech stack

### Scope MVP

Trong scope:

- Import giao dịch từ file CSV hoặc dữ liệu sandbox.
- Cho phép đặt ngân sách theo danh mục.
- Tự động phân loại giao dịch bằng rule trước, AI fallback sau.
- Dashboard ngày/tuần/tháng.
- Cảnh báo sau giao dịch và chức năng “kiểm tra trước khi mua” do người dùng chủ động nhập.
- Người dùng xác nhận/sửa danh mục và đánh dấu giao dịch có kế hoạch/không có kế hoạch.

Ngoài scope:

- Đăng nhập thay người dùng vào tài khoản ngân hàng.
- Đọc hoặc lưu OTP/PIN/mật khẩu.
- Tự động chuyển tiền, chặn giao dịch hoặc quyết định thay người dùng.
- Cam kết cảnh báo trước giao dịch khi chưa có API chính thức từ ngân hàng/ví.
- Đưa ra lời khuyên đầu tư, vay hoặc tín dụng.

### Kiến trúc đề xuất

~~~text
[Flutter Mobile App]
        |
        v
[FastAPI Backend]
        |
        +--> [Transaction Normalizer]
        +--> [Rule-based Categorizer]
        +--> [AI Classifier for ambiguous records]
        +--> [Budget & Trend Engine]
        +--> [Notification Service]
        |
        v
[PostgreSQL]
~~~

### Tech stack

| Thành phần | Công nghệ đề xuất | Vai trò |
|---|---|---|
| Mobile app | Flutter | Một codebase cho Android/iOS; nhập giao dịch, xem dashboard và nhận cảnh báo. |
| Backend API | Python + FastAPI | Validation dữ liệu, nghiệp vụ ngân sách và API cho ứng dụng. |
| Database | PostgreSQL | Lưu người dùng, ngân sách, merchant mapping, giao dịch và feedback phân loại. |
| Background jobs | Redis + Celery/RQ (chỉ thêm khi cần) | Xử lý import, phân loại theo lô và tổng hợp báo cáo. |
| Rule engine | Python rules/regex + merchant mapping | Xử lý trường hợp chắc chắn, rẻ và dễ giải thích. |
| AI layer | Mô hình phân loại nhẹ hoặc LLM với structured JSON output | Chỉ xử lý mô tả giao dịch mơ hồ; luôn trả confidence và schema cố định. |
| Analytics | Pandas + scikit-learn | Baseline, rolling average và phát hiện thay đổi bất thường đơn giản. |
| Notification | Firebase Cloud Messaging | Gửi cảnh báo theo ngưỡng và báo cáo tuần. |
| Deployment MVP | Docker Compose; backend có thể triển khai trên một dịch vụ cloud phù hợp | Tái lập môi trường và demo nhanh. |

### Vì sao không dùng Agent

MVP có workflow cố định và không cần AI tự lập kế hoạch. Rule engine phù hợp với ngân sách và ngưỡng; AI chỉ cần hỗ trợ phân loại hoặc diễn đạt cảnh báo. Dùng Agent sẽ làm tăng độ phức tạp, quyền truy cập và rủi ro mà chưa chứng minh thêm giá trị.

### Nguyên tắc dữ liệu và an toàn

- Chỉ lấy dữ liệu khi người dùng đồng ý rõ ràng.
- MVP ưu tiên CSV đã ẩn thông tin hoặc dữ liệu sandbox.
- Mã hóa dữ liệu khi truyền và khi lưu.
- Tách dữ liệu theo từng người dùng và cho phép xóa toàn bộ dữ liệu.
- Không gửi số tài khoản đầy đủ, OTP hoặc nội dung nhạy cảm không cần thiết đến mô hình AI.
- Mọi kết quả phân loại phải có khả năng sửa; trường hợp confidence thấp phải để “Chưa phân loại”.
- Cảnh báo phải nêu số liệu làm căn cứ, không dùng ngôn ngữ gây xấu hổ hoặc ép buộc.

## 8. Kế hoạch validation

1. Ghi log cá nhân trong 14 ngày để tạo baseline.
2. Phỏng vấn nhanh 3–5 người thường xuyên dùng mobile banking/ví điện tử.
3. Kiểm tra họ đang quản lý ngân sách bằng cách nào và bước nào khó nhất.
4. Dùng dữ liệu mẫu hoặc CSV đã ẩn thông tin để đo độ chính xác phân loại.
5. Chạy pilot 4 tuần với rule-only trước.
6. Chỉ thêm AI nếu các giao dịch mơ hồ còn chiếm tỷ lệ đáng kể hoặc cảnh báo rule-only chưa đủ hữu ích.
7. So sánh kết quả với baseline trước khi quyết định Go / Not Yet / No-Go.
