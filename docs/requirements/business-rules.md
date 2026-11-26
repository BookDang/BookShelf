# Business Rules — BookShelf

## 1. Tổng quan

Tài liệu mô tả các quy tắc, điều kiện và ràng buộc nghiệp vụ trong hệ thống quản lý thư viện BookShelf.

Các quy tắc nghiệp vụ phải được tuân thủ trong quá trình thiết kế, phát triển và vận hành hệ thống.

Phạm vi của tài liệu là phiên bản MVP. Các nghiệp vụ ngoài MVP (gia hạn, đặt trước, tiền phạt, nhiều chi nhánh…) không được mô tả ở đây.

## 2. Thuật ngữ và trạng thái nghiệp vụ

### 2.1. Thuật ngữ

| Thuật ngữ | Định nghĩa |
|---|---|
| Đầu sách | Một ấn phẩm trong danh mục, được mô tả bởi tên sách, tác giả, thể loại, nhà xuất bản, ISBN… |
| Bản sách | Một cuốn sách vật lý thuộc một đầu sách, có mã quản lý riêng. |
| Tài khoản | Thông tin đăng nhập và vai trò của một người dùng. |
| Hồ sơ độc giả | Thông tin thành viên thư viện của một người, có mã thành viên. Hồ sơ độc giả tồn tại độc lập với tài khoản. |
| Phiếu mượn | Một giao dịch mượn của một độc giả, gồm một hoặc nhiều lượt mượn. |
| Lượt mượn | Việc mượn một bản sách cụ thể trong một phiếu mượn. |
| Sẵn có | Trạng thái của bản sách đang ở thư viện và sử dụng được. |
| Đủ điều kiện cho mượn | Xem BR-03-11. |
| Quá hạn | Xem BR-06-05. |
| Thời điểm nghiệp vụ | Mọi ngày giờ nghiệp vụ (ngày mượn, hạn trả, ngày trả, báo cáo) được tính theo múi giờ của thư viện (BP-12). |

### 2.2. Vai trò

MVP có ba vai trò cố định. Không hỗ trợ tạo vai trò hoặc quyền tùy chỉnh.

| Vai trò | Phạm vi quyền |
|---|---|
| Quản trị viên | Quản lý tài khoản nhân viên, vai trò, khóa/mở khóa tài khoản, cấu hình chính sách mượn trả, xem báo cáo. |
| Thủ thư | Quản lý danh mục, kho sách, hồ sơ độc giả, tài khoản độc giả, mượn trả sách, xem báo cáo. |
| Độc giả | Tra cứu sách; xem hồ sơ, sách đang mượn và lịch sử mượn trả của bản thân. |

Người vận hành hệ thống (triển khai, sao lưu, khởi tạo) không phải là một vai trò trong ứng dụng. Người vận hành chỉ thao tác qua công cụ vận hành, ví dụ khi khởi tạo quản trị viên đầu tiên (BR-01-13).

### 2.3. Trạng thái bản sách

| Trạng thái | Ý nghĩa | Tính là sẵn có |
|---|---|---|
| Sẵn có | Đang ở thư viện, sử dụng được | Có |
| Đang mượn | Thuộc một lượt mượn đang hiệu lực | Không |
| Hư hỏng | Không sử dụng được, chờ sửa chữa hoặc thanh lý | Không |
| Mất | Không xác định được vị trí hoặc độc giả làm mất | Không |
| Đã thanh lý | Đã loại khỏi kho; trạng thái cuối | Không |

**Chuyển đổi trạng thái hợp lệ:**

