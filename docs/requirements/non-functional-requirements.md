# Non-functional Requirements — BookShelf

## 1. Tổng quan

Tài liệu mô tả các yêu cầu phi chức năng của hệ thống BookShelf nhằm đảm bảo chất lượng, hiệu năng, bảo mật, độ tin cậy và khả năng vận hành của hệ thống quản lý thư viện.

Các mục tiêu được đặt ở mức phù hợp với bản phát hành MVP: một thư viện, một điểm triển khai, quy mô tại mục 2. Mục tiêu có thể được nâng lên ở các giai đoạn sau.

**Mức độ ưu tiên** dùng chung định nghĩa MoSCoW và quy định hoãn yêu cầu Should với [functional-requirements.md](functional-requirements.md) (mục 6). Nghiệm thu MVP yêu cầu đạt toàn bộ NFR mức Must và các NFR mức Should chưa được Product Owner duyệt hoãn.

**Cách kiểm chứng** cho biết yêu cầu được xác nhận bằng phương pháp nào: kiểm thử tự động, kiểm thử tải, kiểm tra cấu hình, rà soát mã nguồn, diễn tập hoặc theo dõi vận hành.

## 2. Quy mô hệ thống dự kiến

| Thông số | Giá trị |
|---|---:|
| Số lượng đầu sách | 50.000 |
| Số lượng bản sách vật lý | 200.000 |
| Số lượng độc giả | 20.000 |
| Số lượng người dùng đồng thời | 200 |
| Số lượt mượn sách mỗi ngày | 1.000 |
| Số lượt trả sách mỗi ngày | 1.000 |

Các thông số trên là mục tiêu thiết kế ban đầu và cần được thư viện xác nhận trước khi nghiệm thu.

## 3. Ràng buộc và giả định

| ID | Nội dung |
|---|---|
| CON-01 | Hệ thống là ứng dụng web, phục vụ một thư viện duy nhất. |
| CON-02 | Giao diện và nội dung hệ thống bằng tiếng Việt. MVP không hỗ trợ đa ngôn ngữ. |
| CON-03 | Hệ thống bắt buộc có một dịch vụ gửi email để gửi liên kết kích hoạt và khôi phục mật khẩu. Dịch vụ email phải được cấu hình trước khi khởi tạo quản trị viên đầu tiên (BR-01-13). |
| CON-04 | Quầy mượn trả có thể dùng máy quét mã vạch hoạt động như bàn phím; hệ thống không phụ thuộc vào thiết bị quét cụ thể. |
| CON-05 | Thời gian nghiệp vụ theo múi giờ UTC+7 (BP-12). |

## 4. Yêu cầu phi chức năng

### NFR-01 — Hiệu năng (Performance)

| ID | Yêu cầu | Ưu tiên | Cách kiểm chứng |
|---|---|---|---|
| NFR-01-01 | 95% yêu cầu xem và lấy dữ liệu đơn lẻ (chi tiết đầu sách, độc giả, phiếu mượn; danh sách có phân trang) được xử lý trong vòng 300 ms. | Must | Kiểm thử tải |
| NFR-01-02 | 95% yêu cầu tìm kiếm sách được xử lý trong vòng 500 ms. | Must | Kiểm thử tải |
| NFR-01-03 | 95% yêu cầu xác nhận mượn hoặc trả sách được xử lý trong vòng 1 giây. | Must | Kiểm thử tải |
| NFR-01-04 | 95% yêu cầu báo cáo (FR-08) được xử lý trong vòng 3 giây với khoảng thời gian tối đa cho phép. | Should | Kiểm thử tải |
| NFR-01-05 | Các mục tiêu NFR-01-01 đến NFR-01-04 phải đạt khi có 200 người dùng đồng thời, với dữ liệu ở quy mô tại mục 2, theo kịch bản kiểm thử tải đã thống nhất. | Must | Kiểm thử tải |

Thời gian phản hồi được đo tại phía máy chủ, từ khi nhận yêu cầu đến khi hoàn thành phản hồi, không bao gồm độ trễ mạng phía người dùng.

