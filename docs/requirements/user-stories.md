# BookShelf — Library Management System

## 1. Giới thiệu (Introduction)

BookShelf là hệ thống quản lý thư viện trên nền tảng web, dành cho các tổ chức có nhu cầu quản lý danh mục sách, kho sách, độc giả và các hoạt động mượn trả sách.

## 2. Tầm nhìn sản phẩm (Product Vision)

Xây dựng hệ thống quản lý thư viện tập trung, giúp đơn giản hóa các nghiệp vụ quản lý sách, kiểm soát tài sản thư viện và nâng cao hiệu quả phục vụ độc giả.

## 3. Mục tiêu (Objectives)

- Số hóa các nghiệp vụ quản lý thư viện.
- Quản lý tập trung thông tin sách và kho sách.
- Quản lý thông tin và hoạt động của độc giả.
- Quản lý quy trình mượn và trả sách.
- Kiểm soát tình trạng và số lượng sách.
- Hỗ trợ độc giả tra cứu thông tin sách.
- Cung cấp báo cáo và thống kê hoạt động thư viện.

## 4. Đối tượng người dùng (Actors)

| ID | Actor | Vai trò | Mô tả |
|---|---|---|---|
| ACT-01 | Administrator | Quản trị viên | Quản lý tài khoản, phân quyền và cấu hình hệ thống |
| ACT-02 | Librarian | Thủ thư | Quản lý sách, kho sách, độc giả và nghiệp vụ mượn trả |
| ACT-03 | Member | Độc giả | Tra cứu sách, theo dõi thông tin và lịch sử mượn trả |
| ACT-04 | Operator | Người vận hành | Triển khai, sao lưu và khởi tạo hệ thống qua công cụ vận hành; không phải vai trò trong ứng dụng |

## 5. Nhóm nghiệp vụ (Epics)

| ID | Epic | Mô tả |
|---|---|---|
| EP-01 | Quản lý tài khoản | Tài khoản và quyền truy cập |
| EP-02 | Quản lý danh mục sách | Thông tin sách, tác giả, thể loại, nhà xuất bản |
| EP-03 | Quản lý kho sách | Số lượng, vị trí và tình trạng từng bản sách |
| EP-04 | Quản lý độc giả | Thông tin và trạng thái thành viên |
| EP-05 | Quản lý mượn sách | Ghi nhận các giao dịch mượn sách |
| EP-06 | Quản lý trả sách | Trả sách, quá hạn, mất hoặc hư hỏng sách |
| EP-07 | Tra cứu sách | Tìm kiếm và kiểm tra tình trạng sách |
| EP-08 | Báo cáo và thống kê | Thống kê sách, độc giả và giao dịch |

## 6. User Stories

### 6.1. Quy ước

**Mã định danh:** `US-<epic>-<số thứ tự>`, ví dụ `US-05-01` là story thứ nhất của EP-05.

**Mức độ ưu tiên (MoSCoW):**

| Mức | Ý nghĩa | Thuộc bản phát hành MVP |
|---|---|---|
| Must | Bắt buộc phải có. Thiếu story này hệ thống không vận hành được nghiệp vụ cốt lõi. | Có |
| Should | Nên có. Chỉ hoãn khi thiếu nguồn lực và được Product Owner phê duyệt; mỗi lần hoãn được ghi vào mục 8. Story Should đã được duyệt hoãn không chặn nghiệm thu MVP. | Có, trừ khi đã được duyệt hoãn |
| Could | Có thì tốt. Chỉ làm khi đã xong toàn bộ Must và Should. | Không bắt buộc |
| Won't | Không thực hiện trong MVP (xem mục 7). | Không |

**Truy vết:** mỗi story liệt kê các Functional Requirement (FR) trong [functional-requirements.md](functional-requirements.md) và Business Rule (BR) trong [business-rules.md](business-rules.md) liên quan. Thuật ngữ và trạng thái (Sẵn có, đủ điều kiện cho mượn, quá hạn…) được định nghĩa tại mục 2 của Business Rules.

**Tiêu chí nghiệm thu** được viết theo dạng *Given* (điều kiện ban đầu) – *When* (hành động) – *Then* (kết quả mong đợi).

### 6.2. Tổng hợp

| Epic | Số story | Must | Should | Could |
|---|---:|---:|---:|---:|
| EP-01 — Quản lý tài khoản | 12 | 8 | 4 | 0 |
| EP-02 — Quản lý danh mục sách | 8 | 6 | 1 | 1 |
| EP-03 — Quản lý kho sách | 6 | 5 | 0 | 1 |
| EP-04 — Quản lý độc giả | 7 | 6 | 1 | 0 |
| EP-05 — Quản lý mượn sách | 7 | 6 | 1 | 0 |
| EP-06 — Quản lý trả sách | 6 | 5 | 1 | 0 |
| EP-07 — Tra cứu sách | 3 | 2 | 1 | 0 |
| EP-08 — Báo cáo và thống kê | 5 | 3 | 1 | 1 |
| **Tổng** | **54** | **41** | **10** | **3** |

---

### 6.3. EP-01 — Quản lý tài khoản

#### US-01-01 — Đăng nhập

**Actor:** Tất cả người dùng · **Ưu tiên:** Must · **Truy vết:** FR-01-01, BR-01-04, NFR-05-03

> Là một người dùng của hệ thống,  
> Tôi muốn đăng nhập bằng email và mật khẩu,  
> Để truy cập các chức năng thuộc quyền hạn của mình.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* tài khoản ở trạng thái Hoạt động, *When* người dùng nhập đúng email và mật khẩu, *Then* hệ thống cho đăng nhập và hiển thị giao diện tương ứng với vai trò của người dùng.
- **AC2** — *Given* người dùng nhập sai email hoặc mật khẩu, *When* gửi yêu cầu đăng nhập, *Then* hệ thống từ chối và hiển thị một thông báo chung, không cho biết email hay mật khẩu bị sai.
- **AC3** — *Given* tài khoản đang bị khóa hoặc chưa kích hoạt, *When* người dùng nhập đúng thông tin đăng nhập, *Then* hệ thống từ chối đăng nhập và nêu trạng thái của tài khoản.
- **AC4** — *Given* người dùng đã đăng nhập sai 5 lần liên tiếp trong 15 phút, *When* đăng nhập lần tiếp theo, *Then* hệ thống tạm chặn đăng nhập của tài khoản trong 15 phút.

#### US-01-02 — Đăng xuất

**Actor:** Tất cả người dùng · **Ưu tiên:** Must · **Truy vết:** FR-01-02

> Là một người dùng đã đăng nhập,  
> Tôi muốn đăng xuất khỏi hệ thống,  
> Để người khác không thể sử dụng phiên làm việc của tôi trên thiết bị dùng chung.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* người dùng đang đăng nhập, *When* chọn đăng xuất, *Then* phiên làm việc bị hủy và người dùng được chuyển về màn hình đăng nhập.
- **AC2** — *Given* người dùng đã đăng xuất, *When* truy cập lại một trang cần đăng nhập (kể cả bằng nút quay lại của trình duyệt), *Then* hệ thống yêu cầu đăng nhập lại.

#### US-01-03 — Đổi mật khẩu

**Actor:** Tất cả người dùng · **Ưu tiên:** Must · **Truy vết:** FR-01-03, NFR-05-02

> Là một người dùng đã đăng nhập,  
> Tôi muốn thay đổi mật khẩu của mình,  
> Để bảo vệ tài khoản khi nghi ngờ mật khẩu bị lộ.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* người dùng nhập đúng mật khẩu hiện tại và mật khẩu mới hợp lệ, *When* xác nhận đổi mật khẩu, *Then* hệ thống cập nhật mật khẩu, hủy các phiên đăng nhập khác của người dùng, và các lần đăng nhập sau phải dùng mật khẩu mới.
- **AC2** — *Given* người dùng nhập sai mật khẩu hiện tại, *When* xác nhận đổi mật khẩu, *Then* hệ thống từ chối và giữ nguyên mật khẩu cũ.
- **AC3** — *Given* mật khẩu mới không đáp ứng chính sách mật khẩu (tối thiểu 8 ký tự, có cả chữ và số, không trùng email), *When* xác nhận đổi mật khẩu, *Then* hệ thống từ chối và chỉ rõ yêu cầu chưa được đáp ứng.

#### US-01-04 — Khôi phục mật khẩu

**Actor:** Tất cả người dùng · **Ưu tiên:** Should · **Truy vết:** FR-01-04, NFR-05-05

> Là một người dùng quên mật khẩu,  
> Tôi muốn đặt lại mật khẩu qua email đã đăng ký,  
> Để lấy lại quyền truy cập mà không cần nhờ quản trị viên.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* người dùng nhập một email, *When* gửi yêu cầu khôi phục, *Then* hệ thống hiển thị cùng một thông báo bất kể email đó có tồn tại trong hệ thống hay không.
- **AC2** — *Given* email thuộc một tài khoản ở trạng thái Hoạt động, *When* yêu cầu khôi phục được gửi, *Then* hệ thống gửi đến email đó một liên kết đặt lại mật khẩu có hiệu lực trong 30 phút.
- **AC3** — *Given* liên kết đặt lại đã được sử dụng hoặc đã hết hạn, *When* người dùng mở liên kết, *Then* hệ thống từ chối và yêu cầu gửi lại yêu cầu khôi phục.

#### US-01-05 — Tạo tài khoản nhân viên

**Actor:** Quản trị viên · **Ưu tiên:** Must · **Truy vết:** FR-01-05, FR-01-12, BR-01-01, BR-01-02, BR-01-05, BR-01-08, BR-01-11

> Là một quản trị viên,  
> Tôi muốn tạo tài khoản cho thủ thư và quản trị viên khác,  
> Để họ có thể truy cập hệ thống với vai trò phù hợp.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* quản trị viên nhập họ tên, email và chọn vai trò Thủ thư hoặc Quản trị viên, *When* lưu tài khoản, *Then* hệ thống tạo tài khoản với mã định danh duy nhất, vai trò đã chọn, trạng thái Chưa kích hoạt, và gửi liên kết kích hoạt đến email đó.
- **AC2** — *Given* email đã được sử dụng bởi một tài khoản hoặc hồ sơ độc giả khác, *When* lưu tài khoản, *Then* hệ thống từ chối và thông báo email bị trùng.
- **AC3** — *Given* quản trị viên tạo tài khoản, *When* lưu, *Then* quản trị viên không nhập và không xem được mật khẩu của tài khoản đó.