| Từ | Sang | Khi nào | Người thực hiện |
|---|---|---|---|
| (mới) | Sẵn có | Nhập bản sách vào kho | Thủ thư |
| Sẵn có | Đang mượn | Phiếu mượn được xác nhận | Hệ thống (khi thủ thư xác nhận phiếu) |
| Đang mượn | Sẵn có | Trả sách, tình trạng sử dụng được | Thủ thư |
| Đang mượn | Hư hỏng | Trả sách, tình trạng không sử dụng được | Thủ thư |
| Đang mượn | Mất | Ghi nhận độc giả làm mất | Thủ thư |
| Đang mượn | Sẵn có | Hủy phiếu mượn lập sai (BR-05-16) | Thủ thư |
| Sẵn có | Hư hỏng | Phát hiện hư hỏng tại kho | Thủ thư |
| Sẵn có | Mất | Không tìm thấy tại kho | Thủ thư |
| Hư hỏng | Sẵn có | Đã sửa chữa xong | Thủ thư |
| Mất | Sẵn có | Tìm thấy lại | Thủ thư |
| Sẵn có, Hư hỏng, Mất | Đã thanh lý | Thanh lý | Thủ thư |

Mọi chuyển đổi không có trong bảng đều bị từ chối.

### 2.4. Các trạng thái khác

| Đối tượng | Trạng thái | Ghi chú |
|---|---|---|
| Đầu sách | Đang lưu hành, Ngừng lưu hành | Có thể chuyển qua lại (BR-02-11). |
| Hồ sơ độc giả | Hoạt động, Đình chỉ, Hết hiệu lực | Chỉ trạng thái Hoạt động được mượn sách. Thủ thư chuyển trạng thái thủ công (BP-10). |
| Tài khoản | Chưa kích hoạt, Hoạt động, Bị khóa | Chỉ trạng thái Hoạt động được đăng nhập. |
| Phiếu mượn | Đang mượn, Hoàn tất, Đã hủy | Hoàn tất khi mọi lượt mượn đã được xử lý (BR-06-10). Đã hủy khi phiếu bị hủy do lập sai (BR-05-16). |
| Lượt mượn | Đang mượn, Đã trả, Đã ghi nhận mất, Đã hủy, Đã chuyển | Lượt mượn Đã trả có thêm thuộc tính đúng hạn hoặc quá hạn. Lượt mượn chỉ Đã hủy cùng với phiếu mượn. Đã chuyển khi lượt mượn được chuyển sang đúng độc giả (BR-05-19). |

## 3. Quy tắc nghiệp vụ

### BR-01 — Tài khoản và phân quyền

