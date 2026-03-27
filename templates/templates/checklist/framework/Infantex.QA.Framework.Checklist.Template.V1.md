# Infantex.QA.Framework.Checklist.Template.V1

**Người tạo report:** NgocTran, Nguyễn Ngọc Duy, Hà

## 1. Mục tiêu

Báo cáo này dùng để đề xuất và chuẩn hóa **format Checklist Ver1**.

Bài toán cần giải quyết:

- xây dựng một format checklist **ngắn, rõ, dễ scan, dễ rà nhanh**
- giúp tester và intern **nhìn vào là hiểu cần xác nhận gì**
- giữ đúng bản chất của checklist: **xác nhận nhanh độ phủ và trạng thái cơ bản**
- tránh biến checklist thành testcase dài hoặc tài liệu nặng
- hỗ trợ rà nhanh theo area, platform, test round hoặc release scope
- tạo nền phù hợp để **phục vụ automation và trace coverage về sau** khi cần

Phạm vi của báo cáo này:
- chỉ tập trung vào **format Checklist**
- không thay thế cho TCS ở các case có nhiều bước, nhiều nhánh, hoặc cần logic chi tiết

---

## 2. Tiêu chí lựa chọn

Format Checklist được đề xuất cần đáp ứng các tiêu chí sau:

- **Đúng bản chất**: 1 dòng là 1 hạng mục kiểm tra có thể xác nhận được
- **Ngắn gọn**: ưu tiên câu ngắn, dễ scan, không viết thành step-by-step dài
- **Dễ hiểu tối đa**: intern cũng có thể dùng để rà nhanh
- **Có cấu trúc**: dễ lọc theo area, platform, priority, status
- **Tuần tự trong vận hành**: nhìn vào là biết đang cần check gì, trong điều kiện nào, mong đợi gì
- **Mở rộng được**: thêm item, area, platform mà không phá format
- **Tinh gọn và thông minh**: đủ để phục vụ smoke, sanity, quick verification, platform sweep

Checklist này được lựa chọn dựa trên các tiêu chí sau:

- phù hợp với việc kiểm tra nhanh, breadth-first
- thuận tiện cho smoke, sanity, release readiness, quick feature verification
- nhẹ hơn TCS nhưng vẫn đủ để theo dõi và tổng hợp kết quả
- có thể dùng song song với TCS theo đúng vai trò của từng loại tài liệu

---

## 3. Đề xuất format Checklist

### 3.1. Bản chất sử dụng

Checklist được dùng khi cần:

- rà nhanh luồng chính
- xác nhận nhanh trạng thái feature
- kiểm tra nhanh theo release scope
- sweep theo platform hoặc area
- tổng hợp tình trạng pass/fail/block ở mức hạng mục

Checklist **không phù hợp** khi một item cần:
- nhiều bước dài
- nhiều nhánh
- nhiều điều kiện logic
- dữ liệu test chi tiết
- expected phức tạp

Trong các trường hợp đó, item nên được chuyển thành **TCS**.

### 3.2. Bảng format chuẩn Ver1

| Check ID | Area | Check Item | Condition/Setup | Expected Outcome | Priority | Platform | Test Round | Execution Status | Actual Result | Note |
|---|---|---|---|---|---|---|---|---|---|---|

### 3.3. Ý nghĩa từng cột

| Cột | Mục đích sử dụng |
|---|---|
| Check ID | Mã checklist item duy nhất |
| Area | Khu vực hoặc nhóm chức năng chính |
| Check Item | Hạng mục cần xác nhận |
| Condition/Setup | Điều kiện hoặc setup ngắn trước khi check |
| Expected Outcome | Kết quả mong đợi ở mức ngắn gọn |
| Priority | Mức ưu tiên rà |
| Platform | Nền tảng áp dụng |
| Test Round | Mục đích hoặc vòng rà: Smoke / Sanity / Regression / Release |
| Execution Status | Trạng thái thực hiện |
| Actual Result | Chỉ ghi khi cần nêu sai khác chính, lý do block, hoặc Jira ID/link |
| Note | Ghi chú ngắn nếu cần |

### 3.4. Bộ giá trị chuẩn dùng trong Ver1

| Trường | Giá trị chuẩn |
|---|---|
| Priority | Critical / High / Medium / Low |
| Platform | Cross-platform / Android / iOS / Web / Steam / Backend / Other |
| Test Round | Smoke / Sanity / Regression / Release |
| Execution Status | Not Run / Pass / Fail / Blocked |
| Actual Result rule | Pass = để trống / Fail = 1 câu ngắn mô tả sai khác chính hoặc Jira ID/link / Blocked = Blocked due to ... / Not Run = để trống |