#### US-01-06 — Cập nhật thông tin tài khoản

**Actor:** Quản trị viên · **Ưu tiên:** Should · **Truy vết:** FR-01-06, FR-01-15, BR-01-02, BR-01-14

> Là một quản trị viên,  
> Tôi muốn cập nhật thông tin của một tài khoản,  
> Để dữ liệu tài khoản luôn chính xác.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* quản trị viên sửa thông tin hợp lệ, *When* lưu thay đổi, *Then* hệ thống cập nhật thông tin tài khoản.
- **AC2** — *Given* email mới trùng với email của tài khoản khác, *When* lưu thay đổi, *Then* hệ thống từ chối và giữ nguyên dữ liệu cũ.
- **AC3** — *Given* một liên kết kích hoạt hoặc khôi phục mật khẩu còn hạn đã được gửi tới email cũ, *When* quản trị viên đổi email của tài khoản và sau đó liên kết cũ được mở, *Then* hệ thống từ chối liên kết đó.
- **AC4** — *Given* tài khoản đang Chưa kích hoạt, *When* quản trị viên đổi email, *Then* hệ thống gửi liên kết kích hoạt mới tới email mới.

#### US-01-07 — Khóa và mở khóa tài khoản

**Actor:** Quản trị viên · **Ưu tiên:** Must · **Truy vết:** FR-01-07, BR-01-04, BR-01-06, BR-01-12

> Là một quản trị viên,  
> Tôi muốn khóa hoặc mở khóa tài khoản,  
> Để ngăn truy cập trái phép mà không làm mất dữ liệu lịch sử.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* một tài khoản đang hoạt động, *When* quản trị viên khóa tài khoản, *Then* các phiên đang mở của tài khoản bị hủy ngay và người dùng đó không thể đăng nhập ở các lần tiếp theo.
- **AC2** — *Given* một tài khoản đã bị khóa, *When* quản trị viên xem lịch sử giao dịch liên quan, *Then* toàn bộ lịch sử vẫn được giữ nguyên.
- **AC3** — *Given* một tài khoản đang bị khóa, *When* quản trị viên mở khóa, *Then* người dùng có thể đăng nhập lại với quyền hạn như trước khi bị khóa.
- **AC4** — *Given* chỉ còn một tài khoản quản trị viên ở trạng thái Hoạt động, *When* quản trị viên cố gắng khóa tài khoản đó, *Then* hệ thống từ chối.

#### US-01-08 — Phân quyền người dùng

**Actor:** Quản trị viên · **Ưu tiên:** Must · **Truy vết:** FR-01-08, FR-01-09, BR-01-03, BR-01-05, BR-01-08, BR-01-09, BR-01-12

> Là một quản trị viên,  
> Tôi muốn thay đổi vai trò của tài khoản nhân viên giữa Thủ thư và Quản trị viên,  
> Để mỗi người chỉ thực hiện được những nghiệp vụ thuộc trách nhiệm của mình.

MVP sử dụng ba vai trò cố định (Quản trị viên, Thủ thư, Độc giả) với quyền hạn được định nghĩa tại mục 2.2 của Business Rules; không hỗ trợ tạo vai trò hoặc quyền tùy chỉnh.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* quản trị viên đổi vai trò của một tài khoản nhân viên, *When* lưu thay đổi, *Then* quyền hạn mới được áp dụng cho các thao tác tiếp theo của người dùng đó.
- **AC2** — *Given* người dùng không phải quản trị viên, *When* cố gắng thay đổi vai trò của bất kỳ tài khoản nào, *Then* hệ thống từ chối.
- **AC3** — *Given* người dùng không có quyền với một chức năng, *When* truy cập chức năng đó (qua giao diện hoặc gọi trực tiếp), *Then* hệ thống từ chối và không thực hiện thao tác.
- **AC4** — *Given* một tài khoản độc giả, *When* quản trị viên cố gắng đổi vai trò của tài khoản đó, *Then* hệ thống từ chối.
- **AC5** — *Given* chỉ còn một tài khoản quản trị viên ở trạng thái Hoạt động, *When* quản trị viên cố gắng đổi vai trò của tài khoản đó, *Then* hệ thống từ chối.

#### US-01-09 — Xem và cập nhật thông tin cá nhân

**Actor:** Tất cả người dùng · **Ưu tiên:** Should · **Truy vết:** FR-01-10, BR-04-10

> Là một người dùng đã đăng nhập,  
> Tôi muốn xem và cập nhật thông tin cá nhân của mình,  
> Để thư viện có thông tin liên hệ chính xác.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* người dùng mở trang thông tin cá nhân, *When* trang được hiển thị, *Then* người dùng chỉ thấy thông tin của chính mình.
- **AC2** — *Given* người dùng sửa một trường được phép chỉnh sửa (số điện thoại, địa chỉ), *When* lưu thay đổi, *Then* hệ thống cập nhật trường đó.
- **AC3** — *Given* một trường không được phép tự chỉnh sửa (vai trò, email, mã thành viên, trạng thái thành viên), *When* người dùng xem trang, *Then* trường đó chỉ hiển thị ở dạng chỉ đọc.

#### US-01-10 — Cấu hình chính sách mượn trả

**Actor:** Quản trị viên · **Ưu tiên:** Should · **Truy vết:** FR-09-01, FR-09-02, FR-09-03, BR-05-07, BR-05-12, BP-01, BP-02

> Là một quản trị viên,  
> Tôi muốn cấu hình các tham số chính sách mượn trả như số sách tối đa và thời hạn mượn,  
> Để hệ thống phản ánh đúng quy định hiện hành của thư viện mà không cần thay đổi phần mềm.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* quản trị viên thay đổi số lượng sách được mượn đồng thời hoặc thời hạn mượn, *When* lưu thay đổi, *Then* các giao dịch mượn tạo sau thời điểm đó áp dụng giá trị mới.
- **AC2** — *Given* đã có các giao dịch mượn được xác nhận trước khi thay đổi, *When* chính sách được cập nhật, *Then* thời hạn trả của các giao dịch đó không thay đổi.
- **AC3** — *Given* quản trị viên nhập giá trị ngoài khoảng cho phép (số sách từ 1 đến 50, số ngày từ 1 đến 180), *When* lưu thay đổi, *Then* hệ thống từ chối.
- **AC4** — *Given* chính sách được thay đổi, *When* quản trị viên xem lịch sử thay đổi, *Then* hệ thống hiển thị người thay đổi, thời điểm, giá trị cũ và giá trị mới.

#### US-01-11 — Kích hoạt tài khoản

**Actor:** Tất cả người dùng mới · **Ưu tiên:** Must · **Truy vết:** FR-01-12, FR-01-13, BR-01-04, BR-01-11, NFR-05-05

> Là một người dùng vừa được cấp tài khoản,  
> Tôi muốn kích hoạt tài khoản bằng liên kết gửi đến email của mình và tự đặt mật khẩu,  
> Để chỉ mình tôi biết mật khẩu và hệ thống xác nhận được tôi là chủ của email đó.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* tài khoản ở trạng thái Chưa kích hoạt và liên kết kích hoạt còn hiệu lực (72 giờ), *When* người dùng mở liên kết và đặt mật khẩu hợp lệ, *Then* tài khoản chuyển sang trạng thái Hoạt động và người dùng đăng nhập được bằng mật khẩu vừa đặt.
- **AC2** — *Given* liên kết kích hoạt đã hết hạn hoặc đã được sử dụng, *When* người dùng mở liên kết, *Then* hệ thống từ chối và hướng dẫn liên hệ thư viện để được gửi lại.
- **AC3** — *Given* tài khoản ở trạng thái Chưa kích hoạt, *When* thủ thư (với tài khoản độc giả) hoặc quản trị viên (với tài khoản nhân viên) chọn gửi lại liên kết kích hoạt, *Then* hệ thống gửi liên kết mới và liên kết cũ hết hiệu lực. Với quản trị viên đầu tiên khi hệ thống chưa có quản trị viên Hoạt động, người vận hành cấp lại liên kết theo US-01-12.
- **AC4** — *Given* tài khoản độc giả đã được kích hoạt, *When* độc giả đăng nhập, *Then* độc giả chỉ thấy dữ liệu của hồ sơ độc giả liên kết với tài khoản.

#### US-01-12 — Khởi tạo quản trị viên đầu tiên

**Actor:** Người vận hành · **Ưu tiên:** Must · **Truy vết:** FR-01-14, FR-01-12, BR-01-11, BR-01-13, BR-01-14, NFR-05-08