### NFR-02 — Khả năng mở rộng (Scalability)

| ID | Yêu cầu | Ưu tiên | Cách kiểm chứng |
|---|---|---|---|
| NFR-02-01 | Với dữ liệu gấp đôi quy mô tại mục 2 (100.000 đầu sách, 400.000 bản sách, 40.000 độc giả), hệ thống vẫn đạt NFR-01-01 đến NFR-01-03 mà không cần thay đổi mã nguồn. | Should | Kiểm thử tải với dữ liệu mẫu |
| NFR-02-02 | Hệ thống có thể phục vụ 400 người dùng đồng thời và vẫn đạt NFR-01 chỉ bằng cách bổ sung tài nguyên máy chủ, không cần thay đổi mã nguồn. | Could | Kiểm thử tải |
| NFR-02-03 | Dung lượng lưu trữ dữ liệu và tệp tải lên có thể mở rộng mà không làm gián đoạn dịch vụ quá thời gian bảo trì cho phép (NFR-03-03). | Should | Rà soát thiết kế triển khai |

### NFR-03 — Tính sẵn sàng (Availability)

| ID | Yêu cầu | Ưu tiên | Cách kiểm chứng |
|---|---|---|---|
| NFR-03-01 | Hệ thống đạt độ sẵn sàng tối thiểu 99,5% mỗi tháng (tương đương tối đa khoảng 3,6 giờ gián đoạn), không tính thời gian bảo trì có kế hoạch theo NFR-03-03. | Must | Theo dõi vận hành (NFR-09-04) |
| NFR-03-02 | Khi dịch vụ gặp sự cố, hệ thống được khôi phục hoạt động trong vòng 4 giờ (RTO, xem NFR-11-02). | Must | Diễn tập khôi phục |
| NFR-03-03 | Bảo trì có kế hoạch chỉ thực hiện ngoài giờ mở cửa của thư viện, được thông báo trước tối thiểu 24 giờ, và mỗi lần không quá 2 giờ. | Should | Quy trình vận hành |
| NFR-03-04 | Khi hệ thống hoặc một chức năng tạm thời không khả dụng, người dùng thấy thông báo bằng tiếng Việt thay vì trang lỗi kỹ thuật. | Must | Kiểm thử thủ công |

### NFR-04 — Độ tin cậy (Reliability)

| ID | Yêu cầu | Ưu tiên | Cách kiểm chứng |
|---|---|---|---|
| NFR-04-01 | Giao dịch mượn trả sách đã được xác nhận thành công không được mất do lỗi hoặc khởi động lại ứng dụng. | Must | Kiểm thử tự động |
| NFR-04-02 | Việc gửi lại cùng một yêu cầu giao dịch (bấm nút nhiều lần, mạng chập chờn) không được tạo ra phiếu mượn, lượt trả hoặc bản sách trùng lặp. | Must | Kiểm thử tự động |
| NFR-04-03 | Mỗi nghiệp vụ mượn, trả, nhập bản sách và thay đổi trạng thái được thực hiện trọn vẹn hoặc không thực hiện gì; không để dữ liệu ở trạng thái dở dang. | Must | Kiểm thử tự động |
| NFR-04-04 | Khi nhiều người cùng thao tác trên một bản sách, một lượt mượn hoặc một đối tượng, kết quả cuối cùng phải tuân thủ Business Rules (BR-03-05, BR-06-03) và thao tác bị từ chối phải nhận thông báo rõ ràng. | Must | Kiểm thử tự động có truy cập đồng thời |
| NFR-04-05 | Lỗi khi gửi email không làm thất bại nghiệp vụ chính. Email gửi lỗi được thử lại tối thiểu 3 lần trong vòng 30 phút và được ghi nhật ký nếu vẫn thất bại. | Should | Kiểm thử tự động |

### NFR-05 — Bảo mật (Security)

