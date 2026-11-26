# Functional Requirements — BookShelf

## 1. Tổng quan

Tài liệu mô tả các yêu cầu chức năng của hệ thống BookShelf, nhằm đáp ứng các nghiệp vụ quản lý thư viện, quản lý sách, độc giả và hoạt động mượn trả sách.

Tài liệu liên quan:

- [user-stories.md](user-stories.md) — actor, epic và User Stories.
- [business-rules.md](business-rules.md) — thuật ngữ, trạng thái, quy tắc và chính sách nghiệp vụ.
- [non-functional-requirements.md](non-functional-requirements.md) — yêu cầu phi chức năng.

## 2. Quy ước

**Mã định danh:** `FR-<nhóm>-<số thứ tự>`. Mỗi nhóm FR tương ứng với một epic cùng số (FR-01 ↔ EP-01…), riêng FR-09 thuộc EP-01.

**Mức độ ưu tiên (MoSCoW):** dùng chung định nghĩa với User Stories.

| Mức | Ý nghĩa | Thuộc bản phát hành MVP |
|---|---|---|
| Must | Bắt buộc; thiếu thì không vận hành được nghiệp vụ cốt lõi | Có |
| Should | Nên có; chỉ hoãn khi thiếu nguồn lực và được Product Owner phê duyệt (mục 6) | Có, trừ khi đã được duyệt hoãn |
| Could | Có thì tốt; chỉ làm khi đã xong toàn bộ Must và Should | Không bắt buộc |

**Truy vết:** cột *User Story* và *Business Rule* liệt kê các mục liên quan. Một FR được coi là hoàn thành khi các tiêu chí nghiệm thu của User Story liên quan đều đạt.

## 3. Danh sách yêu cầu chức năng

### FR-01 — Quản lý tài khoản và phân quyền

| ID | Yêu cầu chức năng | Ưu tiên | User Story | Business Rule |
|---|---|---|---|---|
| FR-01-01 | Hệ thống cho phép người dùng đăng nhập bằng email và mật khẩu. | Must | US-01-01 | BR-01-04 |
| FR-01-02 | Hệ thống cho phép người dùng đăng xuất. | Must | US-01-02 | — |
| FR-01-03 | Hệ thống cho phép người dùng thay đổi mật khẩu. | Must | US-01-03 | — |
| FR-01-04 | Hệ thống cho phép người dùng khôi phục mật khẩu qua email. | Should | US-01-04 | — |
| FR-01-05 | Hệ thống cho phép quản trị viên tạo tài khoản nhân viên (thủ thư, quản trị viên). | Must | US-01-05 | BR-01-01, BR-01-02, BR-01-05, BR-01-08 |
| FR-01-06 | Hệ thống cho phép quản trị viên cập nhật thông tin tài khoản nhân viên. | Should | US-01-06 | BR-01-02 |
| FR-01-07 | Hệ thống cho phép quản trị viên khóa và mở khóa tài khoản. | Must | US-01-07 | BR-01-04, BR-01-06, BR-01-12 |
| FR-01-08 | Hệ thống cho phép quản trị viên thay đổi vai trò của tài khoản nhân viên. | Must | US-01-08 | BR-01-05, BR-01-08, BR-01-09, BR-01-12 |
| FR-01-09 | Hệ thống kiểm tra quyền truy cập ở mọi yêu cầu theo vai trò của người dùng. | Must | US-01-08 | BR-01-03 |
| FR-01-10 | Hệ thống cho phép người dùng xem và cập nhật thông tin cá nhân được phép chỉnh sửa. | Should | US-01-09, US-04-07 | BR-04-10 |
| FR-01-11 | Hệ thống cho phép thủ thư tạo tài khoản độc giả liên kết với một hồ sơ độc giả có email. | Must | US-04-01, US-04-02 | BR-01-09, BR-01-10 |
| FR-01-12 | Hệ thống gửi liên kết kích hoạt và cho phép người dùng kích hoạt tài khoản bằng cách tự đặt mật khẩu. | Must | US-01-05, US-01-11, US-01-12, US-04-01 | BR-01-11 |
| FR-01-13 | Hệ thống cho phép gửi lại liên kết kích hoạt cho tài khoản chưa kích hoạt. | Should | US-01-11 | BR-01-11 |
| FR-01-14 | Hệ thống cung cấp công cụ vận hành để khởi tạo tài khoản quản trị viên đầu tiên, hoặc cấp lại liên kết kích hoạt cho tài khoản đó, khi hệ thống chưa có quản trị viên ở trạng thái Hoạt động. | Must | US-01-12 | BR-01-11, BR-01-13 |
| FR-01-15 | Hệ thống vô hiệu mọi liên kết kích hoạt và khôi phục mật khẩu chưa sử dụng khi email của tài khoản thay đổi. | Must | US-01-06, US-04-02 | BR-01-14 |

### FR-02 — Quản lý danh mục sách

| ID | Yêu cầu chức năng | Ưu tiên | User Story | Business Rule |
|---|---|---|---|---|
| FR-02-01 | Hệ thống cho phép thêm đầu sách mới. | Must | US-02-01 | BR-02-01, BR-02-02, BR-02-03, BR-02-04, BR-02-05 |
| FR-02-02 | Hệ thống cho phép cập nhật thông tin đầu sách. | Must | US-02-02 | BR-02-02 |
| FR-02-03 | Hệ thống cho phép ngừng lưu hành đầu sách. | Must | US-02-03 | BR-02-08, BR-08-07 |
| FR-02-04 | Hệ thống cho phép xem danh sách đầu sách, lọc theo trạng thái lưu hành. | Must | US-02-04 | — |
| FR-02-05 | Hệ thống cho phép xem thông tin chi tiết đầu sách, gồm tổng số bản sách, số bản sẵn có và số bản có thể mượn. | Must | US-02-04 | BR-03-07, BR-03-11 |
| FR-02-06 | Hệ thống cho phép quản lý thông tin tác giả. | Must | US-02-05 | BR-02-03, BR-02-09 |
| FR-02-07 | Hệ thống cho phép quản lý thể loại sách. | Must | US-02-06 | BR-02-04, BR-02-09, BR-02-10 |
| FR-02-08 | Hệ thống cho phép quản lý nhà xuất bản. | Should | US-02-07 | BR-02-09 |
| FR-02-09 | Hệ thống kiểm tra định dạng và tính duy nhất của ISBN. | Must | US-02-01, US-02-02 | BR-02-06, BR-02-12, BR-02-13 |
| FR-02-10 | Hệ thống cho phép quản lý ảnh bìa và mô tả sách. | Could | US-02-08 | — |
| FR-02-11 | Hệ thống cho phép khôi phục đầu sách ngừng lưu hành về trạng thái đang lưu hành. | Should | US-02-03 | BR-02-11 |
| FR-02-12 | Hệ thống cho phép xóa đầu sách chưa có bản sách và giao dịch nào. | Should | US-02-03 | BR-02-07 |

