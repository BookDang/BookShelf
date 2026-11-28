# Tiến độ dự án — BookShelf

> **Cập nhật lần cuối:** 28/11/2026  
> **Mô hình phát triển:** Agile (Scrum). Sprint kết thúc khi hoàn thành mọi issue của sprint; mục tiêu mỗi sprint là 3 ngày  
> **Công nghệ:** nginx, Next.js, NestJS, MySQL (bản LTS); triển khai trên VPS tự dựng  
> **Giai đoạn hiện tại:** 2. Phân tích yêu cầu — gần hoàn tất, chờ xác nhận và phê duyệt  
> **Tiếp theo:** Sprint 0 — chuẩn bị nền tảng kỹ thuật

Tài liệu theo dõi dự án đang ở đâu trong vòng đời phát triển phần mềm (SDLC), những việc đã xong, những việc còn lại và lộ trình các sprint.

**Ký hiệu trạng thái:** ✅ Hoàn thành · 🟡 Đang thực hiện · 🟠 Làm một phần · ⬜ Chưa bắt đầu

## 1. Tổng quan theo SDLC

Dự án theo mô hình Agile: sau khi chốt yêu cầu ban đầu, các giai đoạn Thiết kế, Phát triển và Kiểm thử được lặp lại trong từng sprint thay vì làm tuần tự một lần.