| ID | Yêu cầu | Ưu tiên | Cách kiểm chứng |
|---|---|---|---|
| NFR-05-01 | Mật khẩu được lưu bằng thuật toán băm một chiều có salt, thuộc danh sách khuyến nghị của OWASP cho lưu trữ mật khẩu. Không lưu, ghi nhật ký hoặc gửi mật khẩu ở dạng rõ. | Must | Rà soát mã nguồn |
| NFR-05-02 | Mật khẩu dài tối thiểu 8 ký tự, có cả chữ và số, và không trùng email của người dùng. | Must | Kiểm thử tự động |
| NFR-05-03 | Sau 5 lần đăng nhập sai liên tiếp trong 15 phút, tài khoản bị tạm chặn đăng nhập 15 phút. | Must | Kiểm thử tự động |
| NFR-05-04 | Phiên đăng nhập hết hạn sau 30 phút không hoạt động đối với tài khoản nhân viên và 7 ngày đối với tài khoản độc giả. | Must | Kiểm thử tự động |
| NFR-05-05 | Liên kết khôi phục mật khẩu hết hạn sau 30 phút; liên kết kích hoạt hết hạn sau 72 giờ. Mỗi liên kết chỉ dùng được một lần, và liên kết mới làm vô hiệu liên kết cũ. Khi email của tài khoản thay đổi, mọi liên kết chưa dùng đã gửi trước đó bị vô hiệu ngay (BR-01-14). | Must | Kiểm thử tự động |
| NFR-05-06 | Mọi kết nối tới hệ thống sử dụng HTTPS với TLS 1.2 trở lên; yêu cầu HTTP được chuyển hướng sang HTTPS. | Must | Kiểm tra cấu hình |
| NFR-05-07 | Quyền truy cập được kiểm tra ở phía máy chủ cho mọi yêu cầu (BR-01-03). Độc giả không truy cập được dữ liệu của độc giả khác bằng cách thay đổi định danh trong yêu cầu (BR-04-07). | Must | Kiểm thử tự động |
| NFR-05-08 | Hệ thống ghi nhật ký kiểm toán cho: khởi tạo quản trị viên đầu tiên, đăng nhập thành công và thất bại, tạo tài khoản, thay đổi email tài khoản, khóa và mở khóa, thay đổi vai trò, thay đổi trạng thái thành viên, thay đổi trạng thái bản sách, mượn, hủy phiếu mượn, chuyển phiếu mượn, trả, thay đổi chính sách. Mỗi bản ghi gồm người thực hiện, thời điểm, đối tượng, giá trị trước và sau. Nhật ký không cho phép sửa hoặc xóa qua ứng dụng và được lưu tối thiểu 1 năm. | Must | Kiểm thử tự động |
| NFR-05-09 | Tệp ảnh bìa chỉ chấp nhận JPEG, PNG, WebP, dung lượng tối đa 2 MB. Hệ thống kiểm tra nội dung thực của tệp, không chỉ phần mở rộng. | Could | Kiểm thử tự động |
| NFR-05-10 | Trước khi phát hành, hệ thống được quét bảo mật theo OWASP Top 10 và không còn lỗ hổng mức Cao hoặc Nghiêm trọng chưa xử lý. | Must | Báo cáo quét bảo mật |
| NFR-05-11 | Hệ thống chỉ thu thập thông tin cá nhân của độc giả cần cho nghiệp vụ (mục 4.5 của FR) và tuân thủ quy định pháp luật Việt Nam hiện hành về bảo vệ dữ liệu cá nhân. | Must | Rà soát pháp lý |
| NFR-05-12 | Thông tin bí mật (mật khẩu cơ sở dữ liệu, khóa dịch vụ email…) không được lưu trong mã nguồn. | Must | Rà soát mã nguồn |

### NFR-06 — Khả năng bảo trì (Maintainability)