### FR-03 — Quản lý kho sách

| ID | Yêu cầu chức năng | Ưu tiên | User Story | Business Rule |
|---|---|---|---|---|
| FR-03-01 | Hệ thống cho phép nhập thêm bản sách vật lý cho một đầu sách. | Must | US-03-01 | BR-03-01, BR-03-02, BR-03-04 |
| FR-03-02 | Hệ thống định danh duy nhất từng bản sách vật lý (sinh mã tự động hoặc nhận mã nhập tay). | Must | US-03-01 | BR-03-03 |
| FR-03-03 | Hệ thống cho phép cập nhật thông tin bản sách. | Must | US-03-02 | BR-03-02 |
| FR-03-04 | Hệ thống cho phép quản lý vị trí lưu trữ sách. | Must | US-03-02 | BR-03-04 |
| FR-03-05 | Hệ thống cho phép ghi chú tình trạng vật lý của bản sách. | Should | US-03-03 | — |
| FR-03-06 | Hệ thống theo dõi trạng thái lưu hành và lịch sử thay đổi trạng thái của từng bản sách. | Must | US-03-03 | BR-03-12, BR-03-15 |
| FR-03-07 | Hệ thống hiển thị tổng số lượng bản sách của từng đầu sách. | Must | US-03-04 | BR-03-07 |
| FR-03-08 | Hệ thống hiển thị số bản sách sẵn có và số bản sách có thể mượn của từng đầu sách. | Must | US-03-04 | BR-03-07, BR-03-08, BR-03-11 |
| FR-03-09 | Hệ thống hỗ trợ kiểm kê kho sách theo đợt. | Could | US-03-06 | — |
| FR-03-10 | Hệ thống cho phép ghi nhận bản sách tại kho bị mất, hư hỏng hoặc thanh lý. | Must | US-03-05 | BR-03-06, BR-03-09, BR-03-10, BR-03-13 |
| FR-03-11 | Hệ thống cho phép đưa bản sách hư hỏng đã sửa hoặc bản sách mất đã tìm thấy về trạng thái Sẵn có. | Should | US-03-05, US-06-05 | BR-03-14 |
| FR-03-12 | Hệ thống cho phép xem danh sách bản sách, lọc theo đầu sách, vị trí và trạng thái. | Should | US-03-03 | — |

### FR-04 — Quản lý độc giả

| ID | Yêu cầu chức năng | Ưu tiên | User Story | Business Rule |
|---|---|---|---|---|
| FR-04-01 | Hệ thống cho phép thủ thư đăng ký hồ sơ độc giả mới. | Must | US-04-01 | BR-04-01, BR-04-11 |
| FR-04-02 | Hệ thống cho phép thủ thư cập nhật thông tin độc giả. | Must | US-04-02 | BR-04-09, BR-04-11, BR-01-10 |
| FR-04-03 | Hệ thống cho phép xem danh sách độc giả. | Must | US-04-03 | — |
| FR-04-04 | Hệ thống cho phép xem thông tin chi tiết độc giả. | Must | US-04-03 | — |
| FR-04-05 | Hệ thống cho phép tìm kiếm độc giả theo mã thành viên, họ tên, email, số điện thoại. | Must | US-04-03 | — |
| FR-04-06 | Hệ thống cho phép thủ thư thay đổi trạng thái thành viên kèm lý do. | Must | US-04-04 | BR-04-02, BR-04-03, BR-04-04, BR-04-06, BR-04-08 |
| FR-04-07 | Hệ thống tự cấp mã thành viên duy nhất khi tạo hồ sơ độc giả. | Must | US-04-01 | BR-04-01, BR-04-09 |
| FR-04-08 | Hệ thống cho phép xem lịch sử mượn trả của độc giả. | Must | US-04-05, US-04-07 | BR-04-07, BR-05-17, BR-05-19 |
| FR-04-09 | Hệ thống cho phép xem danh sách sách độc giả đang mượn. | Must | US-04-05 | — |
| FR-04-10 | Hệ thống cho phép kiểm tra điều kiện mượn sách của độc giả. | Must | US-04-06 | BR-04-02, BR-05-05, BR-05-06 |

### FR-05 — Quản lý mượn sách

| ID | Yêu cầu chức năng | Ưu tiên | User Story | Business Rule |
|---|---|---|---|---|
| FR-05-01 | Hệ thống cho phép thủ thư tạo phiếu mượn sách. | Must | US-05-01 | BR-05-01, BR-05-02, BR-05-03, BR-05-11 |
| FR-05-02 | Hệ thống kiểm tra trạng thái thành viên trước khi cho mượn sách. | Must | US-05-02 | BR-04-02, BR-04-03 |
| FR-05-03 | Hệ thống kiểm tra bản sách đủ điều kiện cho mượn. | Must | US-05-02 | BR-05-04, BR-03-11 |
| FR-05-04 | Hệ thống kiểm tra giới hạn số lượng sách được phép mượn. | Must | US-05-02 | BR-05-05 |
| FR-05-05 | Hệ thống cho phép ghi nhận nhiều bản sách trong một phiếu mượn. | Must | US-05-01 | BR-05-09 |
| FR-05-06 | Hệ thống ghi nhận ngày mượn theo thời điểm xác nhận trên hệ thống. | Must | US-05-01 | BR-05-14 |
| FR-05-07 | Hệ thống xác định thời hạn trả sách theo chính sách của thư viện. | Must | US-05-03 | BR-05-07, BR-05-08, BR-05-12 |
| FR-05-08 | Hệ thống cập nhật trạng thái bản sách sau khi cho mượn thành công. | Must | US-05-01 | BR-05-10 |
| FR-05-09 | Hệ thống cho phép xem danh sách và chi tiết phiếu mượn. | Should | US-05-04 | — |
| FR-05-10 | Hệ thống cho phép độc giả xem thông tin sách đang mượn và thời hạn trả. | Must | US-05-05 | BR-04-07 |
| FR-05-11 | Hệ thống kiểm tra độc giả có lượt mượn đang quá hạn trước khi cho mượn. | Must | US-05-02 | BR-05-06 |
| FR-05-12 | Hệ thống xác nhận phiếu mượn theo nguyên tắc toàn bộ hoặc không, và không cho phép một bản sách thuộc hai lượt mượn đang hiệu lực. | Must | US-05-01, US-05-02 | BR-05-13, BR-03-05, BR-05-15 |
| FR-05-13 | Hệ thống cho phép thủ thư hủy phiếu mượn lập sai khi chưa có lượt mượn nào trong phiếu được xử lý. | Must | US-05-06 | BR-05-16, BR-05-17, BR-05-18 |
| FR-05-14 | Hệ thống cho phép thủ thư chuyển các lượt mượn đang hiệu lực của một phiếu lập sai độc giả sang đúng độc giả trong một thao tác. | Must | US-05-07 | BR-05-18, BR-05-19 |