| ID | Quy tắc nghiệp vụ |
|---|---|
| BR-01-01 | Mỗi tài khoản phải có mã định danh duy nhất. |
| BR-01-02 | Email đăng nhập không được trùng lặp giữa các tài khoản. |
| BR-01-03 | Người dùng chỉ được thực hiện các nghiệp vụ thuộc quyền hạn của vai trò được cấp (mục 2.2). Quyền được kiểm tra ở mọi yêu cầu, không chỉ ở giao diện. |
| BR-01-04 | Tài khoản bị khóa hoặc chưa kích hoạt không được phép đăng nhập. |
| BR-01-05 | Chỉ quản trị viên được tạo tài khoản nhân viên (thủ thư, quản trị viên) và thay đổi vai trò của tài khoản nhân viên. |
| BR-01-06 | Việc khóa tài khoản không được làm mất lịch sử giao dịch. |
| BR-01-07 | Tài khoản đăng nhập và hồ sơ độc giả là hai đối tượng nghiệp vụ riêng biệt. |
| BR-01-08 | Mỗi tài khoản có đúng một vai trò. Người vừa là nhân viên vừa là độc giả phải dùng hai tài khoản với hai email khác nhau. |
| BR-01-09 | Tài khoản độc giả do thủ thư tạo cho một hồ sơ độc giả có email, luôn có vai trò Độc giả và liên kết với đúng một hồ sơ độc giả. Mỗi hồ sơ độc giả liên kết với tối đa một tài khoản. Vai trò của tài khoản độc giả không được thay đổi. |
| BR-01-10 | Email đăng nhập của tài khoản độc giả luôn là email trong hồ sơ độc giả liên kết. Thay đổi email trong hồ sơ làm thay đổi email đăng nhập. |
| BR-01-11 | Mọi tài khoản mới ở trạng thái Chưa kích hoạt và chỉ được kích hoạt khi người dùng mở liên kết kích hoạt gửi đến email của tài khoản và tự đặt mật khẩu. Không ai khác được biết hoặc đặt mật khẩu của người dùng. |
| BR-01-12 | Hệ thống phải luôn có ít nhất một tài khoản quản trị viên ở trạng thái Hoạt động. Không được khóa hoặc đổi vai trò tài khoản quản trị viên hoạt động cuối cùng. |
| BR-01-13 | Người vận hành chỉ được dùng công cụ vận hành khi hệ thống chưa có tài khoản quản trị viên nào ở trạng thái Hoạt động. Khi đó, công cụ tạo tài khoản quản trị viên đầu tiên ở trạng thái Chưa kích hoạt (kích hoạt theo BR-01-11). Liên kết kích hoạt chỉ được gửi tới email của tài khoản; công cụ không hiển thị, ghi nhật ký hay trả về liên kết cho người vận hành. Công cụ từ chối chạy nếu dịch vụ email chưa được cấu hình. Nếu tài khoản quản trị viên đầu tiên đã tồn tại nhưng còn Chưa kích hoạt, chạy lại công cụ sẽ cấp liên kết kích hoạt mới cho chính tài khoản đó (và cập nhật email nếu người vận hành nhập email khác, áp dụng BR-01-14), không tạo tài khoản thứ hai. Khi đã có quản trị viên Hoạt động, công cụ từ chối thực hiện. |
| BR-01-14 | Khi email của một tài khoản thay đổi, mọi liên kết kích hoạt và liên kết khôi phục mật khẩu chưa được sử dụng của tài khoản đó bị vô hiệu ngay. Nếu tài khoản đang Chưa kích hoạt, hệ thống gửi liên kết kích hoạt mới tới email mới. |

### BR-02 — Danh mục sách

| ID | Quy tắc nghiệp vụ |
|---|---|
| BR-02-01 | Mỗi đầu sách phải có mã định danh duy nhất trong hệ thống. |
| BR-02-02 | Mỗi đầu sách phải có tên sách. |
| BR-02-03 | Một đầu sách có thể có nhiều tác giả. |
| BR-02-04 | Một đầu sách có thể thuộc nhiều thể loại. |
| BR-02-05 | Các phiên bản xuất bản khác nhau của cùng một tác phẩm có thể được quản lý thành các đầu sách riêng biệt. |
| BR-02-06 | ISBN không được sử dụng làm mã định danh cho từng bản sách vật lý. |
| BR-02-07 | Không được xóa đầu sách nếu còn bản sách hoặc lịch sử giao dịch liên quan. Đầu sách chưa có bản sách và giao dịch nào thì được phép xóa. |
| BR-02-08 | Đầu sách đã ngừng lưu hành không được sử dụng để tạo giao dịch mượn mới. |
| BR-02-09 | Không được xóa tác giả, thể loại hoặc nhà xuất bản đang được gắn với ít nhất một đầu sách. |
| BR-02-10 | Tên thể loại không được trùng lặp. |
| BR-02-11 | Đầu sách ngừng lưu hành có thể được khôi phục về trạng thái đang lưu hành. |
| BR-02-12 | ISBN là thông tin không bắt buộc. Nếu được nhập, ISBN phải đúng định dạng ISBN-10 hoặc ISBN-13, kể cả số kiểm tra. |
| BR-02-13 | ISBN không được trùng giữa các đầu sách. |

### BR-03 — Kho sách