> Là một người vận hành hệ thống,  
> Tôi muốn tạo tài khoản quản trị viên đầu tiên khi triển khai hệ thống lần đầu,  
> Để thư viện có người tạo được các tài khoản nhân viên khác.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* dịch vụ email đã được cấu hình và hệ thống chưa có tài khoản quản trị viên nào, *When* người vận hành chạy công cụ khởi tạo với họ tên và email hợp lệ, *Then* hệ thống tạo tài khoản vai trò Quản trị viên ở trạng thái Chưa kích hoạt và gửi liên kết kích hoạt tới email đó; công cụ chỉ báo đã gửi thành công, không hiển thị liên kết.
- **AC2** — *Given* quản trị viên đầu tiên mở liên kết kích hoạt từ hộp thư của mình và đặt mật khẩu hợp lệ, *When* kích hoạt xong, *Then* quản trị viên đăng nhập được và tạo được tài khoản nhân viên khác.
- **AC3** — *Given* hệ thống đã có ít nhất một tài khoản quản trị viên ở trạng thái Hoạt động, *When* người vận hành chạy công cụ khởi tạo, *Then* hệ thống từ chối, không tạo tài khoản và không cấp liên kết.
- **AC4** — *Given* chức năng khởi tạo, *When* người dùng truy cập qua giao diện web, *Then* không có màn hình hoặc đường dẫn nào cho phép khởi tạo quản trị viên.
- **AC5** — *Given* công cụ được chạy, *When* xem nhật ký kiểm toán, *Then* có bản ghi cho mỗi lần chạy công cụ.
- **AC6** — *Given* tài khoản quản trị viên đầu tiên còn Chưa kích hoạt và liên kết kích hoạt đã hết hạn sau 72 giờ, *When* người vận hành chạy lại công cụ, *Then* hệ thống không tạo tài khoản thứ hai mà cấp liên kết kích hoạt mới cho tài khoản đó; liên kết cũ hết hiệu lực.
- **AC7** — *Given* tài khoản quản trị viên đầu tiên còn Chưa kích hoạt, *When* người vận hành chạy lại công cụ với một email khác, *Then* email của tài khoản được cập nhật, liên kết gửi tới email cũ bị từ chối, và liên kết mới được cấp cho email mới.
- **AC8** — *Given* dịch vụ email chưa được cấu hình, *When* người vận hành chạy công cụ khởi tạo, *Then* hệ thống từ chối trước khi tạo tài khoản và hướng dẫn cấu hình email.
- **AC9** — *Given* công cụ đã chạy (thành công hoặc lỗi), *When* xem đầu ra của công cụ và nhật ký hệ thống, *Then* không có nơi nào chứa liên kết kích hoạt.

---

### 6.4. EP-02 — Quản lý danh mục sách

#### US-02-01 — Thêm đầu sách mới

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-02-01, FR-02-09, BR-02-01, BR-02-02, BR-02-03, BR-02-04, BR-02-05, BR-02-12, BR-02-13

> Là một thủ thư,  
> Tôi muốn thêm đầu sách mới vào danh mục,  
> Để thư viện quản lý và cho mượn được sách đó.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* thủ thư nhập tên sách và các thông tin hợp lệ, *When* lưu đầu sách, *Then* hệ thống tạo đầu sách với mã định danh duy nhất.
- **AC2** — *Given* tên sách bị bỏ trống, *When* lưu đầu sách, *Then* hệ thống từ chối và thông báo tên sách là bắt buộc.
- **AC3** — *Given* thủ thư chọn nhiều tác giả và nhiều thể loại, *When* lưu đầu sách, *Then* đầu sách được liên kết với tất cả tác giả và thể loại đã chọn.
- **AC4** — *Given* thủ thư nhập ISBN sai định dạng hoặc sai số kiểm tra, *When* lưu đầu sách, *Then* hệ thống từ chối và thông báo ISBN không hợp lệ.
- **AC5** — *Given* ISBN đã được dùng cho một đầu sách khác, *When* lưu đầu sách, *Then* hệ thống từ chối và cho biết đầu sách đang dùng ISBN đó.
- **AC6** — *Given* thủ thư không nhập ISBN, *When* lưu đầu sách, *Then* hệ thống vẫn tạo đầu sách.

#### US-02-02 — Cập nhật thông tin đầu sách

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-02-02, FR-02-09, BR-02-02, BR-02-12, BR-02-13

> Là một thủ thư,  
> Tôi muốn sửa thông tin của một đầu sách,  
> Để danh mục luôn chính xác.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* thủ thư sửa thông tin hợp lệ, *When* lưu thay đổi, *Then* hệ thống cập nhật đầu sách và thông tin mới hiển thị trong kết quả tra cứu.
- **AC2** — *Given* thủ thư xóa trống tên sách, *When* lưu thay đổi, *Then* hệ thống từ chối và giữ nguyên dữ liệu cũ.
- **AC3** — *Given* đầu sách đã có lịch sử mượn trả, *When* thông tin đầu sách được cập nhật, *Then* các giao dịch đã phát sinh vẫn được giữ nguyên.

#### US-02-03 — Ngừng lưu hành đầu sách

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-02-03, FR-02-11, FR-02-12, BR-02-07, BR-02-08, BR-02-11, BR-03-11, BR-07-01, BR-08-07

> Là một thủ thư,  
> Tôi muốn đánh dấu một đầu sách là ngừng lưu hành,  
> Để không cho mượn mới nhưng vẫn giữ được lịch sử.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* một đầu sách đã ngừng lưu hành, *When* thủ thư thêm bản sách thuộc đầu sách đó vào phiếu mượn (kể cả bản sách đang ở trạng thái Sẵn có), *Then* hệ thống từ chối vì bản sách không đủ điều kiện cho mượn.
- **AC2** — *Given* một đầu sách đã ngừng lưu hành, *When* độc giả tra cứu sách, *Then* đầu sách đó không xuất hiện trong kết quả.
- **AC3** — *Given* đầu sách còn bản sách hoặc lịch sử giao dịch, *When* thủ thư cố gắng xóa đầu sách, *Then* hệ thống từ chối và gợi ý chuyển sang ngừng lưu hành.
- **AC4** — *Given* một đầu sách được chuyển sang ngừng lưu hành, *When* xem các báo cáo về giai đoạn trước đó, *Then* số liệu giao dịch lịch sử không thay đổi.
- **AC5** — *Given* đầu sách ngừng lưu hành có bản sách đang được mượn, *When* độc giả trả bản sách đó trong tình trạng sử dụng được, *Then* bản sách chuyển về Sẵn có nhưng vẫn không đủ điều kiện cho mượn.
- **AC6** — *Given* một đầu sách đã ngừng lưu hành, *When* thủ thư khôi phục lưu hành, *Then* các bản sách Sẵn có của đầu sách đó đủ điều kiện cho mượn trở lại và đầu sách xuất hiện lại trong kết quả tra cứu của độc giả.
- **AC7** — *Given* đầu sách chưa có bản sách và giao dịch nào, *When* thủ thư xóa đầu sách, *Then* hệ thống xóa đầu sách sau khi thủ thư xác nhận.

#### US-02-04 — Xem danh sách và chi tiết đầu sách

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-02-04, FR-02-05, BR-03-07, BR-03-11

> Là một thủ thư,  
> Tôi muốn xem danh sách đầu sách và thông tin chi tiết của từng đầu sách,  
> Để nắm được hiện trạng danh mục của thư viện.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* thủ thư mở danh sách đầu sách, *When* danh sách được hiển thị, *Then* danh sách được phân trang và có thể lọc theo trạng thái lưu hành.
- **AC2** — *Given* thủ thư chọn một đầu sách, *When* mở chi tiết, *Then* hệ thống hiển thị thông tin mô tả, tác giả, thể loại, nhà xuất bản, ISBN, trạng thái lưu hành, tổng số bản sách, số bản sách sẵn có và số bản sách có thể mượn.

#### US-02-05 — Quản lý tác giả

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-02-06, BR-02-03, BR-02-09

> Là một thủ thư,  
> Tôi muốn thêm, sửa và tra cứu thông tin tác giả,  
> Để gắn tác giả cho đầu sách một cách thống nhất, tránh trùng lặp.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* thủ thư nhập tên tác giả, *When* lưu tác giả, *Then* tác giả có thể được chọn khi thêm hoặc sửa đầu sách.
- **AC2** — *Given* tác giả đang được gắn với ít nhất một đầu sách, *When* thủ thư cố gắng xóa tác giả, *Then* hệ thống từ chối.

#### US-02-06 — Quản lý thể loại sách

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-02-07, BR-02-04, BR-02-09, BR-02-10

> Là một thủ thư,  
> Tôi muốn quản lý danh sách thể loại sách,  
> Để phân loại sách và hỗ trợ độc giả tra cứu theo thể loại.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* thủ thư nhập tên thể loại chưa tồn tại, *When* lưu thể loại, *Then* thể loại có thể được chọn khi thêm hoặc sửa đầu sách.
- **AC2** — *Given* tên thể loại đã tồn tại, *When* lưu thể loại, *Then* hệ thống từ chối và thông báo trùng lặp.
- **AC3** — *Given* thể loại đang được gắn với ít nhất một đầu sách, *When* thủ thư cố gắng xóa thể loại, *Then* hệ thống từ chối.

#### US-02-07 — Quản lý nhà xuất bản

**Actor:** Thủ thư · **Ưu tiên:** Should · **Truy vết:** FR-02-08, BR-02-09

> Là một thủ thư,  
> Tôi muốn quản lý danh sách nhà xuất bản,  
> Để thông tin xuất bản của đầu sách được nhập thống nhất.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* thủ thư nhập tên nhà xuất bản, *When* lưu, *Then* nhà xuất bản có thể được chọn khi thêm hoặc sửa đầu sách.
- **AC2** — *Given* nhà xuất bản đang được gắn với ít nhất một đầu sách, *When* thủ thư cố gắng xóa, *Then* hệ thống từ chối.

#### US-02-08 — Quản lý ảnh bìa và mô tả sách

**Actor:** Thủ thư · **Ưu tiên:** Could · **Truy vết:** FR-02-10, NFR-05-09

> Là một thủ thư,  
> Tôi muốn tải lên ảnh bìa và nhập mô tả cho đầu sách,  
> Để độc giả dễ nhận diện và lựa chọn sách khi tra cứu.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* thủ thư tải lên ảnh JPEG, PNG hoặc WebP không quá 2 MB, *When* lưu, *Then* ảnh bìa hiển thị ở trang chi tiết và kết quả tra cứu.
- **AC2** — *Given* tệp tải lên sai định dạng hoặc vượt dung lượng cho phép, *When* lưu, *Then* hệ thống từ chối và nêu rõ lý do.
- **AC3** — *Given* đầu sách chưa có ảnh bìa, *When* hiển thị đầu sách, *Then* hệ thống dùng ảnh mặc định.

---

### 6.5. EP-03 — Quản lý kho sách

#### US-03-01 — Nhập bản sách vật lý

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-03-01, FR-03-02, BR-03-01, BR-03-02, BR-03-03, BR-03-04, BR-02-06