### FR-06 — Quản lý trả sách

| ID | Yêu cầu chức năng | Ưu tiên | User Story | Business Rule |
|---|---|---|---|---|
| FR-06-01 | Hệ thống cho phép thủ thư tra cứu lượt mượn đang hiệu lực theo mã bản sách. | Must | US-06-01 | BR-06-02 |
| FR-06-02 | Hệ thống cho phép thủ thư xác nhận trả từng bản sách. | Must | US-06-01, US-06-02 | BR-06-01, BR-06-03, BR-06-06 |
| FR-06-03 | Hệ thống ghi nhận ngày trả theo thời điểm xác nhận và tình trạng sách khi trả. | Must | US-06-01, US-06-04 | BR-06-04, BR-06-11, BR-06-13 |
| FR-06-04 | Hệ thống xác định lượt mượn trả quá hạn và số ngày quá hạn. | Must | US-06-03 | BR-06-05 |
| FR-06-05 | Hệ thống cập nhật trạng thái bản sách theo tình trạng khi trả. | Must | US-06-01, US-06-04 | BR-06-07, BR-06-08 |
| FR-06-06 | Hệ thống cho phép thủ thư ghi nhận bản sách đang mượn bị mất. | Must | US-06-05 | BR-06-09, BR-06-12, BR-06-14 |
| FR-06-07 | Hệ thống tự động hoàn tất phiếu mượn khi mọi lượt mượn đã được xử lý. | Must | US-06-02, US-06-05 | BR-06-10 |
| FR-06-08 | Hệ thống cho phép thủ thư xem danh sách lượt mượn đang quá hạn. | Should | US-06-06 | BR-08-03 |

### FR-07 — Tra cứu sách

| ID | Yêu cầu chức năng | Ưu tiên | User Story | Business Rule |
|---|---|---|---|---|
| FR-07-01 | Hệ thống cho phép tìm kiếm đầu sách theo từ khóa trong tên sách và tên tác giả. | Must | US-07-01 | BR-07-06 |
| FR-07-02 | Hệ thống cho phép tìm kiếm đầu sách theo ISBN. | Must | US-07-01 | — |
| FR-07-03 | Hệ thống cho phép lọc kết quả tìm kiếm theo thể loại. | Must | US-07-01 | — |
| FR-07-04 | Hệ thống phân trang và sắp xếp kết quả tìm kiếm. | Must | US-07-01 | — |
| FR-07-05 | Hệ thống hiển thị chi tiết đầu sách kèm số bản có thể mượn và vị trí lưu trữ. | Must | US-07-02 | BR-07-02, BR-07-05, BR-03-11 |
| FR-07-06 | Hệ thống không hiển thị danh tính độc giả đang mượn trong kết quả tra cứu. | Must | US-07-02 | BR-07-04 |
| FR-07-07 | Hệ thống chỉ trả về đầu sách đang lưu hành khi người tra cứu là độc giả. | Must | US-07-01 | BR-07-01 |
| FR-07-08 | Hệ thống cho phép thủ thư và quản trị viên tra cứu bao gồm đầu sách ngừng lưu hành. | Should | US-07-03 | BR-07-03 |

### FR-08 — Báo cáo và thống kê

| ID | Yêu cầu chức năng | Ưu tiên | User Story | Business Rule |
|---|---|---|---|---|
| FR-08-01 | Hệ thống cung cấp thống kê số đầu sách và số bản sách theo trạng thái và thể loại. | Must | US-08-01 | BR-08-01 |
| FR-08-02 | Hệ thống cung cấp báo cáo số lượt mượn và lượt trả theo khoảng thời gian. | Must | US-08-02 | BR-08-02, BR-08-05, BR-08-07, BR-08-08, BR-05-17 |
| FR-08-03 | Hệ thống cung cấp báo cáo sách đang mượn quá hạn và sách đã trả quá hạn. | Must | US-08-03 | BR-08-03, BR-08-04, BR-06-14 |
| FR-08-04 | Hệ thống cung cấp thống kê độc giả theo trạng thái thành viên và tình hình mượn sách. | Should | US-08-04 | — |
| FR-08-05 | Hệ thống cung cấp danh sách đầu sách được mượn nhiều nhất theo khoảng thời gian. | Could | US-08-05 | BR-08-05 |
| FR-08-06 | Hệ thống giới hạn quyền xem báo cáo cho thủ thư và quản trị viên. | Must | US-08-01, US-08-02, US-08-03, US-08-04, US-08-05 | BR-08-06 |

### FR-09 — Cấu hình chính sách mượn trả

| ID | Yêu cầu chức năng | Ưu tiên | User Story | Business Rule |
|---|---|---|---|---|
| FR-09-01 | Hệ thống cho phép quản trị viên xem chính sách mượn trả đang áp dụng. | Should | US-01-10 | — |
| FR-09-02 | Hệ thống cho phép quản trị viên cập nhật số bản sách được mượn đồng thời và thời hạn mượn. | Should | US-01-10 | BR-05-07, BR-05-12 |
| FR-09-03 | Hệ thống ghi nhận lịch sử thay đổi chính sách (người thay đổi, thời điểm, giá trị cũ và mới). | Should | US-01-10 | — |

Nếu FR-09 bị hoãn khỏi bản phát hành MVP, giá trị BP-01 và BP-02 được thiết lập trong cấu hình hệ thống khi triển khai.

