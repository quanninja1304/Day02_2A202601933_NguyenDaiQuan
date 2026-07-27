# Individual Reflection — Day 02

## Thông tin học viên

| Họ và tên | Mã học viên | Vai trò trong nhóm |
|---|---|---|
| Nguyễn Đại Quân | 2A202601933 | Thành viên |

## 1. Tôi đã tham gia vào phần nào?

| Hoạt động | Tôi đã làm gì? | Kết quả / ảnh hưởng |
|---|---|---|
| Scan cá nhân | Bắt đầu từ trải nghiệm chi tiêu nhiều khoản nhỏ qua mobile banking và ví điện tử, sau đó phân tích theo bốn lăng kính: lặp lại, tốn thời gian, AI có thể hỗ trợ và tác động từ người khác. | Xác định được pain chính không phải là “thiếu một app AI”, mà là người dùng thiếu bối cảnh ngân sách tại thời điểm ra quyết định. |
| Pitch Problem Card | Chuẩn bị pitch cho Problem Card “Cảnh báo chi tiêu theo ngữ cảnh”, tập trung vào actor, workflow hiện tại, bottleneck và metric cần đo. | Ý tưởng có thể được trình bày theo hướng problem-first thay vì bắt đầu bằng chatbot hoặc Agent. |
| Challenge bài cá nhân | Tự đặt câu hỏi liệu cảnh báo sau giao dịch còn đủ giá trị, Rule có giải quyết phần lớn nhu cầu không và làm sao xác định một khoản chi là bốc đồng mà không phán xét người dùng. | Scope MVP được thu hẹp; không giả định ứng dụng có thể can thiệp trực tiếp vào giao dịch ngân hàng. |
| Gom trùng / cluster | Ý tưởng cá nhân được tách thành ba nhóm pain: thiếu cảnh báo ngân sách, khó phân loại giao dịch và tác động của khuyến mãi. | Nhìn ra ba vấn đề có liên quan nhưng không nên gộp thành một hệ thống quá lớn ngay từ đầu. |
| Chọn candidate problem | Ưu tiên card cảnh báo chi tiêu theo ngữ cảnh vì pain xảy ra thường xuyên, workflow rõ và có thể đo bằng dữ liệu cá nhân. | Có một candidate đủ cụ thể để validation bằng log 14 ngày và pilot nhỏ. |
| Validation / research | Đề xuất ghi log cá nhân 14 ngày, phỏng vấn 3–5 người và thử rule-only trước khi thêm AI. Hiện chưa có kết quả phỏng vấn hoặc số liệu baseline thực tế. | Tránh biến các con số mục tiêu thành “bằng chứng”; phân biệt rõ dữ kiện đã quan sát với giả thuyết cần kiểm chứng. |
| Workflow | Mô tả current workflow từ lúc nhận nhu cầu/khuyến mãi đến lúc cuối tháng xem lại lịch sử; xây future workflow theo chuỗi rule → AI fallback → budget engine → cảnh báo → feedback. | Xác định được human boundary, fallback và điểm mà AI thực sự có ích. |
| Problem Statement | Bổ sung actor, bối cảnh, bottleneck, impact, metric và boundary cho vấn đề chi tiêu bốc đồng. | Problem Statement đo được hơn và không còn dừng ở mô tả chung “giúp quản lý chi tiêu tốt hơn”. |
| Rule / Workflow / Agent | So sánh rule cảnh báo theo ngưỡng, workflow có AI hỗ trợ và Agent. | Chọn Workflow; Rule xử lý trường hợp chắc chắn, AI chỉ xử lý dữ liệu mơ hồ. Chưa có lý do đủ mạnh để dùng Agent. |
| Decision | Đề xuất pilot bằng CSV/dữ liệu sandbox và cảnh báo sau giao dịch hoặc chức năng kiểm tra thủ công trước khi mua. | **Go với pilot nhỏ cho phân loại và theo dõi ngân sách; Not Yet với cảnh báo trực tiếp trước giao dịch thật** cho đến khi có tích hợp chính thức và kiểm chứng nhu cầu. |

### Phần đóng góp nhóm cần tự xác nhận trước khi nộp

Bản ghi hiện tại chưa cho biết chính xác Nguyễn Đại Quân đã pitch/challenge hoặc phụ trách hạng mục nào trong candidate chung “Hệ thống số hóa Datasheet & Tự động tạo BOM”. Trước khi nộp, tôi cần bổ sung 2–3 câu về việc mình đã thực sự làm trong buổi nhóm, ví dụ:

- Câu hỏi tôi đã dùng để challenge candidate của bạn khác.
- Phần workflow, research, Problem Statement hoặc slide mà tôi trực tiếp phụ trách.
- Ý kiến của tôi đã làm nhóm thay đổi quyết định hoặc boundary như thế nào.