| ID | Quy tắc nghiệp vụ |
|---|---|
| BR-03-01 | Một đầu sách có thể có nhiều bản sách vật lý. |
| BR-03-02 | Một bản sách vật lý chỉ thuộc về một đầu sách và không được chuyển sang đầu sách khác. |
| BR-03-03 | Mỗi bản sách vật lý phải có mã quản lý duy nhất. |
| BR-03-04 | Mỗi bản sách chưa thanh lý phải có vị trí lưu trữ được xác định. |
| BR-03-05 | Một bản sách chỉ được tồn tại trong tối đa một lượt mượn đang hiệu lực. |
| BR-03-06 | Bản sách bị mất, hư hỏng hoặc đã thanh lý không được phép cho mượn. |
| BR-03-07 | Số bản sách sẵn có của một đầu sách là số bản sách ở trạng thái Sẵn có. Số bản sách có thể mượn là số bản sách đủ điều kiện cho mượn (BR-03-11). Cả hai số được tính từ trạng thái thực tế của bản sách, không được nhập tay. |
| BR-03-08 | Số lượng bản sách sẵn có và có thể mượn không được nhỏ hơn 0. |
| BR-03-09 | Không được thanh lý bản sách đang thuộc một lượt mượn đang hiệu lực. |
| BR-03-10 | Việc thanh lý bản sách không được làm mất lịch sử mượn trả. |
| BR-03-11 | Một bản sách **đủ điều kiện cho mượn** khi và chỉ khi: (a) bản sách ở trạng thái Sẵn có, và (b) đầu sách của bản sách đang lưu hành. Định nghĩa này được dùng thống nhất khi xác nhận phiếu mượn, hiển thị số lượng có thể mượn và lập báo cáo. |
| BR-03-12 | Trạng thái bản sách chỉ được thay đổi theo các chuyển đổi hợp lệ tại mục 2.3. |
| BR-03-13 | Đã thanh lý là trạng thái cuối. Bản sách đã thanh lý không được chuyển sang trạng thái khác. |
| BR-03-14 | Bản sách hư hỏng đã được sửa chữa hoặc bản sách mất được tìm thấy lại có thể được chuyển về trạng thái Sẵn có. Lịch sử trạng thái trước đó được giữ nguyên. |
| BR-03-15 | Mỗi thay đổi trạng thái bản sách phải ghi nhận người thực hiện, thời điểm và lý do (bắt buộc với thay đổi thủ công). |

### BR-04 — Độc giả

| ID | Quy tắc nghiệp vụ |
|---|---|
| BR-04-01 | Mỗi độc giả phải có mã thành viên duy nhất. |
| BR-04-02 | Chỉ độc giả có trạng thái Hoạt động mới được phép mượn sách. |
| BR-04-03 | Độc giả bị đình chỉ hoặc hết hiệu lực không được tạo giao dịch mượn mới. |
| BR-04-04 | Độc giả bị đình chỉ hoặc hết hiệu lực vẫn được phép trả sách đang mượn. |
| BR-04-05 | Không được xóa hồ sơ độc giả nếu còn lịch sử giao dịch cần lưu giữ. |
| BR-04-06 | Việc thay đổi trạng thái thành viên không làm mất các nghĩa vụ mượn trả hiện tại. |
| BR-04-07 | Độc giả chỉ được truy cập thông tin và lịch sử giao dịch của hồ sơ độc giả liên kết với tài khoản của mình. |
| BR-04-08 | Mỗi thay đổi trạng thái thành viên phải ghi nhận người thực hiện, thời điểm và lý do. |
| BR-04-09 | Mã thành viên do hệ thống cấp khi tạo hồ sơ và không được thay đổi. |
| BR-04-10 | Độc giả không được tự thay đổi email, mã thành viên và trạng thái thành viên. Các thay đổi này do thủ thư thực hiện. |
| BR-04-11 | Email trong hồ sơ độc giả là không bắt buộc. Nếu được nhập, email không được trùng với email của hồ sơ độc giả khác hoặc của bất kỳ tài khoản nào khác. |

### BR-05 — Mượn sách

