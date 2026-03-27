# Infantex.QA.Framework.Poker.TestConfig.Approach.V1

## 1. Mục tiêu

Tài liệu này dùng để giúp hiểu và test **hệ thống config của Poker** trước khi bóc tách thành **final test cases**.

Mục tiêu của giai đoạn này:

- hiểu hệ thống config đang phục vụ điều gì
- biết nên chia hệ thống thành những phần nào để test
- biết nên đi theo thứ tự nào
- biết sau bước này sẽ tạo ra những loại test cases nào

> Đây **không phải** file test case chi tiết.  
> Đây là **file nền** để chuẩn bị bóc tách test case sau.

---

## 2. Hệ thống config này cần đảm bảo điều gì

Hệ thống config Poker cần đảm bảo 7 mục tiêu chính:

1. **Định nghĩa đúng game**  
   Tạo đúng mode, variant, sub-variant, format, table size, player number.

2. **Hiển thị đúng game**  
   Game tạo xong phải hiển thị đúng ở lobby, list, filter, metadata.

3. **Kiểm soát đúng quyền tham gia**  
   Chỉ đúng người, đúng điều kiện, đúng thiết bị mới được join hoặc observe.

4. **Kiểm soát đúng economy đầu vào**  
   Buy-in, rebuy, add-on, stack boundary, fee, no rathole phải đúng.

5. **Áp đúng luật chơi trong bàn**  
   Blind, ante, timer, cap, run-it-multi-times, straddle phải đúng.

6. **Áp đúng tournament flow**  
   Start time, registration, payout, bounty, GTD, schedule, breaks, multi-day phải đúng.

7. **Quản lý đúng vòng đời game**  
   Save, edit, reload, auto restart, auto create, cancel, disband phải đúng.

---

## 3. Rule nền khi đọc config

| Nội dung | Loại | Cách hiểu |
|---|---|---|
| Mode không có config | Rule | Không hiển thị config |
| Mode có config con phụ thuộc cha | Rule | Config con vẫn hiển thị |
| Parent = off | Rule | Config con bị disable |
| Parent = on | Rule | Config con hoạt động theo spec |
| Mode có config độc lập | Rule | Config hoạt động theo spec |
| Hidden | UI State | Không có config ở mode đó |
| Disabled | UI State | Có config nhưng đang bị khóa do dependency |
| Enabled | UI State | Có config và thao tác được |

---

## 4. 7 Area chính của hệ thống test config

| Area | Module | Config/Cụm config chính | Test Focus | Test Order |
|---|---|---|---|---|
| **A1. Game Definition** | Game Type Setup / Format Structure / Table Structure | Mode, Variant, Sub-Variant, Mixed Formats, Format Choice, Format Change In, Table Size, Player Number | Khóa đúng loại game được tạo | Round 1 |
| **A2. Publish & Discovery** | Table Identity / Display Flags / Lobby Discoverability | Table Name, Short Description, Private Game, Anonymous Table, Featured, Label as NEW, Filter/List visibility | Khóa đúng cách game được publish và hiển thị | Round 3 |
| **A3. Access Control** | Join Permission / Device-Network Restriction / Observer Control | VIP Only, Buy-in Authorization, Restrict Device, Restrict Observers + sub, GPS/IP/Emulator Restriction, Authorized to Register | Khóa đúng người được join / observe | Round 1 |
| **A4. Economy Entry** | Buy-in Setup / Rebuy-Add-on / Stack Boundary / Fee Logic | Buy-in, Custom Buy-in, Rebuy/Re-entry, Add-on, Starting Chips, Min Holding, Min Cash Out, No Rathole, Fee, FeeCap | Khóa đúng chip/fee/entry economy | Round 1 |
| **A5. Core Gameplay Rules** | Blind & Bet Structure / Timer / Pot-Bet Limitation / Special Hand Rules | Blinds, Betting Size, Blind Structure, Action Time, Calltime, Cap, Ante, Big Blind Ante, Run It Multi-Times, Straddle | Khóa đúng luật chơi trong bàn | Round 1 |
| **A6. Tournament Control** | Registration Window / Tournament Economy / Progression / Multi-day | Start Time, Late Reg, Early Bird, Bubble Protection, Payout, Bounty Cluster, GTD, Blinds Up, Schedule, Restart Every, Sync Breaks, Multi-Day | Khóa đúng tournament flow | Round 2 |
| **A7. Lifecycle & Automation** | Save-Edit-Reload / Automation / End-of-Life | Auto Start, Auto Extension + sub, Auto Restart + sub, Auto Create Table, Game Length, Save Start Time, Disband, Cancel Tournament | Khóa đúng save/edit/restart/clone/cancel | Round 2 |

---

## 5. Cách hiểu nhanh từng Area

| Area | Hiểu nhanh |
|---|---|
| **A1. Game Definition** | Game này là game gì |
| **A2. Publish & Discovery** | Game này hiện ra ngoài lobby như thế nào |
| **A3. Access Control** | Ai được vào, ai không được vào |
| **A4. Economy Entry** | Vào game bằng chip/fee như thế nào |
| **A5. Core Gameplay Rules** | Khi vào bàn rồi thì luật chơi chạy ra sao |
| **A6. Tournament Control** | Nếu là giải đấu thì giải chạy như thế nào |
| **A7. Lifecycle & Automation** | Game được lưu, sửa, lặp lại, hủy như thế nào |

---

## 6. Thứ tự làm việc

| Round | Phạm vi | Mục tiêu |
|---|---|---|
| **Round 1** | A1 + A3 + A4 + A5 | Khóa luồng sống còn của game |
| **Round 2** | A6 + A7 | Khóa tournament flow và lifecycle |
| **Round 3** | A2 | Rà phần publish, display, discoverability |

---

## 7. Loại test asset sẽ tạo sau bước này

| Loại | Dùng để làm gì | Ví dụ |
|---|---|---|
| **Flow TCS** | Test các luồng bắt buộc phải sống | Create game, Join game, Buy-in, Tournament start |
| **Rule TCS** | Test rule riêng của config/cụm config | Visibility, Dependency, Default, Validation, Boundary, Persistence |
| **Consistency Checklist** | Rà tính đồng bộ | Hidden/Disabled/Enabled, component behavior, message, wording |

---

## 8. Cách bóc test case sau bước này

| Bước | Làm gì |
|---|---|
| **B1** | Map từng config vào đúng Area và Module |
| **B2** | Xác định config nào là độc lập, config nào là parent-child, config nào là cluster |
| **B3** | Với từng Module, xác định luồng bắt buộc phải test |
| **B4** | Tạo Flow TCS skeleton |
| **B5** | Tạo Rule TCS skeleton |
| **B6** | Tạo Consistency Checklist skeleton |
| **B7** | Sau đó mới viết final test cases theo `Infantex.QA.Framework.TCS.Template.V1.2` |

---