## 4. Đặc tả chi tiết

### 4.1. Quy định chung

Các quy định sau áp dụng cho mọi chức năng, trừ khi đặc tả riêng nói khác:

| Mã | Quy định |
|---|---|
| GEN-01 | Mọi dữ liệu đầu vào được kiểm tra ở phía máy chủ, kể cả khi giao diện đã kiểm tra. |
| GEN-02 | Khoảng trắng ở đầu và cuối các trường văn bản được loại bỏ trước khi kiểm tra. |
| GEN-03 | Khi dữ liệu không hợp lệ, hệ thống không lưu bất kỳ thay đổi nào và trả về thông báo tiếng Việt chỉ rõ từng trường lỗi và lý do. |
| GEN-04 | Người dùng chưa đăng nhập truy cập chức năng cần đăng nhập được chuyển về màn hình đăng nhập. Người dùng không đủ quyền nhận thông báo không có quyền; thao tác không được thực hiện (BR-01-03). |
| GEN-05 | Yêu cầu tới một đối tượng không tồn tại hoặc ngoài phạm vi quyền của người dùng trả về thông báo không tìm thấy, không tiết lộ đối tượng có tồn tại hay không. |
| GEN-06 | Khi hai người cùng sửa một đối tượng, thay đổi gửi sau dựa trên dữ liệu cũ bị từ chối và người dùng được yêu cầu tải lại dữ liệu mới nhất. |
| GEN-07 | Danh sách được phân trang, mặc định 20 dòng mỗi trang, tối đa 100 dòng mỗi trang. |
| GEN-08 | Ngày giờ được hiển thị theo định dạng `dd/MM/yyyy HH:mm` và múi giờ của thư viện (BP-12). |
| GEN-09 | Các thao tác thay đổi dữ liệu nghiệp vụ được ghi vào nhật ký kiểm toán theo NFR-05-08. |
| GEN-10 | Thao tác không thể hoàn tác (thanh lý, ghi nhận mất, hủy phiếu mượn, chuyển phiếu mượn, khóa tài khoản, ngừng lưu hành, xóa) yêu cầu người dùng xác nhận trước khi thực hiện. |

### 4.2. Đăng nhập, đăng xuất, đổi mật khẩu (FR-01-01 → FR-01-03)

**Tác nhân:** mọi người dùng.

**Đầu vào:**

| Trường | Bắt buộc | Kiểm tra |
|---|---|---|
| Email | Có | Đúng định dạng email; không phân biệt chữ hoa, chữ thường. |
| Mật khẩu | Có | — |
| Mật khẩu hiện tại (đổi mật khẩu) | Có | Khớp mật khẩu đang dùng. |
| Mật khẩu mới (đổi mật khẩu) | Có | Đáp ứng chính sách mật khẩu (NFR-05-02); khác mật khẩu hiện tại. |

**Đầu ra:** phiên đăng nhập và giao diện theo vai trò; khi đăng xuất, phiên bị hủy; khi đổi mật khẩu thành công, các phiên khác của người dùng bị hủy.

**Ngoại lệ:**

| Tình huống | Xử lý |
|---|---|
| Sai email hoặc mật khẩu | Từ chối với thông báo chung, không cho biết trường nào sai. |
| Tài khoản bị khóa hoặc chưa kích hoạt | Từ chối và nêu trạng thái tài khoản. |
| Đăng nhập sai liên tiếp vượt ngưỡng | Tạm khóa đăng nhập theo NFR-05-03. |
| Phiên hết hạn do không hoạt động | Yêu cầu đăng nhập lại (NFR-05-04). |

### 4.3. Khôi phục mật khẩu (FR-01-04)

**Tác nhân:** mọi người dùng.

**Luồng chính:** người dùng nhập email → hệ thống luôn hiển thị cùng một thông báo → nếu email thuộc tài khoản Hoạt động, hệ thống gửi liên kết đặt lại → người dùng mở liên kết và nhập mật khẩu mới → hệ thống cập nhật mật khẩu, vô hiệu liên kết và hủy mọi phiên đang mở.

**Ngoại lệ:**

| Tình huống | Xử lý |
|---|---|
| Email không tồn tại hoặc tài khoản không ở trạng thái Hoạt động | Hiển thị cùng thông báo như trường hợp thành công; không gửi email. |
| Liên kết đã dùng hoặc hết hạn (NFR-05-05) | Từ chối và hướng dẫn gửi lại yêu cầu. |
| Dịch vụ gửi email lỗi | Ghi nhật ký lỗi và thử gửi lại (NFR-04-05); thông báo hiển thị cho người dùng không thay đổi. |

### 4.4. Tài khoản nhân viên (FR-01-05 → FR-01-09)

**Tác nhân:** quản trị viên.

**Đầu vào khi tạo hoặc cập nhật:**

| Trường | Bắt buộc | Kiểm tra |
|---|---|---|
| Họ tên | Có | 1–100 ký tự. |
| Email | Có | Đúng định dạng; không trùng với tài khoản hoặc hồ sơ độc giả nào khác (BR-01-02, BR-04-11). |
| Vai trò | Có | Thủ thư hoặc Quản trị viên. |

**Đầu ra:** tài khoản ở trạng thái Chưa kích hoạt; hệ thống gửi liên kết kích hoạt tới email (FR-01-12).

**Ngoại lệ:**

| Tình huống | Xử lý |
|---|---|
| Email trùng | Từ chối, nêu trường email bị trùng. |
| Đổi vai trò của tài khoản độc giả | Từ chối (BR-01-09). |
| Khóa hoặc hạ vai trò quản trị viên hoạt động cuối cùng | Từ chối (BR-01-12). |
| Khóa tài khoản đang có phiên đăng nhập | Khóa thành công; các phiên đang mở bị hủy ngay. |
| Đổi email của tài khoản | Hủy các phiên đang mở; vô hiệu mọi liên kết kích hoạt và khôi phục mật khẩu chưa dùng (BR-01-14). Nếu tài khoản Chưa kích hoạt, gửi liên kết kích hoạt mới tới email mới. |

**Khởi tạo quản trị viên đầu tiên (FR-01-14):**

