# Infantex.QA.Framework.TCS.Template.V1

## 1. Mục tiêu

Báo cáo này dùng để đề xuất và chuẩn hóa **format Test Case (TCS) Ver1**.

Bài toán cần giải quyết:

- xây dựng một format TCS **dễ đọc, dễ sử dụng, dễ review**
- giúp tester và intern **nhìn vào là hiểu cách chạy**
- giữ nội dung **đúng, đủ, rõ ràng, ngắn gọn, có cấu trúc**
- giảm tình trạng testcase dài, khó theo dõi, khó bảo trì
- giữ khả năng **mở rộng** khi số lượng case tăng hoặc phạm vi test thay đổi

Phạm vi của báo cáo này:
- chỉ tập trung vào **format TCS**
- không bao gồm quy trình phân tích spec hay quy trình sinh danh sách TCS

---

## 2. Tiêu chí lựa chọn

Format TCS được đề xuất cần đáp ứng các tiêu chí sau:

- **Đúng**: phản ánh đúng mục tiêu kiểm tra của testcase
- **Đủ**: có đủ thông tin để người chạy test thực hiện được
- **Không thừa, không thiếu**: tránh dài dòng nhưng không mơ hồ
- **Dễ hiểu tối đa**: intern cũng có thể đọc và chạy
- **Ngắn gọn**: mỗi case trình bày gọn, không gây quá tải khi theo dõi
- **Có cấu trúc**: các cột ổn định, dễ theo dõi và dễ quản lý
- **Tuần tự**: steps đi theo đúng thứ tự thao tác thực tế
- **Mở rộng được**: bổ sung thêm case, module, flow mà không phá vỡ format
- **Tinh gọn và thông minh**: hỗ trợ tốt cho việc đọc, review, quản lý và tái sử dụng

Format này được lựa chọn dựa trên các tiêu chí sau:

- ưu tiên khả năng sử dụng thực tế trong công việc hằng ngày
- ưu tiên ngôn ngữ rõ ràng, dễ tiếp cận với nhiều nhóm người dùng
- phù hợp cho tester, intern, lead và các bên liên quan cùng theo dõi
- đủ chuẩn để áp dụng thống nhất trong Ver1 mà không tạo thêm độ phức tạp không cần thiết

---

## 3. Đề xuất format TCS

### 3.1. Format được chọn

Format được chọn là **business-readable TCS format**.

Đặc điểm:
- dùng ngôn ngữ dễ hiểu
- steps ngắn, tuần tự
- expected rõ, đo được
- không hiển thị mã step kỹ thuật ở mặt trước
- nhìn vào bảng là hiểu case đang kiểm tra gì và cách thực hiện như thế nào

### 3.2. Bảng format chuẩn Ver1

| TC ID | Module | Feature | Scenario | Preconditions | Test Data | Test Steps | Expected Result | Priority | Test Type | Automation Potential | Execution Status | Actual Result | Bug Link | Note |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|

### 3.3. Ý nghĩa từng cột

| Cột | Mục đích sử dụng |
|---|---|
| TC ID | Mã testcase duy nhất |
| Module | Nhóm chức năng lớn |
| Feature | Chức năng cụ thể |
| Scenario | Nội dung kiểm tra chính của case |
| Preconditions | Điều kiện cần trước khi chạy |
| Test Data | Dữ liệu đầu vào tác động trực tiếp tới case |
| Test Steps | Các bước thực hiện ngắn, rõ, tuần tự |
| Expected Result | Kết quả mong đợi rõ, đo được |
| Priority | Mức ưu tiên chạy test |
| Test Type | Loại test để lọc và nhóm |
| Automation Potential | Mức độ phù hợp để đưa vào automation |
| Execution Status | Trạng thái chạy test |
| Actual Result | Kết quả thực tế |
| Bug Link | Link bug nếu fail |
| Note | Ghi chú ngắn nếu cần |

### 3.4. Bộ giá trị chuẩn dùng trong Ver1

| Trường | Giá trị chuẩn |
|---|---|
| Priority | Critical / High / Medium / Low |
| Automation Potential | High / Medium / Low / No |
| Execution Status | Not Run / Pass / Fail / Blocked |
| Test Type | Smoke / Regression / Positive / Negative / Boundary / Validation / Integration / Config |