Tôi không ghi một đóng góp chưa xảy ra chỉ để làm reflection trông đầy đủ.

---

## 2. Bảng dùng AI trong quá trình làm bài

| Phase | Tôi dùng AI để làm gì? | AI hữu ích ở đâu? | AI sai/hời hợt hoặc dễ gây hiểu nhầm ở đâu? | Tôi sửa gì bằng nhận định của mình? |
|---|---|---|---|---|
| Scan | Sau khi tự mô tả trải nghiệm, tôi dùng AI để cấu trúc lại theo bốn lăng kính và tách các pain liên quan. | Giúp diễn đạt actor, dấu hiệu và phần cần kiểm chứng rõ hơn. | AI có thể tách một vấn đề thành nhiều dòng trông như nhiều problem độc lập dù chúng còn trùng nhau. | Giữ một pain trung tâm và ghi rõ các giả thuyết chưa có bằng chứng. |
| Problem Card | Nhờ AI sắp xếp ý tưởng theo actor, workflow, bottleneck, impact, metric và boundary. | Giúp chuyển mô tả giải pháp thành Problem Card đúng cấu trúc. | AI có xu hướng đưa ra con số mục tiêu dù chưa có baseline. | Ghi các con số là mục tiêu pilot và yêu cầu đo baseline 14 ngày trước. |
| Workflow | Dùng AI phản biện current/future workflow và đề xuất fallback. | Giúp thấy Rule có thể xử lý nhiều bước, AI chỉ cần xuất hiện ở phần phân loại mơ hồ và diễn đạt cảnh báo. | Ban đầu ý tưởng “cảnh báo trước khi thanh toán” nghe đơn giản nhưng thực tế phụ thuộc quyền truy cập dữ liệu và tích hợp với ngân hàng/ví. | Thu hẹp MVP về CSV/sandbox, cảnh báo sau giao dịch hoặc kiểm tra thủ công trước khi mua. |
| Research | Chưa dùng kết quả research bên ngoài làm bằng chứng cho pain hoặc tỷ lệ cải thiện. | AI hỗ trợ lập danh sách câu hỏi cần kiểm chứng. | Nếu không kiểm nguồn, AI có thể tạo claim về hành vi tài chính hoặc hiệu quả tiết kiệm không đáng tin cậy. | Không đưa claim thị trường hoặc phần trăm tiết kiệm chưa kiểm chứng vào báo cáo. |
| Problem Statement | Nhờ AI chỉ ra metric và boundary còn mơ hồ. | Giúp phân biệt “chi tiêu bốc đồng” với “khó tổng hợp giao dịch”. | AI có thể mô tả problem quá rộng thành một ứng dụng quản lý tài chính toàn diện. | Chọn điểm nghẽn cụ thể: thiếu bối cảnh ngân sách khi phát sinh khoản chi nhỏ. |
| Rule / Workflow / Agent | Dùng AI so sánh ba mức giải pháp. | Giúp nhận ra luồng tuyến tính chưa cần Agent. | AI dễ đề xuất kiến trúc phức tạp, nhiều service và model trước khi chứng minh pain. | Chọn rule-first, chỉ thêm AI fallback khi có dữ liệu cho thấy rule chưa đủ. |
| Decision | Nhờ AI đề xuất pilot, tiêu chí thành công và điều kiện dừng. | Giúp tạo quyết định có thể kiểm chứng thay vì kết luận “nên xây app”. | AI không thể quyết định thay người dùng liệu cảnh báo có gây khó chịu hoặc thay đổi hành vi thật hay không. | Yêu cầu pilot 4 tuần, feedback người dùng và tỷ lệ cảnh báo không hữu ích trước khi mở rộng. |

---

## 3. Reflection câu hỏi mở

### Tôi học được gì khi nghe hoặc so sánh với các problem khác?

Ý tưởng cá nhân của tôi tập trung vào thay đổi hành vi chi tiêu, trong khi candidate nhóm “Số hóa Datasheet & Tự động tạo BOM” tập trung vào một workflow doanh nghiệp có input/output cụ thể. Sự khác biệt này giúp tôi nhận ra một problem dễ thuyết phục hơn khi có actor rõ, một bước nghẽn quan sát được và baseline đo được. Với bài toán chi tiêu, cảm giác “tôi tiêu quá tay” chưa đủ; tôi cần log giao dịch, thời gian tổng hợp và số lần vượt ngân sách để chứng minh pain.

### Tôi hoặc nhóm có lúc nào bị solution-first không?

Có. Ý tưởng ban đầu của tôi nhanh chóng chuyển sang “AI phân tích thói quen” và “AI cảnh báo trước khi chi tiêu”. Khi vẽ lại workflow, tôi nhận ra phần quan trọng hơn là:

1. Dữ liệu giao dịch đến từ đâu?
2. Người dùng thiếu thông tin ở bước nào?
3. Rule cố định đã đủ chưa?
4. Có thể đo thay đổi hành vi bằng metric nào?

Sau đó tôi đưa giải pháp AI về đúng một số bước hỗ trợ thay vì xem AI là toàn bộ sản phẩm.

### Tôi có thay đổi ý kiến sau khi bị challenge không?

Tôi thay đổi từ giả định “ứng dụng có thể cảnh báo ngay trước mọi giao dịch” sang hai mức khả thi hơn:

- MVP dùng CSV/dữ liệu sandbox để phân loại, theo dõi ngân sách và cảnh báo sau giao dịch.
- Chức năng “kiểm tra trước khi mua” do người dùng chủ động nhập số tiền.

Cảnh báo tự động trước giao dịch thật được xếp vào **Not Yet**, vì cần tích hợp chính thức với ngân hàng hoặc ví và phải xử lý quyền riêng tư, độ trễ và độ tin cậy.

### Tôi đóng góp gì thật sự vào artifact?

Đóng góp chắc chắn của tôi là candidate problem về chi tiêu bốc đồng, phần phân tích theo bốn lăng kính, ba Problem Cards liên quan, current/future workflow, boundary và đề xuất pilot rule-first. Đối với artifact nhóm về Datasheet/BOM, tôi cần ghi lại đúng phần mình thực sự tham gia sau buổi thảo luận thay vì suy đoán hoặc để AI viết thay.

### Điều khó nhất khi viết Problem Statement là gì?

Điều khó nhất là định nghĩa “chi tiêu bốc đồng” theo cách đo được và không phán xét. Một khoản cà phê nhỏ có thể không cần thiết với người này nhưng hoàn toàn hợp lý với người khác. Vì vậy hệ thống không nên tự gắn nhãn đạo đức cho giao dịch. Người dùng phải tự đặt ngân sách, xác nhận giao dịch có kế hoạch hay không và có quyền sửa mọi phân loại.

### Nếu làm lại, tôi sẽ thay đổi gì?

Tôi sẽ chưa nói đến AI ngay. Tôi sẽ:

1. Ghi log chi tiêu thật trong 14 ngày.
2. Đo thời gian tổng hợp cuối kỳ và số giao dịch không nhớ được mục đích.
3. Phỏng vấn 3–5 người có hành vi thanh toán tương tự.
4. Thử dashboard và rule cảnh báo theo ngưỡng trước.
5. Chỉ thêm AI nếu mô tả giao dịch mơ hồ hoặc rule tạo quá nhiều cảnh báo không hữu ích.

---

## 4. Mạch hiểu bài cá nhân

~~~text
Problem:
Nhiều khoản chi nhỏ diễn ra nhanh và riêng lẻ.

Workflow:
Nhận nhu cầu/khuyến mãi → thanh toán → nhận thông báo đơn lẻ
→ tiếp tục chi → cuối tháng mới tổng hợp.

Bottleneck:
Thiếu bối cảnh ngân sách tại thời điểm ra quyết định.

Metric:
Số và tổng tiền giao dịch không có kế hoạch, tỷ lệ vượt ngân sách,
thời gian tổng hợp cuối kỳ, độ chính xác phân loại và tỷ lệ cảnh báo hữu ích.

Boundary:
Không tự giao dịch, không lưu OTP/PIN, không phán xét,
không khẳng định dự báo chắc chắn và người dùng luôn quyết định cuối.

Độ phù hợp với AI:
Rule xử lý ngưỡng và merchant quen thuộc.
AI chỉ hỗ trợ phân loại mơ hồ, phát hiện xu hướng và diễn đạt cảnh báo.

Decision:
Go với pilot nhỏ; Not Yet với tích hợp cảnh báo trước giao dịch thật;
không cần Agent ở giai đoạn này.
~~~

## 5. Tự kiểm trước khi nộp

- [x] Có mô tả rõ actor, workflow, bottleneck, impact và boundary.
- [x] Có phân biệt dữ kiện đã quan sát với giả thuyết cần kiểm chứng.
- [x] Có so sánh Rule / Workflow / Agent.
- [x] Có quyết định Go / Not Yet theo từng scope.
- [x] Có nêu AI hữu ích, hời hợt và phần con người sửa lại.
- [ ] Bổ sung baseline từ log chi tiêu thật.
- [ ] Bổ sung kết quả phỏng vấn hoặc survey.
- [ ] Bổ sung đóng góp thực tế của Nguyễn Đại Quân trong artifact nhóm.
- [ ] Tự đọc lại và sửa giọng văn để reflection phản ánh đúng trải nghiệm cá nhân.