> Là một thủ thư,  
> Tôi muốn nhập thêm các bản sách vật lý cho một đầu sách,  
> Để quản lý được từng cuốn sách thực tế trong kho.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* thủ thư chọn một đầu sách đang lưu hành và nhập số lượng bản sách (1–100) cùng vị trí lưu trữ, *When* lưu, *Then* hệ thống tạo từng bản sách với mã quản lý duy nhất, gắn với đầu sách đó, có trạng thái Sẵn có, và hiển thị danh sách mã để in nhãn.
- **AC2** — *Given* thủ thư không chỉ định vị trí lưu trữ, *When* lưu, *Then* hệ thống từ chối.
- **AC3** — *Given* mã quản lý nhập tay trùng với một bản sách đã có, *When* lưu, *Then* hệ thống từ chối và thông báo trùng mã.
- **AC4** — *Given* các bản sách đã được tạo, *When* thủ thư xem chi tiết đầu sách, *Then* tổng số bản sách, số bản sách sẵn có và số bản sách có thể mượn được cập nhật tương ứng.

#### US-03-02 — Cập nhật bản sách và vị trí lưu trữ

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-03-03, FR-03-04, BR-03-02, BR-03-04

> Là một thủ thư,  
> Tôi muốn cập nhật thông tin và vị trí lưu trữ của một bản sách,  
> Để tìm được sách nhanh chóng trên kệ.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* thủ thư chọn vị trí mới hợp lệ, *When* lưu thay đổi, *Then* bản sách được cập nhật vị trí mới.
- **AC2** — *Given* thủ thư cố gắng chuyển bản sách sang một đầu sách khác, *When* lưu thay đổi, *Then* hệ thống từ chối.

#### US-03-03 — Theo dõi tình trạng và trạng thái lưu hành của bản sách

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-03-05, FR-03-06, FR-03-12, BR-03-05, BR-03-06, BR-03-11, BR-03-12, BR-03-15

> Là một thủ thư,  
> Tôi muốn biết tình trạng vật lý và trạng thái lưu hành hiện tại của từng bản sách,  
> Để biết bản sách nào có thể cho mượn.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* thủ thư tra cứu một bản sách theo mã quản lý, *When* kết quả hiển thị, *Then* hệ thống hiển thị đầu sách, vị trí, ghi chú tình trạng vật lý, trạng thái lưu hành (Sẵn có, Đang mượn, Hư hỏng, Mất, Đã thanh lý) và bản sách có đủ điều kiện cho mượn hay không.
- **AC2** — *Given* bản sách đang được mượn, *When* thủ thư xem chi tiết, *Then* hệ thống hiển thị phiếu mượn đang hiệu lực và thời hạn trả.
- **AC3** — *Given* thủ thư lọc danh sách bản sách theo vị trí và trạng thái, *When* xem kết quả, *Then* hệ thống chỉ hiển thị các bản sách phù hợp, có phân trang. Danh sách này được dùng để đối chiếu thủ công khi kiểm kê trong MVP.
- **AC4** — *Given* bản sách đã có thay đổi trạng thái, *When* thủ thư xem lịch sử của bản sách, *Then* hệ thống hiển thị từng lần thay đổi với trạng thái cũ, trạng thái mới, người thực hiện, thời điểm và lý do.

#### US-03-04 — Xem số lượng bản sách sẵn có và có thể mượn

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-03-07, FR-03-08, BR-03-07, BR-03-08, BR-03-11

> Là một thủ thư,  
> Tôi muốn xem tổng số bản sách, số bản sẵn có và số bản có thể mượn của mỗi đầu sách,  
> Để trả lời nhanh độc giả và lập kế hoạch bổ sung sách.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* một đầu sách đang lưu hành có các bản sách ở nhiều trạng thái khác nhau, *When* thủ thư xem chi tiết đầu sách, *Then* số bản sách sẵn có bằng đúng số bản sách ở trạng thái Sẵn có, và số bản có thể mượn bằng số bản sẵn có.
- **AC2** — *Given* tất cả bản sách của đầu sách đang được mượn, *When* xem chi tiết, *Then* số bản sẵn có và số bản có thể mượn đều là 0 (không bao giờ âm).
- **AC3** — *Given* một đầu sách đã ngừng lưu hành có 2 bản sách ở trạng thái Sẵn có, *When* thủ thư xem chi tiết, *Then* số bản sẵn có là 2 và số bản có thể mượn là 0.

#### US-03-05 — Ghi nhận bản sách bị mất, hư hỏng hoặc thanh lý

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-03-10, FR-03-11, BR-03-06, BR-03-09, BR-03-10, BR-03-12, BR-03-13, BR-03-14, BR-03-15

> Là một thủ thư,  
> Tôi muốn ghi nhận bản sách bị mất, hư hỏng hoặc được thanh lý, và đưa bản sách trở lại lưu hành khi đã sửa hoặc tìm thấy,  
> Để số liệu kho phản ánh đúng thực tế.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* bản sách ở trạng thái Sẵn có, *When* thủ thư ghi nhận bản sách bị mất, hư hỏng hoặc thanh lý kèm lý do, *Then* bản sách không còn được tính vào số lượng sẵn có và không thể được cho mượn.
- **AC2** — *Given* bản sách đang ở trạng thái Đang mượn, *When* thủ thư cố gắng thanh lý, *Then* hệ thống từ chối.
- **AC3** — *Given* bản sách đã được thanh lý, *When* xem lịch sử mượn trả của bản sách, *Then* toàn bộ lịch sử vẫn được giữ nguyên.
- **AC4** — *Given* bản sách ở trạng thái Hư hỏng đã được sửa, hoặc ở trạng thái Mất đã được tìm thấy, *When* thủ thư chuyển bản sách về Sẵn có kèm lý do, *Then* bản sách được tính lại vào số lượng sẵn có và lịch sử trạng thái trước đó được giữ nguyên.
- **AC5** — *Given* bản sách ở trạng thái Đã thanh lý, *When* thủ thư cố gắng chuyển sang bất kỳ trạng thái nào khác, *Then* hệ thống từ chối.

#### US-03-06 — Kiểm kê kho sách theo đợt

**Actor:** Thủ thư · **Ưu tiên:** Could · **Truy vết:** FR-03-09

Story này không bắt buộc cho MVP. Trong MVP, thủ thư kiểm kê thủ công bằng danh sách bản sách lọc theo vị trí (US-03-03 AC3) và cập nhật trạng thái từng bản (US-03-05).

> Là một thủ thư,  
> Tôi muốn đối chiếu số bản sách thực tế trên kệ với dữ liệu trong hệ thống,  
> Để phát hiện sách thất lạc hoặc sai vị trí.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* thủ thư bắt đầu một đợt kiểm kê cho một khu vực lưu trữ, *When* lần lượt ghi nhận mã các bản sách tìm thấy, *Then* hệ thống đánh dấu các bản sách đã được kiểm.
- **AC2** — *Given* đợt kiểm kê kết thúc, *When* thủ thư xem kết quả, *Then* hệ thống liệt kê riêng các bản sách có trong hệ thống nhưng không tìm thấy và các bản sách tìm thấy nhưng sai vị trí.
- **AC3** — *Given* kết quả kiểm kê có chênh lệch, *When* đợt kiểm kê kết thúc, *Then* hệ thống không tự động thay đổi trạng thái bản sách; thủ thư phải xác nhận từng thay đổi.

---

### 6.6. EP-04 — Quản lý độc giả

#### US-04-01 — Đăng ký độc giả mới

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-04-01, FR-04-07, FR-01-11, FR-01-12, BR-04-01, BR-04-09, BR-04-11, BR-01-07, BR-01-09, BR-01-11

> Là một thủ thư,  
> Tôi muốn đăng ký hồ sơ cho độc giả mới và cấp tài khoản cho độc giả có email,  
> Để độc giả có thể mượn sách tại thư viện và tự theo dõi việc mượn sách của mình.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* thủ thư nhập đầy đủ thông tin bắt buộc (họ tên, số điện thoại), *When* lưu, *Then* hệ thống tạo hồ sơ độc giả với mã thành viên duy nhất do hệ thống cấp và trạng thái Hoạt động.
- **AC2** — *Given* thông tin bắt buộc bị thiếu hoặc sai định dạng, *When* lưu, *Then* hệ thống từ chối và chỉ rõ trường không hợp lệ.
- **AC3** — *Given* email đã được dùng bởi hồ sơ độc giả hoặc tài khoản khác, *When* lưu, *Then* hệ thống từ chối và thông báo email bị trùng.
- **AC4** — *Given* hồ sơ có email và thủ thư chọn tạo tài khoản, *When* lưu, *Then* hệ thống tạo tài khoản vai trò Độc giả ở trạng thái Chưa kích hoạt, liên kết với hồ sơ, và gửi liên kết kích hoạt đến email đó. Thủ thư không nhập và không xem được mật khẩu.
- **AC5** — *Given* hồ sơ không có email, *When* lưu, *Then* hệ thống chỉ tạo hồ sơ độc giả, không tạo tài khoản; độc giả vẫn mượn sách được tại quầy.

#### US-04-02 — Cập nhật thông tin độc giả

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-04-02, FR-01-11, FR-01-15, BR-01-10, BR-01-14, BR-04-09, BR-04-11

> Là một thủ thư,  
> Tôi muốn cập nhật thông tin độc giả,  
> Để có thông tin liên hệ chính xác khi cần nhắc trả sách.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* thủ thư sửa thông tin hợp lệ, *When* lưu, *Then* hồ sơ độc giả được cập nhật.
- **AC2** — *Given* thủ thư mở màn hình cập nhật, *When* màn hình hiển thị, *Then* mã thành viên chỉ hiển thị ở dạng chỉ đọc.
- **AC3** — *Given* hồ sơ đã có tài khoản, *When* thủ thư đổi email sang một email chưa được sử dụng, *Then* email đăng nhập của tài khoản đổi theo và các phiên đang mở của tài khoản bị hủy.
- **AC4** — *Given* hồ sơ đã có tài khoản, *When* thủ thư xóa trống email, *Then* hệ thống từ chối.
- **AC5** — *Given* hồ sơ chưa có tài khoản, *When* thủ thư bổ sung email và chọn tạo tài khoản, *Then* hệ thống tạo tài khoản độc giả và gửi liên kết kích hoạt như US-04-01 AC4.
- **AC6** — *Given* một liên kết kích hoạt hoặc khôi phục mật khẩu còn hạn đã được gửi tới email cũ, *When* thủ thư đổi email của hồ sơ và sau đó liên kết cũ được mở, *Then* hệ thống từ chối liên kết đó.
- **AC7** — *Given* tài khoản độc giả đang Chưa kích hoạt, *When* thủ thư đổi email, *Then* hệ thống gửi liên kết kích hoạt mới tới email mới.

