# Quy trình làm việc với Git — BookShelf

Tài liệu quy định cách chia issue, tạo nhánh, commit và Pull Request (PR) cho dự án. Mọi thành viên làm theo quy trình này cho mọi thay đổi, kể cả thay đổi tài liệu.

## 1. Luồng làm việc

### 1.1. Các cấp issue

| Cấp | Vai trò | Ví dụ | Có nhánh riêng |
|---|---|---|---|
| Issue sprint (nhãn `sprint`) | Theo dõi phạm vi một sprint; không chứa mã | #3 — Sprint 0 | Không |
| **Issue công việc** | Một User Story, công việc kỹ thuật hoặc lỗi; là đơn vị được merge vào `develop` | #30 — Đăng nhập | **Nhánh chính** |
| Sub-issue | Một phần nhỏ của issue công việc, làm xong trong khoảng 1 ngày | #31 — API đăng nhập | Nhánh sub-issue |

Issue công việc lớn được chia thành các sub-issue nhỏ gọn để dễ quản lý và chia việc. Issue công việc nhỏ có thể không có sub-issue.

### 1.2. Luồng chuẩn

```
develop
  └─ feat/30-login                    ← nhánh chính của issue #30
       ├─ feat/30-31-login-api        ← sub-issue #31: commit riêng biệt → PR vào feat/30-login
       └─ feat/30-32-login-page       ← sub-issue #32: commit riêng biệt → PR vào feat/30-login
  ← feat/30-login được Squash and merge vào develop thành 1 commit duy nhất
```

1. Chia issue công việc thành các sub-issue.
2. Tạo **nhánh chính** của issue từ `develop` (từ `main` nếu là hotfix).
3. Mỗi sub-issue: tạo nhánh từ nhánh chính, commit từng thay đổi riêng biệt, mở PR vào nhánh chính, kiểm tra, merge, xóa nhánh sub-issue, **đóng tay sub-issue**.
4. Khi mọi sub-issue đã merge vào nhánh chính: mở PR từ nhánh chính vào `develop` (hoặc `main` nếu là hotfix), kiểm tra (nên nhờ thành viên còn lại review), **Squash and merge thành 1 commit duy nhất**, xóa nhánh chính, **đóng tay issue công việc**.

### 1.3. Issue không có sub-issue

Tạo nhánh chính từ `develop`, commit trên chính nhánh đó, mở PR vào `develop` và cũng **Squash and merge thành 1 commit**, sau đó đóng tay issue.

**Kết quả:** trên `develop` và `main`, mỗi issue công việc là đúng một commit. Các commit chi tiết vẫn được xem lại được trong PR của từng sub-issue.

## 2. Các nhánh

| Nhánh | Vai trò | Tạo từ | Merge vào | Cách merge |
|---|---|---|---|---|
| `main` | Mã nguồn đang chạy thật | — | — | — |
| `develop` | Nhánh tích hợp, chứa mọi issue đã hoàn thành; triển khai tới môi trường kiểm thử | `main` | `main` khi phát hành | Create a merge commit |
| Nhánh chính của issue | Gom toàn bộ mã của một issue công việc | `develop` (hotfix: `main`) | `develop` (hotfix: `main`) | **Squash and merge** |
| Nhánh sub-issue | Làm một sub-issue | Nhánh chính của issue | Nhánh chính của issue | Rebase and merge |

Không commit trực tiếp lên `main`, `develop` hay nhánh chính của issue đang có sub-issue. Mọi thay đổi đi qua PR.

## 3. Đặt tên nhánh

**Định dạng:**

| Nhánh | Định dạng | Ví dụ |
|---|---|---|
| Nhánh chính của issue | `<loại>/<số-issue>-<mô-tả>[-r<n>]` | `feat/30-login` |
| Nhánh sub-issue | `<loại>/<số-issue-cha>-<số-sub-issue>-<mô-tả>[-r<n>]` | `feat/30-31-login-api` |

**Loại:**