### 3.5. Cách vận hành của format này

Format này được sử dụng theo logic sau:

- **Area** xác định khu vực đang rà
- **Check Item** xác định hạng mục cần xác nhận
- **Condition/Setup** xác định điều kiện cần có trước khi check
- **Expected Outcome** xác định điều kiện đạt
- **Platform / Test Round** giúp nhóm phạm vi kiểm tra
- **Execution Status / Actual Result** ghi nhận kết quả thực tế

Người chạy checklist theo dõi lần lượt theo trình tự:
**Area -> Check Item -> Condition/Setup -> Expected Outcome -> Platform/Test Round -> Execution**

### 3.6. Quy tắc viết checklist đúng bản chất

| Quy tắc | Hướng áp dụng |
|---|---|
| 1 dòng = 1 check item | Không gộp nhiều ý vào 1 dòng |
| Dùng câu xác nhận ngắn | Viết để rà nhanh, không viết như testcase |
| Không mô tả nhiều bước dài | Nếu dài hoặc nhiều nhánh, chuyển sang TCS |
| Expected ngắn và đo được | Chỉ giữ mức cần thiết để xác nhận pass/fail |
| Actual Result chỉ ghi khi cần | Pass để trống; Fail/Blocked ghi ngắn |

#### Mẫu viết Check Item
- Login với tài khoản hợp lệ
- Mở shop và kiểm tra offer hiển thị
- Join bàn khi đủ buy-in
- Mở event page và kiểm tra banner/timer/reward

#### Mẫu viết Expected Outcome
- User vào lobby thành công
- Offer hiển thị đầy đủ và giá đúng
- User join bàn thành công
- Event page hiển thị đúng banner, timer và reward

### 3.7. Bộ mẫu checklist ngắn

| Check ID | Area | Check Item | Condition/Setup | Expected Outcome | Priority | Platform | Test Round | Execution Status | Actual Result | Note |
|---|---|---|---|---|---|---|---|---|---|---|
| CHK-ACCOUNT-001 | Account | Login với tài khoản hợp lệ | Active account; stable network; latest build installed | User vào lobby thành công, không crash | Critical | Cross-platform | Smoke | Pass |  | Core login |
| CHK-ECONOMY-001 | Economy | Mở shop và kiểm tra offer hiển thị | Shop enabled; internet on | Offer hiển thị đúng và có giá | High | Android | Sanity | Fail | Offers not loaded - JIRA-245 | Quick verification |
| CHK-GAMEPLAY-001 | Gameplay | Join bàn khi đủ buy-in | User đủ buy-in; server available | User join bàn thành công | Critical | Web | Release | Blocked | Blocked due to server unavailable | Core flow |

---

## 4. Giá trị sử dụng và phạm vi áp dụng

### 4.1. Giá trị sử dụng

Format này phù hợp với các nhu cầu sau:

- rà nhanh luồng chính hoặc nhóm feature
- xác nhận nhanh trạng thái release readiness
- sweep theo area hoặc platform
- tạo danh sách coverage ngắn, dễ review, dễ theo dõi
- hỗ trợ intern hoặc tester mới tham gia rà nhanh theo scope rõ ràng
- làm lớp tài liệu nhẹ trước hoặc song song với TCS

### 4.2. Phạm vi áp dụng phù hợp

Format này phù hợp trong các trường hợp:

- smoke
- sanity
- release checklist
- quick verification
- platform sweep
- breadth-first validation

### 4.3. Trường hợp cần chuyển sang TCS

Checklist item nên được chuyển thành TCS khi:

- cần nhiều bước chi tiết để chạy
- có nhiều nhánh logic
- cần dữ liệu test rõ ràng hơn
- expected không thể mô tả ngắn trong một dòng
- cần trace chặt theo scenario riêng biệt

### 4.4. Quan hệ với TCS

- **Checklist** dùng để rà nhanh, breadth-first, xác nhận coverage và trạng thái cơ bản
- **TCS** dùng để kiểm tra chi tiết, có cấu trúc sâu hơn, phù hợp với flow dài hoặc logic rõ ràng
- Hai format nên dùng song song đúng vai trò, không thay thế hoàn toàn cho nhau