- **Tác nhân:** người vận hành hệ thống, qua công cụ vận hành (không qua giao diện web).
- **Đầu vào:** họ tên và email của quản trị viên đầu tiên, kiểm tra như bảng trên.
- **Điều kiện trước:** dịch vụ gửi email đã được cấu hình (CON-03).
- **Luồng chính:** người vận hành chạy công cụ khởi tạo → hệ thống kiểm tra dịch vụ email đã được cấu hình và chưa có tài khoản quản trị viên nào ở trạng thái Hoạt động → nếu chưa có tài khoản quản trị viên đầu tiên thì tạo tài khoản vai trò Quản trị viên ở trạng thái Chưa kích hoạt; nếu đã có nhưng còn Chưa kích hoạt thì dùng lại tài khoản đó → cấp liên kết kích hoạt mới (liên kết cũ hết hiệu lực) và gửi tới email của tài khoản → công cụ chỉ báo kết quả gửi (thành công hoặc lỗi), không hiển thị liên kết → quản trị viên mở liên kết từ hộp thư của mình và tự đặt mật khẩu (FR-01-12).
- **Đầu ra:** tài khoản quản trị viên đầu tiên với một liên kết kích hoạt còn hiệu lực đã được gửi tới email; bản ghi nhật ký kiểm toán cho mỗi lần chạy công cụ (NFR-05-08). Liên kết không xuất hiện ở đầu ra của công cụ hay trong nhật ký (BR-01-13, NFR-09-02).

| Tình huống | Xử lý |
|---|---|
| Hệ thống đã có ít nhất một tài khoản quản trị viên ở trạng thái Hoạt động | Từ chối; không tạo tài khoản, không cấp liên kết. |
| Dịch vụ email chưa được cấu hình | Từ chối trước khi tạo tài khoản; hướng dẫn người vận hành cấu hình dịch vụ email rồi chạy lại. |
| Gửi email thất bại | Báo lỗi cho người vận hành. Tài khoản (nếu vừa tạo) vẫn ở trạng thái Chưa kích hoạt; người vận hành sửa nguyên nhân rồi chạy lại công cụ để cấp liên kết mới. |
| Tài khoản quản trị viên đầu tiên đã tồn tại và còn Chưa kích hoạt (ví dụ liên kết đã hết hạn sau 72 giờ) | Không tạo tài khoản thứ hai; cấp liên kết kích hoạt mới cho tài khoản đó. |
| Người vận hành nhập email khác với email của tài khoản đầu tiên đang Chưa kích hoạt | Cập nhật email của tài khoản đó, vô hiệu mọi liên kết cũ (BR-01-14), rồi cấp liên kết mới. |

### 4.5. Hồ sơ độc giả và tài khoản độc giả (FR-04-01, FR-04-02, FR-04-06, FR-04-07, FR-01-11 → FR-01-13)

**Tác nhân:** thủ thư; độc giả (khi kích hoạt tài khoản).

**Đầu vào hồ sơ độc giả:**

| Trường | Bắt buộc | Kiểm tra |
|---|---|---|
| Họ tên | Có | 1–100 ký tự. |
| Ngày sinh | Không | Không sau ngày hiện tại. |
| Số điện thoại | Có | 9–15 chữ số, cho phép dấu `+` ở đầu. |
| Email | Không | Đúng định dạng; không trùng (BR-04-11). |
| Địa chỉ | Không | Tối đa 255 ký tự. |
| Tạo tài khoản độc giả | Không | Chỉ chọn được khi có email. Mặc định là có. |

**Luồng chính khi đăng ký:**

1. Thủ thư nhập thông tin và lưu.
2. Hệ thống tạo hồ sơ với mã thành viên duy nhất (FR-04-07) và trạng thái Hoạt động.
3. Nếu có email và chọn tạo tài khoản: hệ thống tạo tài khoản vai trò Độc giả ở trạng thái Chưa kích hoạt, liên kết với hồ sơ, và gửi liên kết kích hoạt tới email đó.
4. Độc giả mở liên kết, đặt mật khẩu; tài khoản chuyển sang Hoạt động (FR-01-12).

Việc độc giả có tài khoản hay không không ảnh hưởng đến quyền mượn sách tại quầy.

**Thay đổi trạng thái thành viên:** đầu vào gồm trạng thái mới (Hoạt động, Đình chỉ, Hết hiệu lực) và lý do (bắt buộc, 1–255 ký tự).

**Ngoại lệ:**

| Tình huống | Xử lý |
|---|---|
| Email trùng với hồ sơ hoặc tài khoản khác | Từ chối lưu, nêu trường email. |
| Sửa mã thành viên | Không cho phép; trường chỉ đọc (BR-04-09). |
| Đổi email của hồ sơ đã có tài khoản | Cập nhật email đăng nhập theo (BR-01-10); hủy các phiên đang mở của tài khoản đó; vô hiệu mọi liên kết kích hoạt và khôi phục mật khẩu chưa dùng đã gửi tới email cũ (BR-01-14). Nếu tài khoản Chưa kích hoạt, gửi liên kết kích hoạt mới tới email mới. |
| Xóa email của hồ sơ đã có tài khoản | Từ chối; hồ sơ có tài khoản phải có email. |
| Thêm email cho hồ sơ chưa có tài khoản | Cho phép tạo tài khoản theo bước 3. |
| Liên kết kích hoạt hết hạn (NFR-05-05) | Từ chối; thủ thư hoặc quản trị viên gửi lại liên kết (FR-01-13). |
| Đổi trạng thái sang trạng thái hiện tại hoặc thiếu lý do | Từ chối. |

### 4.6. Danh mục sách (FR-02-01 → FR-02-12)

**Tác nhân:** thủ thư.

**Đầu vào đầu sách:**

| Trường | Bắt buộc | Kiểm tra |
|---|---|---|
| Tên sách | Có | 1–500 ký tự (BR-02-02). |
| Tác giả | Không | Một hoặc nhiều tác giả đã có trong hệ thống (BR-02-03). |
| Thể loại | Không | Một hoặc nhiều thể loại đã có (BR-02-04). |
| Nhà xuất bản | Không | Đã có trong hệ thống. |
| Năm xuất bản | Không | Số nguyên từ 1000 đến năm hiện tại. |
| ISBN | Không | ISBN-10 hoặc ISBN-13 hợp lệ, kể cả số kiểm tra; không trùng (BR-02-12, BR-02-13). Hệ thống chuẩn hóa bằng cách bỏ dấu gạch ngang và khoảng trắng. |
| Mô tả | Không | Tối đa 5.000 ký tự. |
| Ảnh bìa | Không | Định dạng và dung lượng theo NFR-05-09. |