| ID | Quy tắc nghiệp vụ |
|---|---|
| BR-05-01 | Chỉ thủ thư mới được xác nhận giao dịch mượn sách. |
| BR-05-02 | Mỗi phiếu mượn chỉ thuộc về một độc giả. |
| BR-05-03 | Một phiếu mượn phải chứa ít nhất một bản sách. |
| BR-05-04 | Chỉ bản sách đủ điều kiện cho mượn (BR-03-11) mới được đưa vào phiếu mượn. |
| BR-05-05 | Tổng số lượt mượn đang hiệu lực của độc giả sau khi xác nhận phiếu không được vượt quá giới hạn (BP-01). Lượt mượn đã trả hoặc đã ghi nhận mất không được tính. |
| BR-05-06 | Độc giả có lượt mượn đang quá hạn không được mượn thêm sách. |
| BR-05-07 | Thời hạn trả là hết ngày (23:59:59) của ngày mượn cộng thêm số ngày theo chính sách thời hạn mượn (BP-02) có hiệu lực tại thời điểm mượn. |
| BR-05-08 | Thời hạn trả sách phải sau thời điểm mượn sách. |
| BR-05-09 | Một bản sách không được xuất hiện nhiều lần trong cùng một phiếu mượn. |
| BR-05-10 | Sau khi giao dịch mượn thành công, bản sách phải chuyển sang trạng thái Đang mượn. |
| BR-05-11 | Giao dịch mượn phải ghi nhận độc giả, thủ thư, bản sách, ngày mượn và thời hạn trả. |
| BR-05-12 | Việc thay đổi chính sách mượn sách không được tự động thay đổi thời hạn trả của các giao dịch đã xác nhận trước đó. |
| BR-05-13 | Phiếu mượn được xác nhận toàn bộ hoặc bị từ chối toàn bộ. Không xác nhận một phần phiếu. |
| BR-05-14 | Ngày mượn là thời điểm hệ thống xác nhận phiếu mượn. Thủ thư không được nhập hoặc sửa ngày mượn. |
| BR-05-15 | Phiếu mượn đã xác nhận không được sửa hoặc xóa, thời hạn trả không được thay đổi (MVP không hỗ trợ gia hạn — BP-05). Sai sót khi lập phiếu được xử lý như sau: lập sai độc giả thì chuyển phiếu sang đúng độc giả (BR-05-19); lập sai bản sách hoặc giao dịch không diễn ra thì hủy phiếu (BR-05-16) và lập phiếu mới nếu cần. |
| BR-05-16 | Thủ thư được hủy một phiếu mượn đã xác nhận do lập sai bản sách hoặc do giao dịch không diễn ra (độc giả không nhận sách), khi chưa có lượt mượn nào trong phiếu được trả hoặc ghi nhận mất. Việc hủy áp dụng cho toàn bộ phiếu, bắt buộc có lý do, chuyển phiếu và các lượt mượn sang Đã hủy, và đưa các bản sách về trạng thái Sẵn có. Phiếu đã hủy không bị xóa. Phiếu đã có lượt được xử lý thì không được hủy. |
| BR-05-17 | Phiếu mượn và lượt mượn đã hủy không được tính vào giới hạn mượn, sách quá hạn và báo cáo mượn trả, và không hiển thị trong lịch sử mà độc giả xem được. Thủ thư và quản trị viên vẫn xem được phiếu đã hủy kèm lý do và người hủy. |
| BR-05-18 | **Giới hạn của MVP:** lượt mượn đã được trả hoặc ghi nhận mất không được hủy, chuyển hoặc hiệu chỉnh. Lượt đó giữ nguyên dữ liệu và vẫn được tính trong báo cáo cho độc giả ghi trên phiếu gốc. Chức năng hiệu chỉnh lượt mượn đã xử lý nằm ngoài MVP. |
| BR-05-19 | Khi phiếu mượn lập sai độc giả, thủ thư chuyển mọi lượt mượn còn ở trạng thái Đang mượn của phiếu sang đúng độc giả. Thao tác được thực hiện trong một giao dịch: chuyển các lượt đó sang Đã chuyển, tạo phiếu mới cho đúng độc giả với đúng các bản sách đó, cùng ngày mượn và thời hạn trả như phiếu gốc, liên kết hai phiếu, ghi nhận người thực hiện và lý do (bắt buộc). Bản sách giữ trạng thái Đang mượn trong suốt quá trình. Vì thao tác chỉ ghi nhận việc sách đã ở tay độc giả, hệ thống không áp dụng kiểm tra điều kiện mượn (BR-04-02, BR-04-03, BR-05-05, BR-05-06) mà chỉ hiển thị cảnh báo nếu độc giả mới không đủ điều kiện. Lượt mượn Đã chuyển không tính vào giới hạn mượn, sách quá hạn, báo cáo mượn trả, và không hiển thị trong lịch sử mà độc giả ban đầu xem được. |