| # | Giai đoạn | Trạng thái | Cách thực hiện | Issue |
|---|---|---|---|---|
| 1 | Lập kế hoạch (Planning) | 🟠 Làm một phần | Mục tiêu, phạm vi MVP và phần ngoài phạm vi trong issue #1; lộ trình sprint tại mục 4. Chưa có ước lượng nguồn lực và thời gian cụ thể. | — |
| 2 | **Phân tích yêu cầu (Requirements)** | 🟡 **Đang thực hiện** | Bộ tài liệu yêu cầu ban đầu tại [docs/requirements/](requirements/). Được tinh chỉnh tiếp qua phản hồi sau mỗi sprint. | [#1](https://github.com/BookDang/BookShelf/issues/1) |
| 3 | Thiết kế (Design) | ⬜ Chưa bắt đầu | Phần nền tảng (kiến trúc, công nghệ, khung dữ liệu) ở Sprint 0; thiết kế chi tiết của từng tính năng trong sprint thực hiện tính năng đó. | [#3](https://github.com/BookDang/BookShelf/issues/3) |
| 4 | Phát triển (Implementation) | ⬜ Chưa bắt đầu | Sprint 1 → Sprint 7 (mục 4). | [#4](https://github.com/BookDang/BookShelf/issues/4) → [#10](https://github.com/BookDang/BookShelf/issues/10) |
| 5 | Kiểm thử (Testing) | ⬜ Chưa bắt đầu | Kiểm thử trong từng sprint theo Định nghĩa Hoàn thành (mục 3.2); kiểm thử tải, bảo mật và nghiệm thu MVP ở Sprint 7. | Chưa tạo |
| 6 | Triển khai (Deployment) | ⬜ Chưa bắt đầu | Sau khi nghiệm thu MVP (mục 5). | Chưa tạo |
| 7 | Vận hành, bảo trì (Maintenance) | ⬜ Chưa bắt đầu | Theo dõi, sao lưu, xử lý sự cố. | — |

## 2. Giai đoạn hiện tại: Phân tích yêu cầu

### 2.1. Tài liệu bàn giao

| Tài liệu | Nội dung | Trạng thái |
|---|---|---|
| [user-stories.md](requirements/user-stories.md) | 4 actor, 8 epic, 54 User Stories (41 Must, 10 Should, 3 Could) kèm tiêu chí nghiệm thu; quyết định phạm vi MVP; vấn đề còn mở | Bản nháp, chờ rà soát |
| [functional-requirements.md](requirements/functional-requirements.md) | 88 yêu cầu chức năng có ưu tiên và truy vết; đặc tả đầu vào, đầu ra, kiểm tra dữ liệu, ngoại lệ; phụ thuộc giữa các chức năng | Bản nháp, chờ rà soát |
| [non-functional-requirements.md](requirements/non-functional-requirements.md) | 60 yêu cầu phi chức năng thuộc 11 nhóm, có ưu tiên và cách kiểm chứng; ràng buộc và giả định | Bản nháp, chờ rà soát |
| [business-rules.md](requirements/business-rules.md) | Thuật ngữ, vai trò, trạng thái và chuyển trạng thái; quy tắc nghiệp vụ; chính sách nghiệp vụ cho MVP | Bản nháp, chờ rà soát |

Số liệu trên tính tại thời điểm cập nhật. Các tài liệu đã qua 4 vòng rà soát nội bộ và được kiểm tra tự động để đảm bảo mọi mã tham chiếu tồn tại và truy vết giữa User Story với FR khớp hai chiều.

### 2.2. Tiêu chí nghiệm thu của issue #1

- [x] Xác định đầy đủ các nhóm người dùng trong phạm vi dự án.
- [x] User Stories có mô tả và tiêu chí nghiệm thu rõ ràng.
- [x] Yêu cầu chức năng có thể đối chiếu với User Stories.
- [x] Yêu cầu phi chức năng có tiêu chí đánh giá cụ thể.
- [x] Các yêu cầu được phân loại và xác định mức độ ưu tiên.
- [x] Tài liệu không có yêu cầu mâu thuẫn (các mâu thuẫn phát hiện qua rà soát nội bộ đã được xử lý).
- [ ] Tài liệu được rà soát và thống nhất với các bên liên quan.
- [x] Tài liệu được commit lên GitHub (PR [#2](https://github.com/BookDang/BookShelf/pull/2), merge vào nhánh `develop`).

### 2.3. Vấn đề còn mở cần thư viện xác nhận

Chi tiết tại mục 9 của [user-stories.md](requirements/user-stories.md).

| ID | Nội dung | Cần trước |
|---|---|---|
| OI-01 | Giá trị chính sách MVP: 5 bản, 14 ngày, cách xử lý sách mất và hư hỏng, thời hạn thành viên. | Sprint 4 |
| OI-02 | Quy mô hệ thống dự kiến (đầu sách, bản sách, độc giả, người dùng đồng thời). | Sprint 0 (ảnh hưởng kiến trúc) |
| OI-03 | Mức sẵn sàng 99,5% và RPO 24 giờ. | Sprint 0 (ảnh hưởng kiến trúc) |
| OI-04 | Có cần chuyển dữ liệu sách và độc giả hiện có vào hệ thống không. Nếu có, cần bổ sung yêu cầu nhập dữ liệu hàng loạt vào MVP. | Sprint 2 |
| OI-05 | Nhân viên đồng thời là độc giả phải dùng hai tài khoản với hai email khác nhau. | Sprint 1 |

- [ ] OI-01 · [ ] OI-02 · [ ] OI-03 · [ ] OI-04 · [ ] OI-05

### 2.4. Việc cần làm để kết thúc giai đoạn

1. Thư viện xác nhận các vấn đề OI-01 → OI-05 (ưu tiên những mục cần trước Sprint 0); cập nhật tài liệu theo kết quả.
2. Các bên liên quan rà soát và phê duyệt; đánh dấu bộ tài liệu là **baseline v1.0**. Từ đây mọi thay đổi yêu cầu phải được ghi nhận và phê duyệt.
3. Commit các thay đổi phát sinh sau rà soát và đóng issue #1.

Sprint 0 có thể bắt đầu song song với bước 1 và 2.

## 3. Sprint 0: Chuẩn bị nền tảng

### 3.1. Hạng mục

| Hạng mục | Đầu vào chính | Trạng thái | Issue |
|---|---|---|---|
| Lựa chọn công nghệ | NFR-05, NFR-06; ràng buộc CON-01 → CON-05 | 🟡 Đã chốt nginx, Next.js, NestJS, MySQL; còn chọn ORM và viết ADR | [#3](https://github.com/BookDang/BookShelf/issues/3) |
| Kiến trúc hệ thống | NFR-01 → NFR-04, NFR-09, NFR-11 | ⬜ | [#3](https://github.com/BookDang/BookShelf/issues/3) |
| Khung cơ sở dữ liệu ban đầu | Mục 2 của Business Rules (thuật ngữ, trạng thái); NFR-10 | ⬜ | [#3](https://github.com/BookDang/BookShelf/issues/3) |
| Quy ước API và xử lý lỗi | Mục 4.1 của FR (quy định chung GEN-01 → GEN-10) | ⬜ | [#3](https://github.com/BookDang/BookShelf/issues/3) |
| Khung giao diện và quy ước UI | NFR-07, NFR-08 | ⬜ | [#3](https://github.com/BookDang/BookShelf/issues/3) |
| Repo, CI chạy kiểm thử tự động, migration | NFR-06-03, NFR-06-04 | ⬜ | [#3](https://github.com/BookDang/BookShelf/issues/3) |
| Môi trường phát triển và kiểm thử; dịch vụ email cho môi trường phát triển | NFR-06-05, NFR-06-06; CON-03 | ⬜ | [#3](https://github.com/BookDang/BookShelf/issues/3) |
| Chốt dịch vụ gửi email và tên miền | CON-03; NFR-05-06 | ⬜ Chưa xác định | [#3](https://github.com/BookDang/BookShelf/issues/3) |
| Kế hoạch kiểm thử | Tiêu chí nghiệm thu của User Stories; cột "Cách kiểm chứng" của NFR | ⬜ | [#3](https://github.com/BookDang/BookShelf/issues/3) |
| Backlog trên GitHub: mỗi sprint một issue (nhãn `sprint`) chứa checklist story | [user-stories.md](requirements/user-stories.md) | ✅ | [#3](https://github.com/BookDang/BookShelf/issues/3) → [#10](https://github.com/BookDang/BookShelf/issues/10) |

**Kết quả cuối Sprint 0:** một ứng dụng khung chạy được trên môi trường kiểm thử, CI tự động chạy kiểm thử cho mỗi thay đổi, và backlog Sprint 1 đã sẵn sàng.

### 3.2. Định nghĩa Hoàn thành (Definition of Done)

Một User Story chỉ được coi là hoàn thành khi:

- Đạt toàn bộ tiêu chí nghiệm thu của story.
- Mỗi Business Rule liên quan có ít nhất một kiểm thử tự động (NFR-06-01).
- Quyền truy cập được kiểm tra ở phía máy chủ (NFR-05-07); các thao tác thuộc danh sách NFR-05-08 được ghi nhật ký kiểm toán.
- Mã nguồn đã được review và CI chạy thành công.
- Đã được kiểm tra trên môi trường kiểm thử.
- Tài liệu yêu cầu được cập nhật nếu có thay đổi phát sinh trong quá trình làm.

## 4. Lộ trình sprint

**Độ dài sprint:** nhóm 2 người làm ngoài giờ nên sprint không cố định theo thời gian. Một sprint kết thúc khi mọi issue của sprint đã hoàn thành. Mục tiêu mỗi sprint là 3 ngày; sprint vượt quá 3 ngày cần được nhắc và xem lại phạm vi. Với 8 sprint, tổng thời gian mục tiêu khoảng 24 ngày.

Lộ trình là dự kiến, được điều chỉnh sau mỗi buổi review sprint với thư viện. Thứ tự dựa trên mức ưu tiên và phụ thuộc giữa các chức năng (mục 5 của [functional-requirements.md](requirements/functional-requirements.md)): làm toàn bộ story Must trước để sớm có luồng nghiệp vụ chính chạy được, sau đó mới làm story Should.

### 4.1. Tổng quan

| Sprint | Mục tiêu | Kết quả demo | Thời gian dự kiến | Thời gian thực tế | Trạng thái | Issue |
|---|---|---|---|---|---|---|
| 0 | Nền tảng kỹ thuật (mục 3) | Ứng dụng khung chạy trên môi trường kiểm thử | 28/11 – 30/11/2026 | — | ⬜ | [#3](https://github.com/BookDang/BookShelf/issues/3) |
| 1 | Tài khoản và phân quyền | Quản trị viên được khởi tạo, tạo được tài khoản thủ thư; thủ thư kích hoạt và đăng nhập | 01/12 – 03/12/2026 | — | ⬜ | [#4](https://github.com/BookDang/BookShelf/issues/4) |
| 2 | Danh mục và kho sách | Thủ thư nhập đầu sách, tác giả, thể loại và bản sách vào kho | 04/12 – 06/12/2026 | — | ⬜ | [#5](https://github.com/BookDang/BookShelf/issues/5) |
| 3 | Độc giả | Thủ thư đăng ký độc giả; độc giả kích hoạt tài khoản | 07/12 – 09/12/2026 | — | ⬜ | [#6](https://github.com/BookDang/BookShelf/issues/6) |
| 4 | Mượn và trả sách | **Mốc M1:** luồng mượn trả chạy được từ đầu đến cuối | 10/12 – 12/12/2026 | — | ⬜ | [#7](https://github.com/BookDang/BookShelf/issues/7) |
| 5 | Xử lý ngoại lệ mượn trả và màn hình độc giả | Hủy và chuyển phiếu, sách mất và hư hỏng; độc giả xem sách đang mượn và lịch sử | 13/12 – 15/12/2026 | — | ⬜ | [#8](https://github.com/BookDang/BookShelf/issues/8) |
| 6 | Tra cứu và báo cáo | **Mốc M2:** hoàn thành toàn bộ story Must | 16/12 – 18/12/2026 | — | ⬜ | [#9](https://github.com/BookDang/BookShelf/issues/9) |
| 7 | Story Should và hoàn thiện NFR | **Mốc M3:** bản ứng viên phát hành, nghiệm thu MVP | 19/12 – 21/12/2026 | — | ⬜ | [#10](https://github.com/BookDang/BookShelf/issues/10) |

Thời gian dự kiến tính theo mục tiêu 3 ngày mỗi sprint, bắt đầu từ 28/11/2026. Khi một sprint xong sớm hoặc muộn, cập nhật cột "Thời gian thực tế" và lùi hoặc kéo các mốc phía sau tương ứng.

### 4.2. Story theo sprint

**Sprint 1 — Tài khoản và phân quyền** (8 story Must)

| Story | Tên | Ưu tiên |
|---|---|---|
| US-01-12 | Khởi tạo quản trị viên đầu tiên | Must |
| US-01-11 | Kích hoạt tài khoản | Must |
| US-01-01 | Đăng nhập | Must |
| US-01-02 | Đăng xuất | Must |
| US-01-03 | Đổi mật khẩu | Must |
| US-01-05 | Tạo tài khoản nhân viên | Must |
| US-01-07 | Khóa và mở khóa tài khoản | Must |
| US-01-08 | Phân quyền người dùng | Must |

**Sprint 2 — Danh mục và kho sách** (9 story Must)

| Story | Tên | Ưu tiên |
|---|---|---|
| US-02-05 | Quản lý tác giả | Must |
| US-02-06 | Quản lý thể loại sách | Must |
| US-02-01 | Thêm đầu sách mới | Must |
| US-02-02 | Cập nhật thông tin đầu sách | Must |
| US-02-04 | Xem danh sách và chi tiết đầu sách | Must |
| US-03-01 | Nhập bản sách vật lý | Must |
| US-03-02 | Cập nhật bản sách và vị trí lưu trữ | Must |
| US-03-03 | Theo dõi tình trạng và trạng thái lưu hành của bản sách | Must |
| US-03-04 | Xem số lượng bản sách sẵn có và có thể mượn | Must |

**Sprint 3 — Độc giả** (6 story Must)

| Story | Tên | Ưu tiên |
|---|---|---|
| US-04-01 | Đăng ký độc giả mới | Must |
| US-04-02 | Cập nhật thông tin độc giả | Must |
| US-04-03 | Tìm kiếm và xem thông tin độc giả | Must |
| US-04-04 | Quản lý trạng thái thành viên | Must |
| US-02-03 | Ngừng lưu hành đầu sách | Must |
| US-03-05 | Ghi nhận bản sách bị mất, hư hỏng hoặc thanh lý | Must |

**Sprint 4 — Mượn và trả sách** (7 story Must)

| Story | Tên | Ưu tiên |
|---|---|---|
| US-04-06 | Kiểm tra điều kiện mượn sách của độc giả | Must |
| US-05-01 | Tạo phiếu mượn sách | Must |
| US-05-02 | Từ chối mượn khi không đủ điều kiện | Must |
| US-05-03 | Tự động xác định thời hạn trả sách | Must |
| US-06-01 | Ghi nhận trả sách | Must |
| US-06-02 | Trả từng phần trong một phiếu mượn | Must |
| US-06-03 | Xác định trả sách quá hạn | Must |

Chính sách BP-01 và BP-02 dùng giá trị mặc định trong cấu hình cho đến khi có chức năng cấu hình chính sách (US-01-10, Sprint 7).

**Sprint 5 — Xử lý ngoại lệ mượn trả và màn hình độc giả** (6 Must, 1 Should)

| Story | Tên | Ưu tiên |
|---|---|---|
| US-05-06 | Hủy phiếu mượn lập sai | Must |
| US-05-07 | Chuyển phiếu lập sai độc giả sang đúng độc giả | Must |
| US-06-04 | Ghi nhận sách trả về bị hư hỏng | Must |
| US-06-05 | Ghi nhận sách đang mượn bị mất | Must |
| US-04-05 | Xem lịch sử mượn trả và sách đang mượn của độc giả | Must |
| US-05-05 | Độc giả xem sách đang mượn và thời hạn trả | Must |
| US-04-07 | Độc giả xem hồ sơ và lịch sử mượn trả của bản thân | Should |

**Sprint 6 — Tra cứu và báo cáo** (5 Must, 1 Should)

| Story | Tên | Ưu tiên |
|---|---|---|
| US-07-01 | Tìm kiếm sách | Must |
| US-07-02 | Xem chi tiết và tình trạng có thể mượn | Must |
| US-07-03 | Thủ thư tra cứu toàn bộ danh mục | Should |
| US-08-01 | Thống kê đầu sách và bản sách | Must |
| US-08-02 | Báo cáo mượn trả theo khoảng thời gian | Must |
| US-08-03 | Báo cáo sách quá hạn | Must |

**Sprint 7 — Story Should và hoàn thiện NFR** (8 story Should)

| Story | Tên | Ưu tiên |
|---|---|---|
| US-01-04 | Khôi phục mật khẩu | Should |
| US-01-06 | Cập nhật thông tin tài khoản | Should |
| US-01-09 | Xem và cập nhật thông tin cá nhân | Should |
| US-01-10 | Cấu hình chính sách mượn trả | Should |
| US-02-07 | Quản lý nhà xuất bản | Should |
| US-05-04 | Xem danh sách và chi tiết phiếu mượn | Should |
| US-06-06 | Theo dõi danh sách sách đang mượn quá hạn | Should |
| US-08-04 | Thống kê độc giả | Should |

Hoàn thiện NFR trong Sprint 7:

- [ ] Kiểm thử tải với 200 người dùng đồng thời và dữ liệu ở quy mô dự kiến (NFR-01-05).
- [ ] Quét bảo mật theo OWASP Top 10 (NFR-05-10).
- [ ] Kiểm tra khả năng tiếp cận các màn hình độc giả (NFR-08).
- [ ] Diễn tập khôi phục từ bản sao lưu (NFR-11-04).
- [ ] Nghiệm thu MVP với thư viện: toàn bộ Must và các Should chưa được duyệt hoãn.

**Story Could** — chỉ làm khi còn nguồn lực sau khi xong Must và Should: US-02-08 (ảnh bìa và mô tả), US-03-06 (kiểm kê theo đợt), US-08-05 (sách được mượn nhiều nhất).

### 4.3. Phân bổ

| | Sprint 1 | Sprint 2 | Sprint 3 | Sprint 4 | Sprint 5 | Sprint 6 | Sprint 7 | Chưa xếp | Tổng |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| Must | 8 | 9 | 6 | 7 | 6 | 5 | 0 | 0 | 41 |
| Should | 0 | 0 | 0 | 0 | 1 | 1 | 8 | 0 | 10 |
| Could | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 3 | 3 |

## 5. Triển khai

Các việc bắt buộc trước khi đưa vào sử dụng:

- [ ] Cấu hình dịch vụ gửi email trên môi trường thật (CON-03).
- [ ] Khởi tạo quản trị viên đầu tiên bằng công cụ vận hành (FR-01-14).
- [ ] Không còn lỗ hổng bảo mật mức Cao hoặc Nghiêm trọng (NFR-05-10).
- [ ] Thiết lập sao lưu tự động và hoàn thành diễn tập khôi phục (NFR-11-01, NFR-11-04).
- [ ] Thiết lập theo dõi và cảnh báo (NFR-09-03 → NFR-09-05).
- [ ] Chuyển dữ liệu cũ vào hệ thống, nếu OI-04 xác nhận là cần.

## 6. Cách làm việc

- **Theo dõi sprint:** mỗi sprint có một issue trên GitHub (nhãn `sprint`) chứa checklist story; đánh dấu từng mục khi story đạt Định nghĩa Hoàn thành. Đóng issue khi hết checklist, tức là kết thúc sprint.
- **Lập kế hoạch sprint:** đầu mỗi sprint, chọn story từ lộ trình ở mục 4, kiểm tra phụ thuộc và ước lượng lại.
- **Review sprint:** cuối mỗi sprint, demo cho thư viện; ghi nhận phản hồi và điều chỉnh backlog và tài liệu yêu cầu.
- **Retrospective:** sau review, nhóm rút kinh nghiệm cho sprint sau.
- **Thay đổi yêu cầu:** sau khi có baseline v1.0, mọi thay đổi yêu cầu được ghi vào tài liệu yêu cầu và nhật ký ở mục 8.

## 7. Cách cập nhật tài liệu này

- Khi bắt đầu hoặc kết thúc một sprint: cập nhật cột "Thời gian thực tế" và "Trạng thái" ở mục 4.1, ngày "Cập nhật lần cuối" và "Giai đoạn hiện tại" ở đầu tài liệu.
- Khi chuyển story giữa các sprint: sửa bảng ở mục 4.2 và bảng phân bổ ở mục 4.3.
- Khi tạo issue cho một hạng mục: điền số issue vào cột "Issue".
- Mỗi lần cập nhật: thêm một dòng vào mục 8.

## 8. Nhật ký cập nhật

| Ngày | Nội dung |
|---|---|
| 26/11/2026 | Tạo issue #1, bắt đầu giai đoạn Phân tích yêu cầu. Merge bộ tài liệu yêu cầu vào nhánh `develop` qua PR #2. |
| 28/11/2026 | Hoàn thành bản nháp bộ tài liệu yêu cầu sau 4 vòng rà soát nội bộ; tạo tài liệu theo dõi tiến độ. |
| 28/11/2026 | Chọn mô hình Agile (Scrum); thêm Sprint 0, Định nghĩa Hoàn thành và lộ trình Sprint 1 → Sprint 7. |
| 28/11/2026 | Tạo issue theo dõi cho từng sprint: #3 (Sprint 0) → #10 (Sprint 7). |
| 28/11/2026 | Chốt công nghệ: nginx, Next.js, NestJS, MySQL. Đổi cách tính sprint: kết thúc khi xong mọi issue, mục tiêu 3 ngày mỗi sprint; thêm thời gian dự kiến cho từng sprint. |