**Danh mục phụ:** tác giả (họ tên 1–200 ký tự), thể loại (tên 1–100 ký tự, không trùng — BR-02-10), nhà xuất bản (tên 1–200 ký tự).

**Đầu ra:** đầu sách được tạo ở trạng thái Đang lưu hành, có mã định danh duy nhất.

**Ngoại lệ:**

| Tình huống | Xử lý |
|---|---|
| ISBN sai định dạng hoặc trùng | Từ chối, nêu lý do; nếu trùng thì cho biết đầu sách đang dùng ISBN đó. |
| Xóa đầu sách còn bản sách hoặc lịch sử | Từ chối và gợi ý ngừng lưu hành (BR-02-07). |
| Xóa tác giả, thể loại, nhà xuất bản đang được sử dụng | Từ chối, cho biết số đầu sách đang sử dụng (BR-02-09). |
| Ngừng lưu hành đầu sách đang có bản sách được mượn | Cho phép. Các lượt mượn hiện tại không bị ảnh hưởng; bản sách được trả về sẽ không đủ điều kiện cho mượn cho đến khi đầu sách được khôi phục (BR-03-11). |

### 4.7. Kho sách (FR-03-01 → FR-03-12)

**Tác nhân:** thủ thư.

**Đầu vào khi nhập bản sách:**

| Trường | Bắt buộc | Kiểm tra |
|---|---|---|
| Đầu sách | Có | Tồn tại và đang lưu hành. |
| Số lượng | Có | Số nguyên từ 1 đến 100 mỗi lần nhập. |
| Vị trí lưu trữ | Có | Đã có trong danh sách vị trí (BR-03-04). |
| Mã quản lý | Không | Nếu bỏ trống, hệ thống tự sinh. Nếu nhập tay (chỉ khi số lượng là 1): 1–50 ký tự chữ, số, dấu gạch ngang; không trùng (BR-03-03). |
| Ghi chú tình trạng vật lý | Không | Tối đa 255 ký tự. |

**Đầu ra:** các bản sách mới ở trạng thái Sẵn có; danh sách mã quản lý để in nhãn.

**Thay đổi trạng thái thủ công:** đầu vào gồm trạng thái mới và lý do (bắt buộc). Hệ thống chỉ chấp nhận các chuyển đổi tại mục 2.3 của Business Rules.

**Ngoại lệ:**

| Tình huống | Xử lý |
|---|---|
| Mã quản lý trùng | Từ chối, không tạo bản sách nào trong lần nhập. |
| Chuyển đổi trạng thái không hợp lệ (ví dụ thanh lý bản sách Đang mượn, thay đổi bản sách Đã thanh lý) | Từ chối, nêu trạng thái hiện tại và các chuyển đổi được phép (BR-03-09, BR-03-12, BR-03-13). |
| Đổi đầu sách của bản sách | Không cho phép (BR-03-02). |

### 4.8. Mượn sách (FR-05-01 → FR-05-12, FR-04-10)

**Tác nhân:** thủ thư.

**Điều kiện trước:** thủ thư đã đăng nhập.

**Đầu vào:**

| Trường | Bắt buộc | Kiểm tra |
|---|---|---|
| Độc giả | Có | Tìm theo mã thành viên (quét thẻ hoặc nhập tay). |
| Danh sách mã bản sách | Có | Ít nhất 1 bản (BR-05-03); không trùng trong phiếu (BR-05-09). |

**Luồng chính:**

1. Thủ thư chọn độc giả. Hệ thống hiển thị kết quả kiểm tra điều kiện mượn (FR-04-10): trạng thái thành viên, lượt mượn đang quá hạn, số bản còn được mượn.
2. Thủ thư quét lần lượt các bản sách. Với mỗi bản, hệ thống kiểm tra ngay điều kiện cho mượn (BR-03-11) và giới hạn (BR-05-05), hiển thị lý do nếu không hợp lệ.
3. Thủ thư xác nhận phiếu.
4. Hệ thống kiểm tra lại toàn bộ điều kiện tại thời điểm xác nhận. Nếu tất cả hợp lệ, hệ thống trong cùng một giao dịch: tạo phiếu mượn, ghi ngày mượn là thời điểm hiện tại (BR-05-14), tính thời hạn trả (BR-05-07), chuyển các bản sách sang Đang mượn (BR-05-10).
5. Hệ thống hiển thị phiếu mượn gồm mã phiếu, độc giả, danh sách bản sách và thời hạn trả.

**Đầu ra:** phiếu mượn ở trạng thái Đang mượn; mỗi bản sách là một lượt mượn ở trạng thái Đang mượn.

**Ngoại lệ:**

| Tình huống | Xử lý |
|---|---|
| Độc giả không ở trạng thái Hoạt động | Từ chối toàn bộ phiếu, nêu trạng thái (BR-04-02, BR-04-03). |
| Độc giả có lượt mượn đang quá hạn | Từ chối toàn bộ phiếu, liệt kê các lượt quá hạn (BR-05-06). |
| Vượt giới hạn mượn | Từ chối toàn bộ phiếu, cho biết số bản còn được mượn (BR-05-05). |
| Bản sách không đủ điều kiện cho mượn | Không cho thêm vào phiếu; nêu lý do cụ thể: trạng thái bản sách hoặc đầu sách ngừng lưu hành (BR-03-11). |
| Mã bản sách không tồn tại | Thông báo không tìm thấy bản sách. |
| Bản sách vừa được người khác cho mượn trước khi xác nhận | Từ chối toàn bộ phiếu, nêu bản sách bị ảnh hưởng (BR-03-05, BR-05-13). |
| Gửi lại cùng một yêu cầu xác nhận | Không tạo phiếu thứ hai; trả về phiếu đã tạo (NFR-04-02). |

**Hủy phiếu mượn lập sai (FR-05-13):**

- **Đầu vào:** mã phiếu mượn; lý do hủy (bắt buộc, 1–255 ký tự).
- **Luồng chính:** thủ thư mở phiếu mượn → chọn hủy và nhập lý do → xác nhận (GEN-10) → hệ thống trong cùng một giao dịch: chuyển phiếu và mọi lượt mượn sang Đã hủy, chuyển các bản sách về Sẵn có, ghi nhận người hủy, thời điểm và lý do. Thủ thư lập phiếu mới cho đúng độc giả hoặc đúng bản sách nếu cần.
- **Đầu ra:** phiếu mượn ở trạng thái Đã hủy. Phiếu này không tính vào giới hạn mượn, sách quá hạn, báo cáo, và không hiển thị với độc giả (BR-05-17).