#### US-04-03 — Tìm kiếm và xem thông tin độc giả

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-04-03, FR-04-04, FR-04-05

> Là một thủ thư,  
> Tôi muốn tìm độc giả theo mã thành viên, họ tên, email hoặc số điện thoại,  
> Để phục vụ độc giả nhanh chóng tại quầy.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* thủ thư nhập chính xác mã thành viên, *When* tìm kiếm, *Then* hệ thống trả về đúng một độc giả.
- **AC2** — *Given* thủ thư nhập một phần họ tên, *When* tìm kiếm, *Then* hệ thống trả về danh sách độc giả phù hợp, có phân trang.
- **AC3** — *Given* thủ thư chọn một độc giả, *When* mở chi tiết, *Then* hệ thống hiển thị thông tin cá nhân, trạng thái thành viên và số sách đang mượn.

#### US-04-04 — Quản lý trạng thái thành viên

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-04-06, BR-04-02, BR-04-03, BR-04-04, BR-04-06, BR-04-08, BP-10

> Là một thủ thư,  
> Tôi muốn thay đổi trạng thái thành viên của độc giả (Hoạt động, Đình chỉ, Hết hiệu lực),  
> Để kiểm soát quyền mượn sách theo quy định.

Trong MVP, trạng thái thành viên không tự động hết hạn; thủ thư chuyển trạng thái thủ công (BP-10).

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* độc giả bị chuyển sang trạng thái Đình chỉ hoặc Hết hiệu lực, *When* thủ thư tạo phiếu mượn cho độc giả đó, *Then* hệ thống từ chối.
- **AC2** — *Given* độc giả đang ở trạng thái Đình chỉ hoặc Hết hiệu lực và còn sách đang mượn, *When* thủ thư ghi nhận trả sách, *Then* hệ thống cho phép trả bình thường.
- **AC3** — *Given* trạng thái thành viên thay đổi, *When* xem danh sách sách đang mượn của độc giả, *Then* các giao dịch mượn và thời hạn trả hiện tại không thay đổi.
- **AC4** — *Given* thủ thư thay đổi trạng thái, *When* lưu, *Then* hệ thống ghi nhận người thay đổi, thời điểm và lý do; nếu thiếu lý do, hệ thống từ chối.

#### US-04-05 — Xem lịch sử mượn trả và sách đang mượn của độc giả

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-04-08, FR-04-09, BR-06-05, BR-05-17

> Là một thủ thư,  
> Tôi muốn xem sách đang mượn và lịch sử mượn trả của một độc giả,  
> Để giải đáp thắc mắc và xử lý tranh chấp.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* độc giả đang mượn sách, *When* thủ thư mở hồ sơ độc giả, *Then* hệ thống liệt kê từng bản sách đang mượn kèm ngày mượn, thời hạn trả, và đánh dấu bản sách quá hạn kèm số ngày quá hạn.
- **AC2** — *Given* độc giả đã có các giao dịch trước đó, *When* thủ thư xem lịch sử, *Then* hệ thống hiển thị các lượt mượn theo thứ tự thời gian, gồm ngày mượn, ngày trả thực tế, đúng hạn hoặc quá hạn, và kết quả xử lý (trả – sử dụng được, trả – hư hỏng, mất).
- **AC3** — *Given* độc giả có phiếu mượn đã bị hủy, *When* thủ thư xem lịch sử, *Then* phiếu đó được đánh dấu Đã hủy kèm lý do và người hủy.

#### US-04-06 — Kiểm tra điều kiện mượn sách của độc giả

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-04-10, BR-04-02, BR-04-03, BR-05-05, BR-05-06, BR-06-14

> Là một thủ thư,  
> Tôi muốn biết ngay độc giả có đủ điều kiện mượn sách hay không và còn được mượn bao nhiêu cuốn,  
> Để không mất thời gian lập phiếu mượn rồi mới bị từ chối.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* độc giả ở trạng thái Hoạt động, không có lượt mượn đang quá hạn và đang mượn ít hơn giới hạn, *When* thủ thư kiểm tra điều kiện, *Then* hệ thống xác nhận đủ điều kiện và hiển thị số bản sách còn được mượn.
- **AC2** — *Given* độc giả không đủ điều kiện, *When* thủ thư kiểm tra, *Then* hệ thống liệt kê đầy đủ các lý do (ví dụ: bị đình chỉ, có sách quá hạn, đã đạt giới hạn).
- **AC3** — *Given* độc giả có một lượt mượn đã được ghi nhận mất, *When* thủ thư kiểm tra điều kiện, *Then* lượt mượn đó không được tính vào số sách đang mượn và không được coi là đang quá hạn.

#### US-04-07 — Độc giả xem hồ sơ và lịch sử mượn trả của bản thân

**Actor:** Độc giả · **Ưu tiên:** Should · **Truy vết:** FR-04-08, FR-01-10, BR-04-07, BR-01-09, BR-05-17

> Là một độc giả,  
> Tôi muốn xem hồ sơ thành viên và lịch sử mượn trả của mình,  
> Để tự theo dõi hoạt động mượn sách.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* độc giả đã đăng nhập bằng tài khoản đã kích hoạt, *When* mở trang lịch sử, *Then* hệ thống hiển thị các lượt mượn của hồ sơ độc giả liên kết với tài khoản đó.
- **AC2** — *Given* độc giả cố gắng truy cập hồ sơ hoặc lịch sử của độc giả khác (kể cả bằng cách thay đổi đường dẫn), *When* gửi yêu cầu, *Then* hệ thống từ chối.
- **AC3** — *Given* hồ sơ của độc giả có phiếu mượn đã bị hủy, *When* độc giả xem lịch sử, *Then* phiếu đó không được hiển thị.

---

### 6.7. EP-05 — Quản lý mượn sách

#### US-05-01 — Tạo phiếu mượn sách

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-05-01, FR-05-05, FR-05-06, FR-05-08, FR-05-12, BR-05-01, BR-05-02, BR-05-03, BR-05-09, BR-05-10, BR-05-11, BR-05-13, BR-05-14, BR-05-15, BR-03-05, BR-03-11, NFR-04-02

> Là một thủ thư,  
> Tôi muốn lập phiếu mượn cho một độc giả với một hoặc nhiều bản sách,  
> Để ghi nhận chính xác sách nào đang được ai mượn.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* độc giả đủ điều kiện mượn và các bản sách đều đủ điều kiện cho mượn (BR-03-11: ở trạng thái Sẵn có và thuộc đầu sách đang lưu hành), *When* thủ thư xác nhận phiếu mượn, *Then* hệ thống tạo phiếu mượn ghi nhận độc giả, thủ thư, danh sách bản sách, ngày mượn và thời hạn trả.
- **AC2** — *Given* phiếu mượn được xác nhận thành công, *When* xem trạng thái các bản sách trong phiếu, *Then* tất cả đều chuyển sang trạng thái Đang mượn.
- **AC3** — *Given* phiếu mượn không có bản sách nào, *When* thủ thư xác nhận, *Then* hệ thống từ chối.
- **AC4** — *Given* thủ thư quét cùng một bản sách hai lần, *When* thêm vào phiếu, *Then* hệ thống không thêm trùng và thông báo bản sách đã có trong phiếu.
- **AC5** — *Given* hai thủ thư cùng lúc cho mượn cùng một bản sách, *When* cả hai xác nhận phiếu, *Then* chỉ một giao dịch thành công, giao dịch còn lại bị từ chối toàn bộ và nêu bản sách bị ảnh hưởng.
- **AC6** — *Given* phiếu mượn được xác nhận, *When* xem phiếu, *Then* ngày mượn là thời điểm hệ thống xác nhận; thủ thư không nhập hoặc sửa được ngày mượn.
- **AC7** — *Given* thủ thư bấm xác nhận nhiều lần cho cùng một phiếu, *When* hệ thống xử lý, *Then* chỉ một phiếu mượn được tạo.
- **AC8** — *Given* phiếu mượn đã được xác nhận, *When* thủ thư cố gắng sửa hoặc xóa phiếu, *Then* hệ thống không cho phép; sai sót khi lập phiếu được xử lý bằng cách chuyển phiếu sang đúng độc giả (US-05-07) hoặc hủy phiếu (US-05-06).

#### US-05-02 — Từ chối mượn khi không đủ điều kiện

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-05-02, FR-05-03, FR-05-04, FR-05-11, FR-05-12, BR-04-02, BR-04-03, BR-05-04, BR-05-05, BR-05-06, BR-05-13, BR-02-08, BR-03-06, BR-03-11, BP-01, BP-03

> Là một thủ thư,  
> Tôi muốn hệ thống tự động chặn các giao dịch mượn vi phạm quy định,  
> Để không phải tự kiểm tra thủ công từng điều kiện.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* độc giả không ở trạng thái Hoạt động, *When* thủ thư xác nhận phiếu mượn, *Then* hệ thống từ chối và nêu lý do.
- **AC2** — *Given* độc giả có ít nhất một lượt mượn đang quá hạn, *When* thủ thư xác nhận phiếu mượn, *Then* hệ thống từ chối và liệt kê các lượt quá hạn.
- **AC3** — *Given* độc giả đang mượn 4 bản sách và giới hạn là 5, *When* thủ thư xác nhận phiếu mượn 2 bản sách, *Then* hệ thống từ chối toàn bộ phiếu và cho biết độc giả chỉ được mượn thêm 1 bản.
- **AC4** — *Given* một bản sách không đủ điều kiện cho mượn (không ở trạng thái Sẵn có, hoặc thuộc đầu sách ngừng lưu hành), *When* thủ thư thêm bản sách vào phiếu, *Then* hệ thống từ chối bản sách đó và nêu lý do cụ thể.
- **AC5** — *Given* giao dịch mượn bị từ chối, *When* kiểm tra dữ liệu, *Then* không có phiếu mượn nào được tạo và không có bản sách nào bị thay đổi trạng thái.