### 3.5. Cách vận hành của format này

Format này được sử dụng theo logic sau:

- **Scenario** xác định nội dung cần kiểm tra
- **Preconditions** xác định trạng thái cần có trước khi thực hiện
- **Test Data** xác định dữ liệu cần sử dụng
- **Test Steps** xác định trình tự thao tác
- **Expected Result** xác định kết quả được xem là đạt
- **Execution Status / Actual Result / Bug Link** ghi nhận kết quả thực tế sau khi chạy

Người chạy test theo dõi lần lượt theo trình tự:
**Scenario -> Preconditions -> Test Data -> Test Steps -> Expected Result -> Execution**

### 3.6. Bộ mẫu cách viết để intern cũng có thể sử dụng

#### Mẫu viết Scenario
- Cho phép login với tài khoản hợp lệ
- Không cho lưu khi Name trống
- Không cho join bàn khi không đủ buy-in

#### Mẫu viết Test Steps
1. Login bằng tài khoản hợp lệ  
2. Mở màn hình Profile  
3. Nhập Name theo dữ liệu test  
4. Bấm Save  
5. Kiểm tra kết quả  

#### Mẫu viết Expected Result
- User vào Home thành công
- Không lưu dữ liệu, hiển thị lỗi “Name is required”
- Nút Confirm bị disable

### 3.7. Bộ mẫu testcase ngắn

| TC ID | Module | Feature | Scenario | Preconditions | Test Data | Test Steps | Expected Result | Priority | Test Type | Automation Potential | Execution Status | Actual Result | Bug Link | Note |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| LOGIN_01 | Authentication | Login | Cho phép login với tài khoản hợp lệ | App đang ở màn Login | username=valid_user; password=valid_pass | 1. Nhập username hợp lệ  2. Nhập password hợp lệ  3. Bấm Login  4. Kiểm tra kết quả | User vào Home thành công | Critical | Smoke | High | Not Run |  |  | Core flow |
| PROF_02 | Profile | Update Name | Không cho lưu khi Name trống | User đã login | Name="" | 1. Mở màn hình Profile  2. Xóa toàn bộ Name  3. Bấm Save  4. Kiểm tra kết quả | Không lưu dữ liệu, hiển thị lỗi “Name is required” | High | Validation | Medium | Not Run |  |  | Required field |

---

## 4. Giá trị sử dụng và phạm vi áp dụng

### 4.1. Giá trị sử dụng

Format này phù hợp với các nhu cầu sau:

- trình bày testcase theo cách ngắn gọn, rõ ràng và dễ theo dõi
- hỗ trợ nhiều đối tượng cùng sử dụng, bao gồm tester, intern, lead và các bên liên quan
- giảm độ dài và độ rối của testcase so với cách viết truyền thống
- hỗ trợ review, lọc, nhóm và quản lý testcase thuận tiện hơn
- tạo nền tảng ổn định để chuẩn hóa tài liệu test trong giai đoạn đầu

### 4.2. Phạm vi áp dụng phù hợp

Format này phù hợp trong các trường hợp:

- feature nhỏ và vừa
- tài liệu cần thống nhất nhanh để áp dụng rộng
- nhóm người dùng có nhiều mức kinh nghiệm khác nhau
- môi trường làm việc cần ưu tiên tính rõ ràng và khả năng sử dụng thực tế
- trường hợp cần một format chung để vừa thiết kế case vừa ghi nhận execution cơ bản

### 4.3. Trường hợp cần cân nhắc mở rộng thêm

Format này có thể cần mở rộng thêm khi:

- flow có nhiều nhánh lớn hoặc điều kiện phức tạp
- cần trace chặt với requirement/spec
- cần quản lý execution riêng theo nhiều vòng chạy, nhiều build hoặc nhiều tester
- cần quản lý dataset hoặc step mapping ở mức chi tiết hơn

Các thành phần có thể bổ sung ở các phiên bản sau:
- Spec Ref
- Test Pack
- Dataset Ref
- reusable step mapping
- flow group / module group
- execution tách riêng theo từng run