### BR-06 — Trả sách

| ID | Quy tắc nghiệp vụ |
|---|---|
| BR-06-01 | Chỉ thủ thư mới được xác nhận giao dịch trả sách. |
| BR-06-02 | Chỉ bản sách thuộc một lượt mượn đang hiệu lực mới được phép ghi nhận trả sách. |
| BR-06-03 | Một lượt mượn chỉ được xác nhận trả thành công một lần. |
| BR-06-04 | Ngày trả sách thực tế không được trước ngày mượn sách. |
| BR-06-05 | Lượt mượn là quá hạn nếu thời điểm trả (hoặc thời điểm hiện tại, với lượt mượn chưa trả) sau thời hạn trả (BR-05-07). Số ngày quá hạn là số ngày lịch tính từ ngày hạn trả đến ngày trả (hoặc ngày hiện tại). |
| BR-06-06 | Độc giả được phép trả từng bản sách trong một phiếu mượn. |
| BR-06-07 | Bản sách được trả trong tình trạng có thể sử dụng sẽ chuyển về trạng thái Sẵn có. |
| BR-06-08 | Bản sách được trả trong tình trạng không thể sử dụng phải được chuyển sang trạng thái Hư hỏng. |
| BR-06-09 | Bản sách được xác nhận bị mất phải chuyển sang trạng thái Mất và không được tính vào số lượng sách sẵn có. |
| BR-06-10 | Phiếu mượn chỉ được hoàn tất khi tất cả lượt mượn trong phiếu đã được trả, đã được ghi nhận mất hoặc đã được chuyển (BR-05-19). |
| BR-06-11 | Giao dịch trả sách phải ghi nhận thủ thư, bản sách, ngày trả và tình trạng sách khi trả (Sử dụng được hoặc Hư hỏng, kèm mô tả tùy chọn). |
| BR-06-12 | Trong MVP, hệ thống chỉ ghi nhận trạng thái mất hoặc hư hỏng và mô tả. Việc bồi thường được xử lý ngoài hệ thống (BP-08, BP-09). |
| BR-06-13 | Ngày trả là thời điểm hệ thống xác nhận trả sách. Thủ thư không được nhập hoặc sửa ngày trả. |
| BR-06-14 | Lượt mượn đã ghi nhận mất được coi là đã xử lý: không còn tính vào giới hạn mượn (BR-05-05) và không còn được coi là đang quá hạn (BR-05-06). |

### BR-07 — Tra cứu sách

| ID | Quy tắc nghiệp vụ |
|---|---|
| BR-07-01 | Độc giả chỉ được tra cứu các đầu sách đang lưu hành. |
| BR-07-02 | Đầu sách đang lưu hành nhưng không còn bản sách có thể mượn vẫn được hiển thị trong kết quả tra cứu. |
| BR-07-03 | Thủ thư và quản trị viên được tra cứu cả các đầu sách đã ngừng lưu hành. |
| BR-07-04 | Thông tin tra cứu không được tiết lộ danh tính của độc giả đang mượn sách. |
| BR-07-05 | Số lượng có thể mượn hiển thị khi tra cứu được xác định theo BR-03-11. |
| BR-07-06 | Trong MVP, chỉ người dùng đã đăng nhập mới được tra cứu sách (BP-11). |

