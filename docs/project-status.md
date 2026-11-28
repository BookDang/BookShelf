# Tiến độ dự án — BookShelf

> **Cập nhật lần cuối:** 28/11/2026  
> **Giai đoạn hiện tại:** 2. Phân tích yêu cầu — gần hoàn tất, chờ xác nhận và phê duyệt

Tài liệu theo dõi dự án đang ở giai đoạn nào của vòng đời phát triển phần mềm (SDLC), những việc đã xong, những việc còn lại và việc tiếp theo.

**Ký hiệu trạng thái:** ✅ Hoàn thành · 🟡 Đang thực hiện · 🟠 Làm một phần · ⬜ Chưa bắt đầu

## 1. Tổng quan theo SDLC

| # | Giai đoạn | Trạng thái | Đầu ra chính | Issue |
|---|---|---|---|---|
| 1 | Lập kế hoạch (Planning) | 🟠 Làm một phần | Mục tiêu, phạm vi MVP và phần ngoài phạm vi (trong issue #1). Chưa có kế hoạch tiến độ, nguồn lực, đánh giá khả thi. | — |
| 2 | **Phân tích yêu cầu (Requirements)** | 🟡 **Đang thực hiện** | [docs/requirements/](requirements/) | [#1](https://github.com/BookDang/BookShelf/issues/1) |
| 3 | Thiết kế (Design) | ⬜ Chưa bắt đầu | Kiến trúc, công nghệ, cơ sở dữ liệu, API, UI/UX | Chưa tạo |
| 4 | Phát triển (Implementation) | ⬜ Chưa bắt đầu | Mã nguồn MVP | Chưa tạo |
| 5 | Kiểm thử (Testing) | ⬜ Chưa bắt đầu | Kết quả kiểm thử theo tiêu chí nghiệm thu và NFR | Chưa tạo |
| 6 | Triển khai (Deployment) | ⬜ Chưa bắt đầu | Hệ thống chạy trên môi trường thật | Chưa tạo |
| 7 | Vận hành, bảo trì (Maintenance) | ⬜ Chưa bắt đầu | Theo dõi, sao lưu, xử lý sự cố | — |

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

- [ ] **OI-01** — Giá trị chính sách MVP: 5 bản, 14 ngày, cách xử lý sách mất và hư hỏng, thời hạn thành viên.
- [ ] **OI-02** — Quy mô hệ thống dự kiến (đầu sách, bản sách, độc giả, người dùng đồng thời).
- [ ] **OI-03** — Mức sẵn sàng 99,5% và RPO 24 giờ.
- [ ] **OI-04** — Có cần chuyển dữ liệu sách và độc giả hiện có vào hệ thống không. Nếu có, cần bổ sung yêu cầu nhập dữ liệu hàng loạt vào MVP.
- [ ] **OI-05** — Nhân viên đồng thời là độc giả phải dùng hai tài khoản với hai email khác nhau.

### 2.4. Việc cần làm để kết thúc giai đoạn

1. Thư viện xác nhận các vấn đề OI-01 → OI-05; cập nhật tài liệu theo kết quả.
2. Các bên liên quan rà soát và phê duyệt; đánh dấu bộ tài liệu là **baseline v1.0**. Từ đây mọi thay đổi yêu cầu phải được ghi nhận và phê duyệt.
3. Commit các thay đổi phát sinh sau rà soát và đóng issue #1.

## 3. Giai đoạn tiếp theo: Thiết kế

Đề xuất tạo các issue sau. Cột "Đầu vào" chỉ ra phần tài liệu yêu cầu cần dùng.

| Hạng mục | Đầu vào chính | Issue |
|---|---|---|
| Kiến trúc hệ thống | NFR-01 → NFR-04, NFR-09, NFR-11; ràng buộc CON-01 → CON-05 | Chưa tạo |
| Lựa chọn công nghệ | Kiến trúc hệ thống; NFR-05, NFR-06 | Chưa tạo |
| Thiết kế cơ sở dữ liệu | Mục 2 của Business Rules (thuật ngữ, trạng thái); NFR-10 | Chưa tạo |
| Thiết kế API | Mục 4 của FR (đầu vào, đầu ra, ngoại lệ); NFR-04, NFR-05 | Chưa tạo |
| Thiết kế UI/UX | Tiêu chí nghiệm thu của User Stories; NFR-07, NFR-08 | Chưa tạo |
| Kế hoạch kiểm thử | Tiêu chí nghiệm thu của User Stories; cột "Cách kiểm chứng" của NFR | Chưa tạo |

## 4. Các giai đoạn sau

**Phát triển** — làm theo thứ tự đề xuất ở mục 5 của [functional-requirements.md](requirements/functional-requirements.md):

1. Xác thực, phân quyền, khởi tạo quản trị viên đầu tiên (FR-01).
2. Danh mục và kho sách (FR-02, FR-03).
3. Độc giả và tài khoản độc giả (FR-04, FR-01-11).
4. Cấu hình chính sách (FR-09).
5. Mượn và trả sách (FR-05, FR-06).
6. Tra cứu (FR-07).
7. Báo cáo (FR-08).

**Kiểm thử** — điều kiện nghiệm thu MVP: đạt toàn bộ yêu cầu Must và các yêu cầu Should chưa được duyệt hoãn (mục 6 của FR).

**Triển khai** — các việc bắt buộc trước khi đưa vào sử dụng:

- [ ] Cấu hình dịch vụ gửi email (CON-03).
- [ ] Khởi tạo quản trị viên đầu tiên bằng công cụ vận hành (FR-01-14).
- [ ] Quét bảo mật, không còn lỗ hổng mức Cao hoặc Nghiêm trọng (NFR-05-10).
- [ ] Thiết lập sao lưu tự động và diễn tập khôi phục (NFR-11-01, NFR-11-04).
- [ ] Thiết lập theo dõi và cảnh báo (NFR-09-03 → NFR-09-05).

## 5. Cách cập nhật tài liệu này

- Khi chuyển sang giai đoạn mới hoặc hoàn thành một hạng mục: cập nhật trạng thái ở mục 1, ngày "Cập nhật lần cuối" và "Giai đoạn hiện tại" ở đầu tài liệu.
- Khi tạo issue cho một hạng mục: điền số issue vào cột "Issue".
- Mỗi lần cập nhật: thêm một dòng vào mục 6.

## 6. Nhật ký cập nhật

| Ngày | Nội dung |
|---|---|
| 26/11/2026 | Tạo issue #1, bắt đầu giai đoạn Phân tích yêu cầu. Merge bộ tài liệu yêu cầu vào nhánh `develop` qua PR #2. |
| 28/11/2026 | Hoàn thành bản nháp bộ tài liệu yêu cầu sau 4 vòng rà soát nội bộ; tạo tài liệu theo dõi tiến độ. |