| ID | Yêu cầu | Ưu tiên | Cách kiểm chứng |
|---|---|---|---|
| NFR-06-01 | Mọi Business Rule thuộc BR-03, BR-05 và BR-06 có ít nhất một kiểm thử tự động. | Must | Đối chiếu danh sách kiểm thử với BR |
| NFR-06-02 | Độ bao phủ kiểm thử tự động của phần xử lý nghiệp vụ đạt tối thiểu 70% số dòng mã. | Should | Báo cáo độ bao phủ |
| NFR-06-03 | Kiểm thử tự động và kiểm tra quy ước mã nguồn chạy tự động cho mỗi thay đổi trước khi được hợp nhất vào nhánh chính. | Must | Cấu hình CI |
| NFR-06-04 | Thay đổi cấu trúc cơ sở dữ liệu được quản lý bằng các tệp migration có phiên bản, chạy được tự động. | Must | Rà soát mã nguồn |
| NFR-06-05 | Tài liệu hướng dẫn cho phép một lập trình viên mới chạy được hệ thống trên máy cá nhân trong vòng 30 phút. | Should | Thử nghiệm với thành viên mới |
| NFR-06-06 | Cấu hình theo môi trường (kết nối cơ sở dữ liệu, dịch vụ email, chính sách mặc định) được tách khỏi mã nguồn. | Must | Rà soát mã nguồn |

### NFR-07 — Tính dễ sử dụng (Usability)

| ID | Yêu cầu | Ưu tiên | Cách kiểm chứng |
|---|---|---|---|
| NFR-07-01 | Thủ thư đã được hướng dẫn hoàn thành một phiếu mượn 3 bản sách trong vòng 60 giây và một lượt trả trong vòng 15 giây, tính từ khi quét mã đầu tiên. | Must | Kiểm thử với người dùng |
| NFR-07-02 | Các màn hình mượn và trả sách nhận được mã từ máy quét mã vạch (CON-04) và thao tác được hoàn toàn bằng bàn phím. | Must | Kiểm thử thủ công |
| NFR-07-03 | Thông báo lỗi bằng tiếng Việt, nêu rõ lý do và cách khắc phục, không hiển thị thông tin kỹ thuật (mã lỗi hệ thống, stack trace). | Must | Kiểm thử thủ công |
| NFR-07-04 | Màn hình dành cho độc giả sử dụng được trên điện thoại có chiều rộng màn hình từ 360 px. Màn hình dành cho nhân viên sử dụng được trên màn hình từ 1280 px. | Should | Kiểm thử thủ công |
| NFR-07-05 | Hệ thống hoạt động đúng trên hai phiên bản mới nhất của Chrome, Edge, Firefox và Safari. | Must | Kiểm thử trên trình duyệt |

### NFR-08 — Khả năng tiếp cận (Accessibility)

| ID | Yêu cầu | Ưu tiên | Cách kiểm chứng |
|---|---|---|---|
| NFR-08-01 | Các màn hình dành cho độc giả (đăng nhập, tra cứu, chi tiết sách, sách đang mượn, lịch sử) đáp ứng WCAG 2.1 mức AA. | Should | Công cụ kiểm tra tự động và kiểm tra thủ công |
| NFR-08-02 | Mọi chức năng sử dụng được hoàn toàn bằng bàn phím, có hiển thị rõ vị trí đang chọn. | Must | Kiểm thử thủ công |
| NFR-08-03 | Văn bản có tỷ lệ tương phản tối thiểu 4,5:1 so với nền; mọi trường nhập liệu có nhãn; thông tin không được truyền đạt chỉ bằng màu sắc (ví dụ trạng thái quá hạn có cả chữ). | Must | Công cụ kiểm tra tự động |
| NFR-08-04 | Không có lỗi mức Nghiêm trọng hoặc Cao khi kiểm tra bằng công cụ kiểm tra khả năng tiếp cận tự động trên các màn hình chính. | Should | Công cụ kiểm tra tự động |

### NFR-09 — Khả năng quan sát hệ thống (Observability)