#### US-05-03 — Tự động xác định thời hạn trả sách

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-05-07, BR-05-07, BR-05-08, BR-05-12, BP-02

> Là một thủ thư,  
> Tôi muốn hệ thống tự tính thời hạn trả theo chính sách của thư viện,  
> Để thời hạn trả được áp dụng thống nhất cho mọi độc giả.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* chính sách thời hạn mượn là 14 ngày, *When* phiếu mượn được xác nhận vào ngày D (theo giờ UTC+7), *Then* thời hạn trả của các bản sách trong phiếu là 23:59:59 ngày D + 14.
- **AC2** — *Given* chính sách thời hạn mượn được thay đổi sau khi phiếu đã xác nhận, *When* xem phiếu mượn đó, *Then* thời hạn trả không thay đổi.

#### US-05-04 — Xem danh sách và chi tiết phiếu mượn

**Actor:** Thủ thư · **Ưu tiên:** Should · **Truy vết:** FR-05-09

> Là một thủ thư,  
> Tôi muốn xem danh sách phiếu mượn và lọc theo trạng thái, độc giả hoặc khoảng thời gian,  
> Để theo dõi tình hình mượn sách.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* thủ thư mở danh sách phiếu mượn, *When* lọc theo trạng thái (đang mượn, đã hoàn tất), độc giả hoặc khoảng thời gian, *Then* hệ thống chỉ hiển thị các phiếu phù hợp, có phân trang.
- **AC2** — *Given* thủ thư chọn một phiếu mượn, *When* mở chi tiết, *Then* hệ thống hiển thị từng bản sách trong phiếu cùng trạng thái đã trả hay chưa.

#### US-05-05 — Độc giả xem sách đang mượn và thời hạn trả

**Actor:** Độc giả · **Ưu tiên:** Must · **Truy vết:** FR-05-10, BR-04-07, BR-01-09, BR-06-05

> Là một độc giả,  
> Tôi muốn xem danh sách sách mình đang mượn và thời hạn trả,  
> Để trả sách đúng hạn.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* độc giả đang mượn sách, *When* mở trang sách đang mượn, *Then* hệ thống hiển thị từng bản sách cùng ngày mượn và thời hạn trả.
- **AC2** — *Given* một bản sách đã quá hạn, *When* hiển thị danh sách, *Then* bản sách đó được đánh dấu quá hạn kèm số ngày quá hạn.
- **AC3** — *Given* độc giả không mượn sách nào, *When* mở trang, *Then* hệ thống hiển thị thông báo không có sách đang mượn.

#### US-05-06 — Hủy phiếu mượn lập sai

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-05-13, BR-05-15, BR-05-16, BR-05-17, BR-05-18, BR-08-02, NFR-05-08

> Là một thủ thư,  
> Tôi muốn hủy một phiếu mượn đã lập sai bản sách hoặc giao dịch không diễn ra,  
> Để dữ liệu mượn trả và báo cáo không bị ghi nhận sai.

Phiếu lập sai độc giả được xử lý bằng chuyển phiếu (US-05-07), không bằng hủy phiếu.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* phiếu mượn ở trạng thái Đang mượn và chưa có lượt nào được trả hoặc ghi nhận mất, *When* thủ thư hủy phiếu kèm lý do và xác nhận, *Then* phiếu và các lượt mượn chuyển sang Đã hủy, các bản sách trở về Sẵn có, và hệ thống ghi nhận người hủy, thời điểm và lý do.
- **AC2** — *Given* phiếu mượn đã có ít nhất một lượt được trả hoặc ghi nhận mất, *When* thủ thư cố gắng hủy phiếu, *Then* hệ thống từ chối; nếu phiếu lập sai độc giả, hệ thống gợi ý dùng chuyển phiếu (US-05-07).
- **AC3** — *Given* thủ thư không nhập lý do, *When* xác nhận hủy, *Then* hệ thống từ chối.
- **AC4** — *Given* một phiếu mượn đã bị hủy, *When* kiểm tra điều kiện mượn của độc giả hoặc tạo báo cáo mượn trả, *Then* phiếu đó không được tính vào giới hạn mượn, sách quá hạn, số lượt mượn và số lượt trả.
- **AC5** — *Given* thủ thư quét nhầm bản sách X thay vì bản sách Y cho cùng một độc giả, *When* thủ thư hủy phiếu và lập phiếu mới với bản sách Y, *Then* bản sách X trở về Sẵn có, phiếu mới được xác nhận, và báo cáo chỉ tính phiếu mới.

#### US-05-07 — Chuyển phiếu lập sai độc giả sang đúng độc giả

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-05-14, BR-05-15, BR-05-18, BR-05-19, BR-06-10, BR-08-02, NFR-05-08

> Là một thủ thư,  
> Tôi muốn chuyển các sách đang mượn của một phiếu lập nhầm độc giả sang đúng độc giả đang giữ sách,  
> Để hệ thống luôn ghi nhận đúng ai đang giữ sách, kể cả khi độc giả đó không đủ điều kiện mượn mới.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* phiếu 2 bản sách lập nhầm cho độc giả A thay vì độc giả B, chưa có lượt nào được xử lý, *When* thủ thư chuyển phiếu sang độc giả B kèm lý do, *Then* trong cùng một thao tác, 2 lượt của phiếu gốc chuyển sang Đã chuyển, phiếu mới của B được tạo với cùng ngày mượn và thời hạn trả, phiếu gốc chuyển sang Hoàn tất, và 2 bản sách luôn ở trạng thái Đang mượn.
- **AC2** — *Given* phiếu 3 bản sách lập nhầm cho độc giả A, 1 bản đã được trả, *When* thủ thư chuyển phiếu sang độc giả B, *Then* chỉ 2 bản còn Đang mượn được chuyển sang phiếu mới của B; lượt đã trả giữ nguyên trên phiếu gốc và vẫn được tính trong báo cáo (giới hạn của MVP — BR-05-18).
- **AC3** — *Given* độc giả B đã đạt giới hạn mượn, có sách quá hạn hoặc đang bị đình chỉ, *When* thủ thư chuyển phiếu sang B, *Then* hệ thống hiển thị cảnh báo; sau khi thủ thư xác nhận, thao tác vẫn thành công và các bản sách được ghi nhận là B đang mượn. B vẫn bị chặn mượn mới theo các quy tắc thông thường.
- **AC4** — *Given* thao tác chuyển phiếu thất bại vì bất kỳ lý do nào, *When* kiểm tra dữ liệu, *Then* phiếu gốc, các lượt mượn và trạng thái bản sách không thay đổi.
- **AC5** — *Given* chuyển phiếu thành công, *When* kiểm tra điều kiện mượn và lịch sử của độc giả A, *Then* các lượt Đã chuyển không tính vào giới hạn mượn hoặc sách quá hạn của A và không hiển thị trong lịch sử mà A xem được.
- **AC6** — *Given* chuyển phiếu thành công, *When* tạo báo cáo mượn trả, *Then* mỗi bản sách được chuyển chỉ được tính một lượt mượn (thuộc phiếu mới).
- **AC7** — *Given* thủ thư không nhập lý do hoặc chọn độc giả trùng với độc giả trên phiếu gốc, *When* xác nhận, *Then* hệ thống từ chối.

---

### 6.8. EP-06 — Quản lý trả sách

#### US-06-01 — Ghi nhận trả sách

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-06-01, FR-06-02, FR-06-03, FR-06-05, BR-06-01, BR-06-02, BR-06-03, BR-06-04, BR-06-07, BR-06-11, BR-06-13, BR-04-04

> Là một thủ thư,  
> Tôi muốn ghi nhận việc trả sách bằng cách quét mã bản sách,  
> Để cập nhật nhanh việc trả sách và đưa sách trở lại lưu hành.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* bản sách thuộc một lượt mượn đang hiệu lực, *When* thủ thư quét mã bản sách, *Then* hệ thống hiển thị độc giả, phiếu mượn, ngày mượn, thời hạn trả và số ngày quá hạn nếu có.
- **AC2** — *Given* bản sách được trả trong tình trạng sử dụng được, *When* thủ thư xác nhận trả, *Then* hệ thống ghi nhận thủ thư, ngày trả, tình trạng khi trả, chuyển lượt mượn sang Đã trả và bản sách về trạng thái Sẵn có.
- **AC3** — *Given* bản sách không thuộc lượt mượn nào đang hiệu lực (ví dụ đã được trả trước đó), *When* thủ thư quét mã để trả, *Then* hệ thống từ chối và nêu trạng thái hiện tại của bản sách.
- **AC4** — *Given* thủ thư xác nhận trả, *When* hệ thống ghi nhận, *Then* ngày trả là thời điểm hệ thống xác nhận; thủ thư không nhập hoặc sửa được ngày trả.
- **AC5** — *Given* hai thủ thư cùng xác nhận trả một bản sách, *When* hệ thống xử lý, *Then* chỉ một xác nhận thành công.

#### US-06-02 — Trả từng phần trong một phiếu mượn

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-06-02, FR-06-07, BR-06-06, BR-06-10, BP-04

> Là một thủ thư,  
> Tôi muốn ghi nhận trả từng bản sách riêng lẻ trong một phiếu mượn,  
> Để độc giả không phải trả tất cả sách cùng lúc.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* phiếu mượn có 3 bản sách, *When* độc giả trả 1 bản sách, *Then* phiếu mượn vẫn ở trạng thái đang mượn với 2 bản sách chưa trả.
- **AC2** — *Given* mọi lượt mượn còn lại trong phiếu đều đã được trả (kể cả trả hư hỏng) hoặc ghi nhận mất, *When* lượt mượn cuối cùng được xử lý, *Then* phiếu mượn chuyển sang trạng thái Hoàn tất.

#### US-06-03 — Xác định trả sách quá hạn

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-06-04, BR-06-05, BR-08-04, BP-07

