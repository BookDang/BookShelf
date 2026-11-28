# Quy trình làm việc với Git — BookShelf

Tài liệu quy định cách tạo nhánh, commit và Pull Request (PR) cho dự án. Mọi thành viên làm theo quy trình này cho mọi thay đổi, kể cả thay đổi tài liệu.

## 1. Luồng làm việc

```
Issue → Nhánh từ develop → Commit → Push → PR vào develop → Review → Rebase and merge → Xóa nhánh
```

1. Mỗi việc đều bắt đầu từ một issue.
2. Tạo nhánh cho issue từ `develop` mới nhất.
3. Commit từng thay đổi riêng biệt.
4. Mở PR vào `develop`; thành viên còn lại review.
5. Merge sau khi được approve và CI xanh; xóa nhánh.

## 2. Các nhánh

| Nhánh | Vai trò | Tạo từ | Merge vào | Triển khai tới |
|---|---|---|---|---|
| `main` | Mã nguồn đang chạy thật | — | — | Môi trường thật |
| `develop` | Nhánh tích hợp, chứa mọi việc đã hoàn thành | `main` | `main` khi phát hành | Môi trường kiểm thử |
| `<loại>/<số-issue>-<mô-tả>` | Làm một issue | `develop` | `develop` | — |
| `hotfix/<số-issue>-<mô-tả>` | Sửa lỗi gấp trên môi trường thật | `main` | `main` và `develop` | Môi trường thật |

Không commit trực tiếp lên `main` hoặc `develop`. Mọi thay đổi đi qua PR.

## 3. Đặt tên nhánh

**Định dạng:** `<loại>/<số-issue>-<mô-tả-ngắn>[-r<n>]`

| Loại | Dùng khi | Ví dụ |
|---|---|---|
| `feat` | Thêm tính năng (User Story) | `feat/30-login` |
| `fix` | Sửa lỗi | `fix/45-overdue-days` |
| `docs` | Chỉ thay đổi tài liệu | `docs/11-adr-tech-stack` |
| `chore` | Cấu hình, công cụ, thư viện phụ thuộc | `chore/16-monorepo-ci` |
| `refactor` | Sửa cấu trúc mã, không đổi hành vi | `refactor/52-loan-service` |
| `test` | Chỉ thêm hoặc sửa kiểm thử | `test/60-loan-concurrency` |
| `hotfix` | Sửa lỗi gấp trên môi trường thật | `hotfix/70-login-error` |

**Quy tắc:**

- Chữ thường, các từ nối bằng dấu gạch ngang, không dấu tiếng Việt, tối đa khoảng 50 ký tự.
- Bắt buộc có số issue.
- **Hậu tố `-r<n>` dành cho issue bị mở lại** (mục 8). Lần làm đầu tiên không có hậu tố; mỗi lần issue bị mở lại và cần làm tiếp thì tăng số: `fix/45-overdue-days-r2`, `fix/45-overdue-days-r3`.
- Không dùng lại tên của một nhánh đã merge hoặc đã xóa.

## 4. Tạo và cập nhật nhánh

1. Có issue trước, rồi mới tạo nhánh. Mỗi nhánh chỉ làm một issue.
2. Tạo nhánh từ `develop` mới nhất:

   ```bash
   git switch develop
   git pull
   git switch -c docs/11-adr-tech-stack
   ```

   Hoặc dùng GitHub CLI để tạo nhánh và liên kết luôn với issue:

   ```bash
   gh issue develop 11 --base develop --name docs/11-adr-tech-stack --checkout
   ```