| ID | Yêu cầu | Ưu tiên | Cách kiểm chứng |
|---|---|---|---|
| NFR-09-01 | Nhật ký ứng dụng có cấu trúc, mỗi bản ghi gồm thời điểm, mức độ, mã định danh yêu cầu và người dùng (nếu có). | Must | Rà soát nhật ký |
| NFR-09-02 | Nhật ký ứng dụng không chứa mật khẩu, mã liên kết kích hoạt hoặc khôi phục, mã phiên đăng nhập. | Must | Rà soát nhật ký |
| NFR-09-03 | Hệ thống cung cấp điểm kiểm tra tình trạng (health check) cho biết ứng dụng và cơ sở dữ liệu có hoạt động hay không. | Must | Kiểm thử tự động |
| NFR-09-04 | Hệ thống theo dõi tối thiểu: số yêu cầu, tỷ lệ lỗi, thời gian phản hồi p95 và thời gian hoạt động. | Should | Bảng theo dõi vận hành |
| NFR-09-05 | Người vận hành nhận cảnh báo khi hệ thống không phản hồi quá 5 phút, hoặc tỷ lệ lỗi phía máy chủ vượt 5% trong 5 phút, hoặc sao lưu thất bại. | Should | Diễn tập cảnh báo |
| NFR-09-06 | Nhật ký ứng dụng được lưu tối thiểu 30 ngày. | Should | Kiểm tra cấu hình |

### NFR-10 — Tính toàn vẹn dữ liệu (Data Integrity)

| ID | Yêu cầu | Ưu tiên | Cách kiểm chứng |
|---|---|---|---|
| NFR-10-01 | Tính duy nhất (mã tài khoản, email, mã đầu sách, ISBN, mã bản sách, mã thành viên, tên thể loại) được đảm bảo ở tầng lưu trữ dữ liệu, không chỉ ở tầng ứng dụng. | Must | Kiểm thử tự động |
| NFR-10-02 | Dữ liệu có lịch sử giao dịch (đầu sách, bản sách, hồ sơ độc giả, tài khoản, phiếu mượn) không bị xóa vật lý; việc loại bỏ được thể hiện bằng trạng thái. | Must | Rà soát thiết kế |
| NFR-10-03 | Số bản sách sẵn có và có thể mượn luôn khớp với trạng thái thực tế của bản sách (BR-03-07). Số bản sách ở trạng thái Đang mượn luôn bằng số lượt mượn đang hiệu lực. | Must | Truy vấn đối soát chạy tự động hằng ngày, cảnh báo khi lệch |
| NFR-10-04 | Thời điểm được lưu kèm múi giờ hoặc theo UTC, và được hiển thị theo múi giờ của thư viện (BP-12). | Must | Kiểm thử tự động |
| NFR-10-05 | Quan hệ giữa các đối tượng (bản sách – đầu sách, lượt mượn – phiếu mượn – bản sách – độc giả, tài khoản – hồ sơ độc giả) được ràng buộc ở tầng lưu trữ dữ liệu. | Must | Rà soát thiết kế |

### NFR-11 — Sao lưu và phục hồi sau sự cố (Backup & Disaster Recovery)

| ID | Yêu cầu | Ưu tiên | Cách kiểm chứng |
|---|---|---|---|
| NFR-11-01 | Lượng dữ liệu tối đa có thể mất khi xảy ra sự cố (RPO) không quá 24 giờ. Cơ sở dữ liệu và tệp tải lên được sao lưu tự động tối thiểu một lần mỗi ngày, ngoài giờ mở cửa. | Must | Kiểm tra lịch sao lưu |
| NFR-11-02 | Thời gian khôi phục hệ thống sau sự cố (RTO) không quá 4 giờ. | Must | Diễn tập khôi phục |
| NFR-11-03 | Bản sao lưu được lưu ở vị trí tách biệt với máy chủ chính, được mã hóa, và được giữ tối thiểu 30 ngày. | Must | Kiểm tra cấu hình |
| NFR-11-04 | Việc khôi phục từ bản sao lưu được diễn tập trước khi đưa vào vận hành và tối thiểu mỗi quý một lần; kết quả diễn tập được ghi nhận. | Must | Biên bản diễn tập |
| NFR-11-05 | Quy trình khôi phục được viết thành tài liệu để người vận hành thực hiện được mà không cần đội phát triển. | Should | Rà soát tài liệu |

RPO 24 giờ là mức chấp nhận cho MVP. Nếu thư viện không chấp nhận phải nhập lại giao dịch của tối đa một ngày, cần nâng NFR-11-01 lên mức sao lưu liên tục.