| Loại | Dùng khi | Ví dụ |
|---|---|---|
| `feat` | Thêm tính năng (User Story) | `feat/30-login` |
| `fix` | Sửa lỗi | `fix/45-overdue-days` |
| `docs` | Chỉ thay đổi tài liệu | `docs/11-adr-tech-stack` |
| `chore` | Cấu hình, công cụ, thư viện phụ thuộc | `chore/16-monorepo-ci` |
| `refactor` | Sửa cấu trúc mã, không đổi hành vi | `refactor/52-loan-service` |
| `test` | Chỉ thêm hoặc sửa kiểm thử | `test/60-loan-concurrency` |
| `hotfix` | Sửa lỗi gấp trên môi trường thật | `hotfix/70-login-error` |

Nhánh sub-issue dùng cùng loại với nhánh chính.

**Quy tắc:**

- Chữ thường, các từ nối bằng dấu gạch ngang, không dấu tiếng Việt, tối đa khoảng 50 ký tự.
- Bắt buộc có số issue. Nhánh sub-issue bắt đầu bằng số issue cha để các nhánh cùng issue đứng cạnh nhau.
- Không đặt nhánh sub-issue dạng `feat/30-login/31-api`: Git không cho phép vừa có nhánh `feat/30-login` vừa có nhánh nằm "bên trong" nó.
- **Hậu tố `-r<n>` dành cho issue bị mở lại** (mục 8). Lần làm đầu tiên không có hậu tố; mỗi lần issue bị mở lại và cần làm tiếp thì tăng số: `-r2`, `-r3`.
- Không dùng lại tên của một nhánh đã merge hoặc đã xóa.

## 4. Tạo và cập nhật nhánh

**Tạo nhánh chính của issue #30:**

```bash
git switch develop && git pull
git switch -c feat/30-login
git push -u origin feat/30-login
```

**Tạo nhánh cho sub-issue #31 từ nhánh chính:**

```bash
git switch feat/30-login && git pull
git switch -c feat/30-31-login-api
```

Có thể dùng GitHub CLI để tạo nhánh và liên kết luôn với issue:

```bash
gh issue develop 31 --base feat/30-login --name feat/30-31-login-api --checkout
```

**Quy tắc:**

