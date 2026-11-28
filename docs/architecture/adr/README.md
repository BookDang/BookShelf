# Quyết định kiến trúc (ADR)

ADR (Architecture Decision Record) ghi lại một quyết định kỹ thuật quan trọng: bối cảnh, quyết định, lý do và hệ quả. Mục đích là để cả nhóm và người mới hiểu vì sao hệ thống được xây dựng như hiện tại.

## Danh sách

| Số | Tiêu đề | Trạng thái | Ngày | Issue |
|---|---|---|---|---|
| [0001](0001-tech-stack.md) | Bộ công nghệ cho MVP | Đã chấp nhận | 28/11/2026 | #11 |

## Khi nào cần viết ADR

- Chọn hoặc thay đổi công nghệ, thư viện chính, dịch vụ bên ngoài.
- Quyết định ảnh hưởng tới cấu trúc hệ thống, dữ liệu, bảo mật hoặc cách triển khai.
- Quyết định khó đảo ngược hoặc tốn nhiều công sức để thay đổi về sau.

## Quy ước

- Tên tệp: `NNNN-<mô-tả-ngắn>.md`, đánh số tăng dần, không dùng lại số.
- Mỗi ADR đi qua PR như mọi thay đổi khác (xem [CONTRIBUTING.md](../../../CONTRIBUTING.md)).
- ADR đã chấp nhận không sửa nội dung quyết định. Khi quyết định thay đổi, viết ADR mới và chuyển ADR cũ sang trạng thái "Bị thay thế bởi ADR-NNNN".
- Cập nhật bảng danh sách ở trên khi thêm hoặc đổi trạng thái ADR.

**Trạng thái:** Đề xuất · Đã chấp nhận · Bị thay thế bởi ADR-NNNN · Không còn áp dụng

## Mẫu

```markdown
# ADR-NNNN: <Tiêu đề>

- **Trạng thái:** Đề xuất
- **Ngày:** dd/mm/yyyy
- **Issue:** #<số>

## Bối cảnh

Vấn đề cần quyết định, các ràng buộc và yêu cầu liên quan (dẫn chiếu FR, NFR, BR).

## Quyết định

Nội dung quyết định, cụ thể và kiểm chứng được.

## Lý do

Vì sao chọn phương án này.

## Hệ quả

Tích cực, tiêu cực, rủi ro và cách giảm thiểu.

## Phương án đã cân nhắc

Các phương án khác và lý do không chọn.
```