| Tình huống | Xử lý |
|---|---|
| Phiếu đã có ít nhất một lượt được trả hoặc ghi nhận mất | Từ chối hủy (BR-05-16). Nếu phiếu lập sai độc giả, hiển thị gợi ý dùng chuyển phiếu (FR-05-14). |
| Phiếu đã ở trạng thái Đã hủy hoặc Hoàn tất | Từ chối hủy. |
| Thiếu lý do | Từ chối. |

**Chuyển phiếu lập sai độc giả (FR-05-14):**

- **Đầu vào:** mã phiếu mượn gốc; độc giả đúng (tìm theo mã thành viên); lý do (bắt buộc, 1–255 ký tự).
- **Luồng chính:**
  1. Thủ thư mở phiếu gốc và chọn chuyển phiếu.
  2. Hệ thống liệt kê các lượt còn ở trạng thái Đang mượn sẽ được chuyển. Các lượt đã trả hoặc ghi nhận mất được giữ nguyên trên phiếu gốc (BR-05-18).
  3. Thủ thư chọn độc giả đúng. Hệ thống hiển thị kết quả kiểm tra điều kiện mượn của độc giả đó (FR-04-10) dưới dạng **cảnh báo**, không chặn thao tác (BR-05-19).
  4. Thủ thư nhập lý do và xác nhận (GEN-10).
  5. Hệ thống trong cùng một giao dịch: chuyển các lượt Đang mượn của phiếu gốc sang Đã chuyển; tạo phiếu mới cho độc giả đúng với các bản sách đó, giữ nguyên ngày mượn và thời hạn trả của phiếu gốc; liên kết hai phiếu; ghi nhận người thực hiện, thời điểm và lý do; hoàn tất phiếu gốc nếu không còn lượt nào Đang mượn (BR-06-10). Bản sách giữ trạng thái Đang mượn.
- **Đầu ra:** phiếu mới của độc giả đúng; phiếu gốc ở trạng thái Hoàn tất.

| Tình huống | Xử lý |
|---|---|
| Phiếu gốc không còn lượt nào ở trạng thái Đang mượn | Từ chối chuyển. |
| Độc giả đúng trùng với độc giả trên phiếu gốc | Từ chối chuyển. |
| Độc giả đúng không ở trạng thái Hoạt động, có sách quá hạn hoặc sẽ vượt giới hạn mượn sau khi chuyển | Vẫn cho chuyển sau khi thủ thư xác nhận đã đọc cảnh báo. Độc giả đó vẫn bị chặn mượn mới theo các quy tắc thông thường. |
| Thiếu lý do | Từ chối. |
| Một lượt vừa được người khác xử lý trước khi xác nhận | Từ chối toàn bộ thao tác; thủ thư tải lại phiếu và thực hiện lại. |

### 4.9. Trả sách (FR-06-01 → FR-06-08)

**Tác nhân:** thủ thư.

**Đầu vào:**

| Trường | Bắt buộc | Kiểm tra |
|---|---|---|
| Mã bản sách | Có | Thuộc một lượt mượn đang hiệu lực (BR-06-02). |
| Kết quả xử lý | Có | Trả – sử dụng được; Trả – hư hỏng; Mất. |
| Mô tả | Bắt buộc khi hư hỏng hoặc mất | Tối đa 255 ký tự. |

**Luồng chính:**

1. Thủ thư quét mã bản sách. Hệ thống hiển thị độc giả, phiếu mượn, ngày mượn, thời hạn trả, và số ngày quá hạn nếu có (FR-06-01).
2. Thủ thư chọn kết quả xử lý và xác nhận.
3. Hệ thống trong cùng một giao dịch: ghi ngày trả là thời điểm hiện tại (BR-06-13), xác định đúng hạn hoặc quá hạn (BR-06-05), cập nhật trạng thái lượt mượn và bản sách theo bảng dưới, hoàn tất phiếu nếu mọi lượt mượn đã xử lý (BR-06-10).

| Kết quả xử lý | Lượt mượn | Bản sách |
|---|---|---|
| Trả – sử dụng được | Đã trả | Sẵn có |
| Trả – hư hỏng | Đã trả | Hư hỏng |
| Mất | Đã ghi nhận mất | Mất |

**Đầu ra:** thông tin lượt mượn sau xử lý; danh sách bản sách còn lại chưa trả của phiếu.

**Ngoại lệ:**

| Tình huống | Xử lý |
|---|---|
| Bản sách không thuộc lượt mượn đang hiệu lực (đã trả trước đó, chưa từng được mượn) | Từ chối, nêu trạng thái hiện tại của bản sách (BR-06-02, BR-06-03). |
| Thiếu mô tả khi hư hỏng hoặc mất | Từ chối. |
| Hai thủ thư cùng xác nhận trả một bản sách | Chỉ một xác nhận thành công; xác nhận còn lại bị từ chối (BR-06-03). |
| Độc giả bị đình chỉ hoặc hết hiệu lực | Vẫn cho trả bình thường (BR-04-04). |

### 4.10. Tra cứu sách (FR-07-01 → FR-07-08)

**Tác nhân:** độc giả, thủ thư, quản trị viên (đã đăng nhập — BR-07-06).

**Đầu vào:**

| Trường | Bắt buộc | Kiểm tra |
|---|---|---|
| Từ khóa | Không | Tối đa 200 ký tự; tìm trong tên sách và tên tác giả; không phân biệt chữ hoa, chữ thường; không phân biệt dấu tiếng Việt. |
| ISBN | Không | Chuẩn hóa như mục 4.6 trước khi so khớp chính xác. |
| Thể loại | Không | Một thể loại có trong hệ thống. |
| Bao gồm ngừng lưu hành | Không | Chỉ có hiệu lực với thủ thư và quản trị viên (BR-07-03). |
| Sắp xếp | Không | Mức độ phù hợp (mặc định), tên sách, năm xuất bản. |

**Đầu ra (danh sách):** tên sách, tác giả, thể loại, năm xuất bản, ảnh bìa (nếu có), số bản có thể mượn.

**Đầu ra (chi tiết):** thêm mô tả, nhà xuất bản, ISBN và danh sách vị trí lưu trữ của các bản có thể mượn. Không có thông tin người đang mượn (BR-07-04).