1. Có issue trước, rồi mới tạo nhánh. Mỗi nhánh chỉ làm một issue hoặc một sub-issue.
2. Khi bắt đầu làm: gán mình vào issue và chuyển thẻ trên [GitHub Project](https://github.com/users/BookDang/projects/4) sang `In Progress`.
3. Giữ nhánh sub-issue ngắn: mục tiêu tối đa 1 ngày. Sub-issue lớn hơn thì tách tiếp.
4. **Cập nhật nhánh chính** khi `develop` có thay đổi mới: `git merge develop`. Không rebase nhánh chính vì nhiều nhánh sub-issue tạo từ nó và có thể cả hai thành viên cùng dùng.
5. **Cập nhật nhánh sub-issue** khi nhánh chính có thay đổi mới: `git rebase feat/30-login` (nhánh sub-issue chỉ một người làm).

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
| Chân | `Refs #<số-sub-issue>` trên nhánh sub-issue. Thay đổi phá vỡ tương thích ghi thêm `BREAKING CHANGE: <mô tả>` |

### 5.2. Commit trên nhánh sub-issue

- **Mỗi commit là một thay đổi riêng biệt và trọn vẹn.** Ví dụ: thêm migration, thêm service, thêm màn hình là ba commit, không gộp làm một.
- Mỗi commit nên build được và kiểm thử chạy qua.
- Trước khi xin review, dọn các commit tạm (`wip`, `fix typo`, …) bằng `git rebase -i`.

### 5.3. Commit duy nhất khi merge vào `develop` hoặc `main`

Khi Squash and merge nhánh chính, người merge sửa message của commit gộp theo mẫu:

```
feat(auth): add staff login and logout

Staff sign in with email and password; sessions expire after 30
minutes of inactivity and are revoked on logout.

- API endpoints for login and logout (#31)
- Login page with field-level errors (#32)
- Lockout after 5 failed attempts (#33)

Closes #30
Closes #31
Closes #32
Closes #33
```

- Tiêu đề: tiêu đề của PR nhánh chính, theo định dạng commit.
- Thân: tóm tắt vì sao thay đổi và danh sách sub-issue. Xóa danh sách commit mà GitHub tự điền.
- Chân: `Closes #` cho issue công việc và từng sub-issue. Các dòng này để truy vết; issue vẫn được đóng tay theo mục 6.

### 5.4. Nguyên tắc chung

- **Không thêm chữ ký hoặc dòng đồng tác giả của công cụ AI** (ví dụ `Co-Authored-By` của trợ lý AI, dòng "Generated with …") vào commit, PR hay issue.
- Không commit thông tin bí mật: tệp `.env`, mật khẩu, khóa API, chứng chỉ (NFR-05-12).
- Không commit tệp sinh tự động hoặc thư mục build (`node_modules`, `dist`, `.next`, …).

## 6. Pull Request

**Mọi thay đổi đều đi qua PR, nhưng approve không bắt buộc:** người mở PR được tự merge khi đã đạt các điều kiện merge bên dưới. Nên nhờ thành viên còn lại review với PR nhánh chính của issue và các thay đổi có rủi ro (mượn trả, phân quyền, cơ sở dữ liệu).

| | PR sub-issue | PR nhánh chính |
|---|---|---|
| Từ → vào | Nhánh sub-issue → nhánh chính | Nhánh chính → `develop` (hotfix: `main`) |
| Tiêu đề | Định dạng commit, tiếng Anh | Định dạng commit, tiếng Anh; dùng làm tiêu đề commit gộp |
| Nội dung | `Part of #<issue-cha>`, `Resolves #<sub-issue>`; tóm tắt; cách kiểm tra | `Closes #` cho issue công việc và mọi sub-issue; tóm tắt; checklist [Định nghĩa Hoàn thành](docs/project-status.md#32-định-nghĩa-hoàn-thành-definition-of-done) |
| Review tập trung vào | Chi tiết mã, kiểm thử, từng commit | Tổng thể: tiêu chí nghiệm thu của issue đạt đủ, các phần ghép với nhau đúng, CI xanh |
| Cách merge | Rebase and merge | **Squash and merge** — 1 commit, message theo mục 5.3 |
| Sau khi merge | Xóa nhánh sub-issue; **đóng tay sub-issue** | Xóa nhánh chính; **đóng tay issue công việc** (và sub-issue nào còn mở); kiểm tra thẻ trên Project đã sang `Done` |

**Điều kiện merge:** CI xanh; không còn trao đổi chưa giải quyết; nhánh đã cập nhật theo nhánh đích; người merge đã tự kiểm tra theo danh sách "Người review (hoặc người tự merge) kiểm tra" bên dưới.

**Đóng issue bằng tay:** nhánh mặc định của repo là `main`, mà GitHub chỉ tự đóng issue theo từ khóa `Closes` khi thay đổi vào nhánh mặc định. Vì vậy **người merge PR chịu trách nhiệm đóng tay issue** ngay sau khi merge:

- Merge PR sub-issue → đóng sub-issue đó.
- Merge PR nhánh chính vào `develop` → đóng issue công việc.
- Khi đóng, ghi bình luận liên kết tới PR đã merge, ví dụ `Done in #50`.
- PR hotfix merge vào `main` tự đóng issue theo `Closes`; kiểm tra lại sau khi merge.

**Người review (hoặc người tự merge) kiểm tra:**

- Thay đổi đáp ứng tiêu chí nghiệm thu của issue hoặc User Story.
- Có kiểm thử cho các Business Rule liên quan.
- Commit và tiêu đề PR đúng định dạng.
- Không có thông tin bí mật, không có chữ ký AI.

## 7. Phát hành và hotfix

**Phát hành:**

1. Mở PR từ `develop` vào `main`, tiêu đề `release: vX.Y.Z`.
2. Merge bằng **Create a merge commit**.
3. Gắn tag phiên bản trên `main` theo [Semantic Versioning](https://semver.org/): `v0.1.0`, `v0.2.0`, … Trước khi nghiệm thu MVP dùng `0.y.z`; bản nghiệm thu MVP là `v1.0.0`.

**Hotfix:**

1. Tạo issue cho lỗi, gắn nhãn `bug`; chia sub-issue nếu cần.
2. Tạo nhánh chính `hotfix/<số-issue>-<mô-tả>` từ `main`; các nhánh sub-issue `hotfix/<số-issue-cha>-<số-sub-issue>-<mô-tả>` tạo từ nhánh chính.
3. Merge các sub-issue vào nhánh chính như luồng chuẩn.
4. Mở PR nhánh chính vào `main`, kiểm tra, **Squash and merge** thành 1 commit; gắn tag tăng số patch (ví dụ `v1.0.1`).
5. Merge `main` vào `develop` để `develop` có bản sửa.

## 8. Xử lý bug bị mở lại

**Mở lại issue cũ hay tạo issue mới:**

- **Mở lại** khi bản sửa trước chưa giải quyết đúng lỗi đã mô tả trong issue.
- **Tạo issue mới** khi là lỗi khác, hoặc lỗi cũ xuất hiện lại sau một thay đổi khác về sau (regression). Liên kết tới issue cũ trong phần mô tả.

**Khi issue hoặc sub-issue bị mở lại:**

1. Ghi bình luận vào issue: lỗi còn ở đâu, cách tái hiện, và liên kết tới PR trước.
2. Tạo nhánh mới với hậu tố lần làm, không khôi phục hay dùng lại nhánh cũ:

   | Tình huống | Nhánh mới | Tạo từ | PR vào |
   |---|---|---|---|
   | Sub-issue bị mở lại, nhánh chính **chưa** merge | `feat/30-31-login-api-r2` | Nhánh chính | Nhánh chính |
   | Issue hoặc sub-issue bị mở lại, nhánh chính **đã** merge vào `develop` | `fix/30-login-r2` | `develop` | `develop` |
   | Bản sửa trước đã lên môi trường thật và cần sửa gấp | `hotfix/30-login-r2` | `main` | `main` |

3. PR mới ghi `Closes #<số-issue>` và liên kết tới PR trước (ví dụ `Follow-up to #50`).
4. Bổ sung kiểm thử tái hiện đúng trường hợp đã làm bản sửa trước thất bại.

## 9. Bảo vệ nhánh trên GitHub

Áp dụng cho `main` và `develop`:

- Bắt buộc merge qua PR; không bắt buộc approve.
- Bắt buộc CI xanh (bật sau khi hoàn thành issue #16).
- Bắt buộc giải quyết hết trao đổi trước khi merge.
- Cấm force push và cấm xóa nhánh.
- Quy định áp dụng cả với quản trị viên repo: không ai push thẳng lên `main` hoặc `develop`.

**Cài đặt merge của repo:**

- Bật cả ba cách merge (Squash, Rebase, Merge commit) vì GitHub không giới hạn cách merge theo từng nhánh. Người merge chọn đúng cách theo bảng ở mục 2.
- Squash merge: tiêu đề mặc định là tiêu đề PR, phần thân để trống để người merge điền theo mục 5.3.
- Merge commit (PR phát hành): tiêu đề mặc định là tiêu đề PR.

## 10. Ví dụ đầy đủ

Issue #30 "Đăng nhập" có hai sub-issue: #31 (API) và #32 (giao diện).

```bash
# 1. Nhánh chính của issue #30
git switch develop && git pull
git switch -c feat/30-login && git push -u origin feat/30-login

# 2. Sub-issue #31: nhánh con, commit riêng biệt, PR vào nhánh chính
git switch -c feat/30-31-login-api
git commit -m "feat(auth): add session table migration" -m "Refs #31"
git commit -m "feat(auth): add login and logout endpoints" -m "Refs #31"
git push -u origin feat/30-31-login-api
gh pr create --base feat/30-login --title "feat(auth): add login and logout endpoints" --body "Part of #30. Resolves #31."
# → kiểm tra → Rebase and merge → xóa nhánh
gh issue close 31 --comment "Done in #<số-PR>"

# 3. Sub-issue #32: làm tương tự với nhánh feat/30-32-login-page

# 4. Khi #31 và #32 đã merge: PR nhánh chính vào develop
gh pr create --base develop --head feat/30-login --title "feat(auth): add staff login and logout" \
  --body "Closes #30, closes #31, closes #32"
# → kiểm tra (nên nhờ review) → Squash and merge (sửa message theo mục 5.3) → xóa nhánh chính
gh issue close 30 --comment "Done in #<số-PR>"
```