3. Khi bắt đầu làm: gán mình vào issue và chuyển thẻ trên [GitHub Project](https://github.com/users/BookDang/projects/4) sang `In Progress`.
4. Giữ nhánh ngắn: mục tiêu tối đa 1–2 ngày. Issue lớn hơn thì tách nhỏ.
5. Khi `develop` có thay đổi mới, cập nhật nhánh bằng `git rebase develop` (nhánh chỉ một người làm). Nếu nhánh có người khác cùng làm thì dùng `git merge develop`.

## 5. Commit

### 5.1. Định dạng

Theo chuẩn [Conventional Commits](https://www.conventionalcommits.org/), **viết bằng tiếng Anh**:

```
<loại>(<phạm vi>): <mô tả>

<thân: giải thích vì sao thay đổi — không bắt buộc>

Refs #<số-issue>
```

| Thành phần | Quy định |
|---|---|
| Loại | `feat`, `fix`, `docs`, `chore`, `refactor`, `test`, `ci`, `perf`, `style`, `build` |
| Phạm vi | Nghiệp vụ: `auth`, `catalog`, `inventory`, `members`, `loans`, `returns`, `search`, `reports`. Hạ tầng: `web`, `api`, `db`, `infra`. Tài liệu: `requirements`, `architecture`, `contributing`. Có thể bỏ trống khi thay đổi không thuộc phạm vi cụ thể. |
| Mô tả | Câu mệnh lệnh, bắt đầu bằng chữ thường, không có dấu chấm cuối, tối đa 72 ký tự |
| Thân | Giải thích vì sao thay đổi, không lặp lại thay đổi gì; mỗi dòng tối đa 72 ký tự |
| Chân | `Refs #<số-issue>` để liên kết với issue. Thay đổi phá vỡ tương thích ghi thêm `BREAKING CHANGE: <mô tả>` |

**Ví dụ:**

```
feat(loans): reject loans for members with overdue items

A member with any overdue loan item must not borrow more books
(BR-05-06). The check runs again at confirmation time to cover
items that became overdue while the slip was being prepared.

Refs #30
```

### 5.2. Nguyên tắc

- **Mỗi commit là một thay đổi riêng biệt và trọn vẹn.** Tách các phần độc lập thành các commit khác nhau. Ví dụ: thêm migration, thêm service, thêm màn hình là ba commit, không gộp làm một.
- Mỗi commit phải build được và kiểm thử phải chạy qua, vì mọi commit được giữ nguyên khi merge (mục 6).
- Trước khi xin review, dọn các commit tạm (`wip`, `fix typo`, …) bằng `git rebase -i develop`.
- **Không thêm chữ ký hoặc dòng đồng tác giả của công cụ AI** (ví dụ `Co-Authored-By` của trợ lý AI, dòng "Generated with …") vào commit, PR hay issue.
- Không commit thông tin bí mật: tệp `.env`, mật khẩu, khóa API, chứng chỉ (NFR-05-12).
- Không commit tệp sinh tự động hoặc thư mục build (`node_modules`, `dist`, `.next`, …).

## 6. Pull Request

| Quy định | Nội dung |
|---|---|
| Đích | `develop`. Riêng `hotfix/*` mở PR vào `main`. |
| Tiêu đề | Theo định dạng commit, bằng tiếng Anh. Ví dụ: `docs(architecture): add ADR-0001 tech stack` |
| Nội dung | `Closes #<số-issue>` để issue tự đóng khi merge; tóm tắt thay đổi; cách kiểm tra; checklist [Định nghĩa Hoàn thành](docs/project-status.md#32-định-nghĩa-hoàn-thành-definition-of-done) |
| Review | **Mọi PR đều phải được thành viên còn lại review và approve**, kể cả PR chỉ thay đổi tài liệu. Người mở PR không tự approve. |
| Điều kiện merge | Có approve; CI xanh; không còn trao đổi chưa giải quyết; nhánh đã cập nhật theo `develop` |
| Cách merge vào `develop` | **Rebase and merge** — giữ nguyên từng commit riêng biệt, lịch sử thẳng |
| Sau khi merge | Xóa nhánh; kiểm tra issue đã tự đóng và thẻ trên Project đã sang `Done` |

**Người review kiểm tra:**

- Thay đổi đáp ứng tiêu chí nghiệm thu của issue hoặc User Story.
- Có kiểm thử cho các Business Rule liên quan.
- Commit đúng định dạng, mỗi commit là một thay đổi riêng biệt.
- Không có thông tin bí mật, không có chữ ký AI.

## 7. Phát hành và hotfix

**Phát hành:**

1. Mở PR từ `develop` vào `main`, tiêu đề `release: vX.Y.Z`.
2. Merge bằng **Create a merge commit**.
3. Gắn tag phiên bản trên `main` theo [Semantic Versioning](https://semver.org/): `v0.1.0`, `v0.2.0`, … Trước khi nghiệm thu MVP dùng `0.y.z`; bản nghiệm thu MVP là `v1.0.0`.

**Hotfix:**

1. Tạo issue cho lỗi, gắn nhãn `bug`.
2. Tạo nhánh `hotfix/<số-issue>-<mô-tả>` từ `main`.
3. Mở PR vào `main`, review và merge như PR thường; gắn tag tăng số patch (ví dụ `v1.0.1`).
4. Merge `main` vào `develop` để `develop` có bản sửa.

## 8. Xử lý bug bị mở lại

**Mở lại issue cũ hay tạo issue mới:**

- **Mở lại** khi bản sửa trước chưa giải quyết đúng lỗi đã mô tả trong issue.
- **Tạo issue mới** khi là lỗi khác, hoặc lỗi cũ xuất hiện lại sau một thay đổi khác về sau (regression). Liên kết tới issue cũ trong phần mô tả.

**Khi issue bị mở lại:**

1. Ghi bình luận vào issue: lỗi còn ở đâu, cách tái hiện, và liên kết tới PR trước.
2. Tạo nhánh mới từ `develop` mới nhất, thêm hậu tố lần làm: lần đầu là `fix/45-overdue-days`, lần mở lại thứ nhất là `fix/45-overdue-days-r2`, lần tiếp theo là `fix/45-overdue-days-r3`. Nếu bản sửa trước đã lên môi trường thật thì dùng `hotfix/45-overdue-days-r2` tạo từ `main`.
3. Không khôi phục hay dùng lại nhánh cũ.
4. PR mới ghi `Closes #45` và liên kết tới PR trước (ví dụ `Follow-up to #50`).
5. Bổ sung kiểm thử tái hiện đúng trường hợp đã làm bản sửa trước thất bại.

## 9. Bảo vệ nhánh trên GitHub

Áp dụng cho `main` và `develop`:

- Bắt buộc merge qua PR, có ít nhất 1 approve.
- Bắt buộc CI xanh (bật sau khi hoàn thành issue #16).
- Bắt buộc giải quyết hết trao đổi trước khi merge.
- Cấm force push và cấm xóa nhánh.

## 10. Ví dụ đầy đủ

```bash
# 1. Tạo nhánh cho issue #11
git switch develop && git pull
git switch -c docs/11-adr-tech-stack

# 2. Commit từng phần riêng biệt
git add docs/architecture/adr/README.md
git commit -m "docs(architecture): add ADR template and index" -m "Refs #11"
git add docs/architecture/adr/0001-tech-stack.md
git commit -m "docs(architecture): add ADR-0001 tech stack" -m "Refs #11"

# 3. Push và mở PR
git push -u origin docs/11-adr-tech-stack
gh pr create --base develop --title "docs(architecture): add ADR-0001 tech stack" --body "Closes #11"

# 4. Thành viên còn lại review, approve → Rebase and merge → xóa nhánh
```