**Ngoại lệ:**

| Tình huống | Xử lý |
|---|---|
| Không có kết quả | Hiển thị thông báo không tìm thấy và gợi ý bỏ bớt điều kiện lọc. |
| Độc giả mở trực tiếp đầu sách ngừng lưu hành | Trả về không tìm thấy (GEN-05). |

### 4.11. Báo cáo (FR-08-01 → FR-08-06)

**Tác nhân:** thủ thư, quản trị viên.

| Báo cáo | Tham số | Nội dung |
|---|---|---|
| Kho sách (FR-08-01) | — (số liệu tại thời điểm xem) | Số đầu sách theo trạng thái lưu hành; số bản sách theo từng trạng thái; số đầu sách và bản sách theo thể loại. |
| Mượn trả (FR-08-02) | Từ ngày, đến ngày (tối đa 366 ngày) | Số lượt mượn, số lượt trả, số lượt ghi nhận mất; phân theo ngày. |
| Quá hạn (FR-08-03) | Từ ngày, đến ngày (cho phần đã trả quá hạn) | Danh sách lượt mượn đang quá hạn tại thời điểm xem; số lượt đã trả quá hạn trong khoảng thời gian. |
| Độc giả (FR-08-04) | — | Số độc giả theo trạng thái; số độc giả đang mượn ít nhất 1 bản; số độc giả có lượt quá hạn. |
| Sách mượn nhiều nhất (FR-08-05) | Từ ngày, đến ngày; số dòng (mặc định 20) | Đầu sách xếp theo số lượt mượn giảm dần. |

**Ngoại lệ:** ngày bắt đầu sau ngày kết thúc hoặc khoảng thời gian vượt giới hạn thì hệ thống từ chối và nêu lý do.

### 4.12. Cấu hình chính sách (FR-09-01 → FR-09-03)

**Tác nhân:** quản trị viên.

| Trường | Bắt buộc | Kiểm tra |
|---|---|---|
| Số bản sách được mượn đồng thời | Có | Số nguyên từ 1 đến 50. |
| Thời hạn mượn (ngày) | Có | Số nguyên từ 1 đến 180. |

**Đầu ra:** chính sách mới có hiệu lực ngay cho các phiếu mượn xác nhận sau thời điểm lưu (BR-05-12); một bản ghi lịch sử thay đổi được tạo.

**Ngoại lệ:** giá trị ngoài khoảng cho phép thì hệ thống từ chối. Giảm giới hạn mượn xuống dưới số bản độc giả đang mượn không ảnh hưởng tới lượt mượn hiện tại; độc giả đó chỉ không mượn thêm được cho đến khi trả bớt.

## 5. Phụ thuộc giữa các chức năng

| Chức năng | Phụ thuộc vào | Lý do |
|---|---|---|
| Mọi chức năng (trừ đăng nhập, khôi phục mật khẩu, kích hoạt) | FR-01-01, FR-01-09 | Cần xác thực và kiểm tra quyền. |
| FR-01-04, FR-01-12, FR-01-13, FR-01-14 | Dịch vụ gửi email | Gửi liên kết khôi phục và kích hoạt. Riêng FR-01-14 không chạy được nếu chưa cấu hình email. |
| FR-01-05 | FR-01-14 | Cần có quản trị viên đầu tiên để tạo các tài khoản nhân viên khác. |
| FR-01-11 | FR-04-01 | Tài khoản độc giả liên kết với hồ sơ độc giả. |
| FR-02-01 | FR-02-06, FR-02-07, FR-02-08 | Tác giả, thể loại, nhà xuất bản phải có trước khi gắn vào đầu sách. |
| FR-03-01 | FR-02-01, FR-03-04 | Bản sách thuộc một đầu sách và cần vị trí lưu trữ. |
| FR-05 | FR-03, FR-04, FR-09 (hoặc cấu hình BP-01, BP-02) | Cần bản sách, độc giả và chính sách mượn. |
| FR-06 | FR-05 | Chỉ trả được sách đã được mượn. |
| FR-07 | FR-02, FR-03 | Tra cứu danh mục và số bản có thể mượn. |
| FR-04-08, FR-04-09, FR-05-10 | FR-05, FR-06 | Hiển thị dữ liệu mượn trả. |
| FR-05-10, FR-04-08 (phía độc giả) | FR-01-11, FR-01-12 | Độc giả cần tài khoản đã kích hoạt và liên kết với hồ sơ. |
| FR-08 | FR-02 → FR-06 | Tổng hợp dữ liệu từ các nghiệp vụ. |

**Thứ tự triển khai đề xuất cho MVP:**

1. FR-01 (trừ FR-01-11), bắt đầu từ FR-01-14 — nền tảng xác thực, phân quyền và khởi tạo quản trị viên đầu tiên.
2. FR-02, FR-03 — danh mục và kho sách.
3. FR-04, FR-01-11 — độc giả và tài khoản độc giả.
4. FR-09 hoặc cấu hình mặc định BP-01, BP-02.
5. FR-05, FR-06 — mượn và trả sách.
6. FR-07 — tra cứu.
7. FR-08 — báo cáo.

## 6. Phạm vi MVP

- Bản phát hành MVP gồm toàn bộ FR mức Must và các FR mức Should chưa được duyệt hoãn.
- **Hoãn yêu cầu Should:** chỉ được hoãn khi Product Owner phê duyệt. Mỗi lần hoãn được ghi vào mục 8 của [user-stories.md](user-stories.md), gồm ID, lý do, phương án tạm thời (nếu có) và giai đoạn dự kiến thực hiện. Yêu cầu Should đã được duyệt hoãn không chặn nghiệm thu MVP. Ví dụ: nếu FR-09 được duyệt hoãn, BP-01 và BP-02 được đặt trong cấu hình khi triển khai.
- **Điều kiện nghiệm thu MVP:** đạt toàn bộ yêu cầu Must và toàn bộ yêu cầu Should chưa được duyệt hoãn. Yêu cầu Must không được hoãn.
- Các FR mức Could (FR-02-10, FR-03-09, FR-08-05) chỉ được thực hiện khi đã xong Must và Should. Trong MVP, việc kiểm kê được thực hiện thủ công bằng danh sách bản sách lọc theo vị trí (FR-03-12).
- Các nghiệp vụ ngoài MVP được liệt kê tại mục 7 của [user-stories.md](user-stories.md).