> Là một thủ thư,  
> Tôi muốn hệ thống tự xác định bản sách được trả quá hạn,  
> Để lưu lại vi phạm và phục vụ thống kê.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* thời hạn trả là 23:59:59 ngày 10 và bản sách được trả vào ngày 13, *When* thủ thư xác nhận trả, *Then* hệ thống đánh dấu lượt mượn là trả quá hạn với số ngày quá hạn là 3.
- **AC2** — *Given* thời điểm trả không vượt thời hạn trả, *When* thủ thư xác nhận trả, *Then* lượt mượn được ghi nhận là trả đúng hạn.
- **AC3** — *Given* MVP không áp dụng tiền phạt quá hạn, *When* sách được trả quá hạn, *Then* hệ thống không phát sinh khoản phạt nào.

#### US-06-04 — Ghi nhận sách trả về bị hư hỏng

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-06-03, FR-06-05, BR-06-08, BR-06-12, BR-03-06, BP-09

> Là một thủ thư,  
> Tôi muốn ghi nhận bản sách được trả trong tình trạng hư hỏng,  
> Để bản sách đó không được cho mượn tiếp và có căn cứ xử lý.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* bản sách được trả trong tình trạng không sử dụng được, *When* thủ thư xác nhận trả với tình trạng hư hỏng và mô tả hư hỏng, *Then* lượt mượn chuyển sang Đã trả, bản sách chuyển sang trạng thái Hư hỏng và không được tính vào số lượng sẵn có.
- **AC2** — *Given* bản sách đã được ghi nhận hư hỏng, *When* thủ thư thêm bản sách vào phiếu mượn mới, *Then* hệ thống từ chối.
- **AC3** — *Given* thủ thư chọn tình trạng hư hỏng nhưng không nhập mô tả, *When* xác nhận trả, *Then* hệ thống từ chối.
- **AC4** — *Given* MVP không quản lý bồi thường (BP-09), *When* ghi nhận hư hỏng, *Then* hệ thống không phát sinh khoản bồi thường nào.

#### US-06-05 — Ghi nhận sách đang mượn bị mất

**Actor:** Thủ thư · **Ưu tiên:** Must · **Truy vết:** FR-06-06, FR-06-07, FR-03-11, BR-06-09, BR-06-10, BR-06-12, BR-06-14, BR-03-14, BP-08

> Là một thủ thư,  
> Tôi muốn ghi nhận bản sách mà độc giả báo làm mất,  
> Để khép lại lượt mượn và cập nhật đúng số liệu kho.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* bản sách đang được mượn, *When* thủ thư ghi nhận bản sách bị mất kèm mô tả, *Then* lượt mượn chuyển sang Đã ghi nhận mất, bản sách chuyển sang trạng thái Mất và không được tính vào số lượng sẵn có.
- **AC2** — *Given* bản sách mất là bản sách cuối cùng chưa xử lý trong phiếu, *When* ghi nhận mất, *Then* phiếu mượn chuyển sang trạng thái Hoàn tất.
- **AC3** — *Given* bản sách đã ghi nhận mất được tìm thấy lại, *When* thủ thư chuyển bản sách về Sẵn có, *Then* lượt mượn vẫn giữ kết quả Đã ghi nhận mất và lịch sử trạng thái của bản sách được giữ nguyên.
- **AC4** — *Given* độc giả có một lượt mượn đã ghi nhận mất, *When* kiểm tra điều kiện mượn, *Then* lượt mượn đó không tính vào giới hạn mượn và không được coi là đang quá hạn.
- **AC5** — *Given* MVP không quản lý bồi thường (BP-08), *When* ghi nhận mất, *Then* hệ thống không phát sinh khoản bồi thường nào.

#### US-06-06 — Theo dõi danh sách sách đang mượn quá hạn

**Actor:** Thủ thư · **Ưu tiên:** Should · **Truy vết:** FR-06-08, BR-08-03

> Là một thủ thư,  
> Tôi muốn xem danh sách các bản sách đang mượn quá hạn kèm thông tin liên hệ của độc giả,  
> Để chủ động nhắc độc giả trả sách.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* có bản sách chưa trả và đã vượt thời hạn trả, *When* thủ thư mở danh sách quá hạn, *Then* bản sách đó xuất hiện kèm độc giả, thông tin liên hệ, thời hạn trả và số ngày quá hạn.
- **AC2** — *Given* danh sách quá hạn đang hiển thị, *When* thủ thư sắp xếp theo số ngày quá hạn, *Then* danh sách được sắp xếp tương ứng.

---

### 6.9. EP-07 — Tra cứu sách

#### US-07-01 — Tìm kiếm sách

**Actor:** Độc giả · **Ưu tiên:** Must · **Truy vết:** FR-07-01, FR-07-02, FR-07-03, FR-07-04, FR-07-07, BR-07-01, BR-07-02, BR-07-06, NFR-01-02

> Là một độc giả,  
> Tôi muốn tìm sách theo tên sách, tác giả, thể loại hoặc ISBN,  
> Để biết thư viện có cuốn sách tôi cần hay không.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* độc giả nhập một phần tên sách hoặc tên tác giả, có dấu hoặc không dấu, chữ hoa hoặc chữ thường, *When* tìm kiếm, *Then* hệ thống trả về các đầu sách phù hợp, có phân trang.
- **AC2** — *Given* độc giả lọc theo thể loại, *When* tìm kiếm, *Then* chỉ các đầu sách thuộc thể loại đó được hiển thị.
- **AC3** — *Given* một đầu sách đang lưu hành nhưng không còn bản sách có thể mượn, *When* độc giả tìm kiếm, *Then* đầu sách vẫn xuất hiện trong kết quả với số bản có thể mượn là 0.
- **AC4** — *Given* một đầu sách đã ngừng lưu hành, *When* độc giả tìm kiếm, *Then* đầu sách đó không xuất hiện.
- **AC5** — *Given* không có đầu sách nào phù hợp, *When* tìm kiếm, *Then* hệ thống hiển thị thông báo không tìm thấy kết quả.
- **AC6** — *Given* độc giả nhập ISBN có dấu gạch ngang, *When* tìm kiếm, *Then* hệ thống trả về đầu sách có ISBN tương ứng.
- **AC7** — *Given* người dùng chưa đăng nhập, *When* truy cập chức năng tra cứu, *Then* hệ thống yêu cầu đăng nhập (BP-11).

#### US-07-02 — Xem chi tiết và tình trạng có thể mượn

**Actor:** Độc giả · **Ưu tiên:** Must · **Truy vết:** FR-07-05, FR-07-06, BR-07-04, BR-07-05, BR-03-11

> Là một độc giả,  
> Tôi muốn xem chi tiết đầu sách và biết hiện còn bản sách nào có thể mượn,  
> Để quyết định có đến thư viện mượn sách hay không.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* độc giả mở chi tiết một đầu sách, *When* trang hiển thị, *Then* hệ thống hiển thị thông tin mô tả, tác giả, thể loại, nhà xuất bản, ISBN, số bản sách có thể mượn và vị trí lưu trữ của các bản đó.
- **AC2** — *Given* đầu sách có bản sách đang mượn, hư hỏng, mất hoặc đã thanh lý, *When* hiển thị số bản có thể mượn, *Then* các bản sách đó không được tính (BR-03-11).
- **AC3** — *Given* có bản sách của đầu sách đang được mượn, *When* độc giả xem chi tiết, *Then* hệ thống không hiển thị bất kỳ thông tin nào về danh tính người đang mượn.
- **AC4** — *Given* độc giả mở trực tiếp đường dẫn tới một đầu sách đã ngừng lưu hành, *When* trang được yêu cầu, *Then* hệ thống trả về không tìm thấy.

#### US-07-03 — Thủ thư tra cứu toàn bộ danh mục

**Actor:** Thủ thư · **Ưu tiên:** Should · **Truy vết:** FR-07-08, BR-07-03

> Là một thủ thư,  
> Tôi muốn tra cứu cả các đầu sách đã ngừng lưu hành,  
> Để trả lời các câu hỏi về sách trước đây thư viện từng có.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* thủ thư tra cứu với tùy chọn bao gồm sách ngừng lưu hành, *When* tìm kiếm, *Then* kết quả gồm cả đầu sách ngừng lưu hành và trạng thái được thể hiện rõ.
- **AC2** — *Given* người dùng có vai trò độc giả, *When* tra cứu, *Then* tùy chọn bao gồm sách ngừng lưu hành không khả dụng.

---

### 6.10. EP-08 — Báo cáo và thống kê

> Áp dụng chung cho mọi story trong EP-08 (FR-08-06, BR-08-06): chỉ thủ thư và quản trị viên được xem báo cáo; độc giả không được truy cập các báo cáo này. Mốc thời gian trong báo cáo tính theo giờ UTC+7 (BR-08-08).

#### US-08-01 — Thống kê đầu sách và bản sách

**Actor:** Thủ thư, Quản trị viên · **Ưu tiên:** Must · **Truy vết:** FR-08-01, FR-08-06, BR-08-01, BR-03-07

> Là một thủ thư,  
> Tôi muốn xem thống kê số đầu sách và số bản sách theo trạng thái và thể loại,  
> Để nắm được quy mô và tình trạng tài sản của thư viện.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* thủ thư mở báo cáo kho sách, *When* báo cáo hiển thị, *Then* số đầu sách và số bản sách được thống kê riêng biệt.
- **AC2** — *Given* thủ thư xem báo cáo, *When* nhóm theo trạng thái bản sách, *Then* tổng số bản sách ở các trạng thái bằng tổng số bản sách của thư viện.
- **AC3** — *Given* thủ thư xem báo cáo, *When* nhóm theo thể loại, *Then* hệ thống hiển thị số đầu sách và số bản sách của từng thể loại.

#### US-08-02 — Báo cáo mượn trả theo khoảng thời gian

**Actor:** Thủ thư, Quản trị viên · **Ưu tiên:** Must · **Truy vết:** FR-08-02, FR-08-06, BR-08-02, BR-08-05, BR-08-07, BR-08-08, BR-05-17, NFR-01-04