### BR-08 — Báo cáo và thống kê

| ID | Quy tắc nghiệp vụ |
|---|---|
| BR-08-01 | Số lượng đầu sách và số lượng bản sách vật lý phải được thống kê riêng biệt. |
| BR-08-02 | Báo cáo mượn trả chỉ tính các giao dịch đã được xác nhận thành công; không tính phiếu mượn đã hủy (BR-05-17) và lượt mượn đã chuyển (BR-05-19). |
| BR-08-03 | Sách đang mượn quá hạn là lượt mượn ở trạng thái Đang mượn và đã vượt quá thời hạn trả. |
| BR-08-04 | Sách đã trả quá hạn và sách đang mượn quá hạn phải được thống kê riêng biệt. |
| BR-08-05 | Số lượt mượn sách được tính theo số lượt mượn của từng bản sách, không phải số lượng phiếu mượn. |
| BR-08-06 | Chỉ thủ thư và quản trị viên được xem báo cáo. Độc giả không được truy cập báo cáo. |
| BR-08-07 | Việc ngừng lưu hành hoặc thanh lý sách không được làm thay đổi số liệu giao dịch lịch sử đã phát sinh. |
| BR-08-08 | Các mốc thời gian trong báo cáo được tính theo múi giờ của thư viện (BP-12). |

## 4. Chính sách nghiệp vụ (Business Policies)

| ID | Chính sách | Giá trị cho MVP | Ghi chú |
|---|---|---|---|
| BP-01 | Số lượng bản sách được mượn đồng thời | 5 bản | Quản trị viên cấu hình được (FR-09). |
| BP-02 | Thời hạn mượn sách | 14 ngày | Quản trị viên cấu hình được (FR-09). |
| BP-03 | Cho phép mượn khi có sách quá hạn | Không | |
| BP-04 | Cho phép trả sách từng phần | Có | |
| BP-05 | Gia hạn mượn sách | Không hỗ trợ trong MVP | |
| BP-06 | Đặt trước sách | Không hỗ trợ trong MVP | |
| BP-07 | Tiền phạt quá hạn | Không hỗ trợ trong MVP | |
| BP-08 | Xử lý sách bị mất | Ghi nhận trạng thái Mất; bồi thường xử lý ngoài hệ thống | |
| BP-09 | Xử lý sách hư hỏng | Ghi nhận trạng thái Hư hỏng; bồi thường xử lý ngoài hệ thống | |
| BP-10 | Thời hạn thành viên | Không tự động hết hạn; thủ thư chuyển trạng thái thủ công | |
| BP-11 | Tra cứu sách không cần đăng nhập | Không hỗ trợ trong MVP | |
| BP-12 | Múi giờ nghiệp vụ | UTC+7 (Asia/Ho_Chi_Minh) | |

Giá trị của BP-01, BP-02, BP-08, BP-09 và BP-10 là đề xuất cho MVP và cần được bên nghiệp vụ của thư viện xác nhận trước khi nghiệm thu.

## 5. Nguyên tắc quản lý quy tắc nghiệp vụ

- Mỗi quy tắc nghiệp vụ phải có mã định danh duy nhất.
- Quy tắc nghiệp vụ phải rõ ràng và có thể kiểm chứng.
- Quy tắc nghiệp vụ không được mâu thuẫn với nhau.
- Quy tắc nghiệp vụ phải có khả năng đối chiếu với Functional Requirements.
- Những thay đổi về chính sách nghiệp vụ phải được ghi nhận.
- Các quy tắc nghiệp vụ quan trọng phải được kiểm thử tự động (NFR-06-01).