> Là một thủ thư,  
> Tôi muốn xem số lượt mượn và trả sách trong một khoảng thời gian,  
> Để đánh giá mức độ hoạt động của thư viện.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* thủ thư chọn khoảng thời gian không quá 366 ngày, *When* tạo báo cáo, *Then* hệ thống hiển thị số lượt mượn, số lượt trả và số lượt ghi nhận mất trong khoảng đó, phân theo ngày.
- **AC2** — *Given* một phiếu mượn có 3 bản sách, *When* tính số lượt mượn, *Then* phiếu đó được tính là 3 lượt mượn.
- **AC3** — *Given* có giao dịch bị từ chối, chưa được xác nhận hoặc phiếu mượn đã bị hủy, *When* tạo báo cáo, *Then* các giao dịch đó không được tính.
- **AC4** — *Given* một đầu sách đã ngừng lưu hành hoặc bản sách đã thanh lý, *When* tạo báo cáo cho khoảng thời gian trước đó, *Then* số liệu không thay đổi so với trước khi ngừng lưu hành hoặc thanh lý.
- **AC5** — *Given* ngày bắt đầu sau ngày kết thúc hoặc khoảng thời gian vượt 366 ngày, *When* tạo báo cáo, *Then* hệ thống từ chối và nêu lý do.

#### US-08-03 — Báo cáo sách quá hạn

**Actor:** Thủ thư, Quản trị viên · **Ưu tiên:** Must · **Truy vết:** FR-08-03, FR-08-06, BR-08-03, BR-08-04, BR-06-14

> Là một thủ thư,  
> Tôi muốn xem thống kê sách đang mượn quá hạn và sách đã trả quá hạn,  
> Để đánh giá tình trạng tuân thủ quy định mượn trả.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* thủ thư mở báo cáo quá hạn, *When* báo cáo hiển thị, *Then* số bản sách đang mượn quá hạn và số lượt đã trả quá hạn được thống kê riêng biệt.
- **AC2** — *Given* bản sách đã được ghi nhận mất, *When* tính số sách đang mượn quá hạn, *Then* bản sách đó không được tính.

#### US-08-04 — Thống kê độc giả

**Actor:** Thủ thư, Quản trị viên · **Ưu tiên:** Should · **Truy vết:** FR-08-04, FR-08-06, BR-08-06

> Là một thủ thư,  
> Tôi muốn xem thống kê độc giả theo trạng thái thành viên và số độc giả đang mượn sách,  
> Để đánh giá mức độ sử dụng thư viện.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* thủ thư mở báo cáo độc giả, *When* báo cáo hiển thị, *Then* hệ thống hiển thị số độc giả theo từng trạng thái thành viên.
- **AC2** — *Given* thủ thư xem báo cáo, *When* báo cáo hiển thị, *Then* hệ thống hiển thị số độc giả hiện đang mượn ít nhất một bản sách và số độc giả có sách quá hạn.

#### US-08-05 — Thống kê sách được mượn nhiều nhất

**Actor:** Thủ thư · **Ưu tiên:** Could · **Truy vết:** FR-08-05, FR-08-06, BR-08-05

> Là một thủ thư,  
> Tôi muốn xem danh sách đầu sách được mượn nhiều nhất trong một khoảng thời gian,  
> Để có căn cứ bổ sung thêm bản sách cho các đầu sách có nhu cầu cao.

**Tiêu chí nghiệm thu:**

- **AC1** — *Given* thủ thư chọn khoảng thời gian, *When* tạo báo cáo, *Then* hệ thống liệt kê các đầu sách theo số lượt mượn giảm dần, trong đó số lượt mượn được tính theo từng bản sách.

## 7. Phạm vi ngoài MVP (Out of Scope)

- Đọc sách điện tử trực tuyến.
- Mua bán sách trực tuyến.
- Mạng xã hội dành cho người đọc sách.
- Quản lý nhiều chi nhánh thư viện.
- Thanh toán tiền phạt trực tuyến.
- Đề xuất sách bằng trí tuệ nhân tạo.
- Gia hạn mượn sách, đặt trước sách và tiền phạt quá hạn (BP-05, BP-06, BP-07).
- Tra cứu sách không cần đăng nhập (BP-11).
- Quản lý bồi thường sách mất hoặc hư hỏng trong hệ thống (BP-08, BP-09).
- Tự động gửi email nhắc hạn trả hoặc thông báo quá hạn.
- Vai trò và quyền tùy chỉnh; một tài khoản có nhiều vai trò.
- Tự đăng ký thành viên trực tuyến.
- Xuất báo cáo ra tệp (Excel, PDF).
- Hiệu chỉnh giao dịch mượn trả đã xử lý, ví dụ chuyển lượt mượn đã trả sang độc giả khác (BR-05-18).
- Đa ngôn ngữ.

## 8. Quyết định phạm vi MVP

Các vấn đề phát sinh trong quá trình rà soát đã được chốt như sau:

| ID | Vấn đề | Quyết định | Tài liệu liên quan |
|---|---|---|---|
| DEC-01 | Cấu hình chính sách mượn trả chưa có FR | Bổ sung nhóm FR-09 (mức Should). Nếu hoãn, BP-01 và BP-02 được đặt trong cấu hình khi triển khai. | FR-09, US-01-10 |
| DEC-02 | Ai tạo tài khoản độc giả và cách liên kết với hồ sơ | Thủ thư tạo tài khoản độc giả cùng lúc với hồ sơ (hoặc sau đó), liên kết 1–1; độc giả tự kích hoạt qua email để xác minh quyền sở hữu. Quản trị viên chỉ tạo tài khoản nhân viên. | BR-01-09 → BR-01-11, FR-01-11 → FR-01-13, US-01-11, US-04-01 |
| DEC-03 | Khái niệm "được phép công bố" của đầu sách | Bỏ khái niệm riêng; độc giả thấy mọi đầu sách đang lưu hành. | BR-07-01 |
| DEC-04 | Mâu thuẫn giữa "sẵn có" và "đủ điều kiện cho mượn" | Định nghĩa thống nhất "đủ điều kiện cho mượn" = Sẵn có và đầu sách đang lưu hành; tách hai số "sẵn có" và "có thể mượn". | BR-03-07, BR-03-11, US-03-04, US-05-01 |
| DEC-05 | Chính sách sách mất, hư hỏng, thời hạn thành viên | Chỉ ghi nhận trạng thái; bồi thường xử lý ngoài hệ thống; thành viên không tự động hết hạn. | BP-08 → BP-10 |
| DEC-06 | Khách chưa đăng nhập tra cứu sách | Không hỗ trợ trong MVP. | BP-11, BR-07-06 |
| DEC-07 | Chính sách mật khẩu, thời hạn liên kết, giới hạn ảnh bìa | Xác định trong NFR-05. | NFR-05-02, NFR-05-05, NFR-05-09 |
| DEC-08 | Kiểm kê kho sách | Kiểm kê theo đợt chuyển xuống Could; MVP kiểm kê thủ công bằng danh sách lọc theo vị trí. | FR-03-09, FR-03-12, US-03-06 |
| DEC-09 | Ngày mượn và ngày trả | Lấy theo thời điểm hệ thống xác nhận; không cho nhập tay. | BR-05-14, BR-06-13 |
| DEC-10 | Tạo quản trị viên đầu tiên khi hệ thống chưa có dữ liệu | Người vận hành dùng công cụ vận hành; chỉ chạy được khi chưa có quản trị viên Hoạt động; chạy lại thì cấp liên kết mới cho tài khoản đầu tiên còn Chưa kích hoạt thay vì tạo tài khoản thứ hai. Liên kết chỉ gửi qua email, không hiển thị cho người vận hành; dịch vụ email phải được cấu hình trước. Quản trị viên tự kích hoạt và đặt mật khẩu. | BR-01-13, FR-01-14, US-01-12, CON-03 |
| DEC-11 | Liên kết đã gửi tới email cũ sau khi đổi email | Đổi email làm vô hiệu ngay mọi liên kết kích hoạt và khôi phục mật khẩu chưa dùng. | BR-01-14, FR-01-15, NFR-05-05 |
| DEC-12 | Sửa sai sót sau khi xác nhận phiếu mượn | Lập sai độc giả: chuyển các lượt còn Đang mượn sang đúng độc giả trong một giao dịch, giữ nguyên ngày mượn và hạn trả, không chặn bởi điều kiện mượn (chỉ cảnh báo). Lập sai bản sách hoặc giao dịch không diễn ra: hủy toàn bộ phiếu khi chưa có lượt nào được xử lý. Lượt đã trả hoặc ghi nhận mất không hiệu chỉnh được (giới hạn của MVP). | BR-05-15 → BR-05-19, FR-05-13, FR-05-14, US-05-06, US-05-07 |
| DEC-13 | Hoãn yêu cầu Should có chặn nghiệm thu không | Should chỉ hoãn khi Product Owner phê duyệt và được ghi vào bảng hoãn dưới đây; Should đã được duyệt hoãn không chặn nghiệm thu MVP. | FR mục 6, NFR mục 1 |

**Yêu cầu Should đã được duyệt hoãn:**

| ID | Lý do hoãn | Phương án tạm thời | Người phê duyệt, ngày | Giai đoạn dự kiến |
|---|---|---|---|---|
| — | Chưa có | — | — | — |

## 9. Vấn đề còn mở

Các nội dung sau cần thư viện xác nhận trước khi nghiệm thu tài liệu:

| ID | Nội dung cần xác nhận | Tài liệu liên quan |
|---|---|---|
| OI-01 | Giá trị chính sách cho MVP: 5 bản, 14 ngày, cách xử lý sách mất và hư hỏng, thời hạn thành viên. | BP-01, BP-02, BP-08 → BP-10 |
| OI-02 | Quy mô hệ thống dự kiến (số đầu sách, bản sách, độc giả, người dùng đồng thời). | NFR mục 2 |
| OI-03 | Mức độ sẵn sàng 99,5% và RPO 24 giờ có chấp nhận được không. | NFR-03-01, NFR-11-01 |
| OI-04 | Có cần chuyển dữ liệu sách và độc giả hiện có vào hệ thống khi đưa vào sử dụng không. Nếu có, cần bổ sung yêu cầu nhập dữ liệu hàng loạt vào MVP. | — |
| OI-05 | Nhân viên đồng thời là độc giả phải dùng hai tài khoản với hai email khác nhau. Cần xác nhận cách làm này chấp nhận được. | BR-01-08 |
