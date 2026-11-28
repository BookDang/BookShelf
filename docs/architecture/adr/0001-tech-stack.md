# ADR-0001: Bộ công nghệ cho MVP

- **Trạng thái:** Đã chấp nhận
- **Ngày:** 28/11/2026
- **Issue:** #11

## Bối cảnh

- Nhóm phát triển gồm 2 người, quen với hệ sinh thái JavaScript/TypeScript, làm ngoài giờ.
- Mục tiêu hoàn thành MVP trong khoảng 1 tháng (8 sprint, mục tiêu 3 ngày mỗi sprint — xem [project-status.md](../../project-status.md)).
- Hệ thống triển khai trên VPS do nhóm tự quản lý.
- Các yêu cầu ảnh hưởng trực tiếp tới lựa chọn công nghệ:

| Yêu cầu | Nội dung | Ảnh hưởng |
|---|---|---|
| NFR-04-03, NFR-04-04 | Giao dịch mượn trả trọn vẹn; không cho mượn trùng một bản sách khi thao tác đồng thời | Cơ sở dữ liệu cần giao dịch và khóa dòng |
| NFR-10-01, NFR-10-05 | Ràng buộc duy nhất và khóa ngoại ở tầng lưu trữ | Cơ sở dữ liệu quan hệ |
| FR mục 4.10 | Tìm kiếm không phân biệt hoa thường và không phân biệt dấu tiếng Việt | Collation hoặc cách chuẩn hóa dữ liệu tìm kiếm |
| NFR-05-06 | HTTPS với TLS 1.2 trở lên | Reverse proxy có TLS |
| NFR-05-07 | Kiểm tra quyền ở phía máy chủ cho mọi yêu cầu | Backend có cơ chế phân quyền dùng chung |
| NFR-01-05, NFR-03-01 | 200 người dùng đồng thời; sẵn sàng 99,5% | Một máy chủ đủ đáp ứng; không cần kiến trúc phân tán |
| NFR-06-05 | Lập trình viên mới chạy được hệ thống trong 30 phút | Môi trường phát triển đóng gói, tái tạo được |
| NFR-03-02 | Khôi phục hoạt động sau sự cố | Ứng dụng tự khởi động lại khi lỗi hoặc khi máy chủ khởi động lại |

## Quyết định

| Thành phần | Lựa chọn | Phiên bản | Vai trò |
|---|---|---|---|
| Ngôn ngữ | TypeScript | Phiên bản được Next.js và NestJS hỗ trợ chính thức; chốt trong #16 | Dùng chung cho frontend, backend và gói dùng chung |
| Môi trường chạy | Node.js | **26 LTS** (Lithium) | Chạy Next.js, NestJS và công cụ |
| Frontend | Next.js | **16.x** (React 19) | Giao diện cho nhân viên và độc giả |
| Backend | NestJS | **12.x** | API, xác thực, phân quyền, nghiệp vụ |
| Cơ sở dữ liệu | PostgreSQL (mã hóa `UTF8`; extension `unaccent`, `pg_trgm`) | **18**, bản vá (minor) mới nhất khi cài đặt (18.7 tại ngày quyết định) | Lưu trữ dữ liệu nghiệp vụ |
| Reverse proxy | nginx | Nhánh **stable** mới nhất | HTTPS; định tuyến cùng một tên miền: `/` → Next.js, `/api` → NestJS |
| Quản lý gói | pnpm (workspace) | **12.x** | Quản lý monorepo `apps/web`, `apps/api`, `packages/shared` |
| Môi trường phát triển | Docker, Docker Compose | Bản ổn định mới nhất | **Chỉ dùng trên máy phát triển:** chạy PostgreSQL, Mailpit (hứng email) và các dịch vụ phụ trợ bằng container |
| Môi trường kiểm thử và môi trường thật | Cài trực tiếp trên VPS, **không dùng Docker** | Cùng phiên bản với bảng trên | Node.js, PostgreSQL và nginx chạy như dịch vụ của hệ điều hành; Next.js và NestJS chạy dưới trình quản lý tiến trình (systemd hoặc PM2, chốt trong #18) để tự khởi động lại |
| Hạ tầng | VPS tự quản lý | — | Môi trường kiểm thử và môi trường thật |

**Chính sách phiên bản:**

- Ghi cố định phiên bản chính (major) trong `package.json`; cho phép cập nhật bản vá (patch) và bản nhỏ (minor) sau khi CI chạy qua.
- Image Docker ở môi trường phát triển (PostgreSQL, Node.js) phải cùng phiên bản chính với bản cài trên VPS, để tránh lệch hành vi giữa máy phát triển và môi trường thật.
- Node.js luôn dùng dòng **LTS**.
- PostgreSQL dùng một phiên bản chính còn trong thời hạn hỗ trợ (mỗi phiên bản chính được hỗ trợ 5 năm) và cập nhật bản vá hằng quý. Chỉ chuyển sang phiên bản chính mới khi đã có ít nhất bản vá thứ hai (ví dụ 19.2) và ORM, extension đang dùng đã hỗ trợ.
- Nâng phiên bản chính của bất kỳ thành phần nào phải có issue riêng; nếu ảnh hưởng tới kiến trúc thì viết ADR mới.

**Ngoài phạm vi ADR này** — quyết định trong các issue riêng:

| Nội dung | Issue |
|---|---|
| ORM và công cụ migration | #12 (ADR-0002) |
| Kiến trúc chi tiết, cấu trúc module | #13 |
| Thư viện giao diện | #19 |
| Công cụ kiểm thử | #20 |
| CI và phiên bản TypeScript | #16 |
| Dịch vụ email và tên miền | #21 |
| Hệ điều hành và cấu hình VPS; trình quản lý tiến trình; quy trình triển khai | #18 |

## Lý do

- **TypeScript cho cả hai phía:** nhóm đã quen; kiểu dữ liệu và schema kiểm tra đầu vào dùng chung qua `packages/shared`, giảm lỗi lệch giữa frontend và backend.
- **NestJS:** cấu trúc module rõ ràng, có sẵn dependency injection, guard, pipe, interceptor. Guard dùng chung giúp kiểm tra quyền ở mọi yêu cầu (NFR-05-07); pipe dùng chung giúp kiểm tra dữ liệu đầu vào thống nhất (GEN-01, GEN-03).
- **Next.js:** định tuyến và render phía máy chủ cho hai nhóm giao diện (nhân viên và độc giả) trong cùng một ứng dụng.
- **PostgreSQL 18:**
  - Giao dịch và khóa dòng `SELECT … FOR UPDATE`, đáp ứng NFR-04-03 và NFR-04-04.
  - Ràng buộc duy nhất và khóa ngoại ở tầng dữ liệu (NFR-10-01, NFR-10-05). Có thêm **partial unique index**, ví dụ `UNIQUE (copy_id) WHERE status = 'ON_LOAN'`, để chính cơ sở dữ liệu chặn một bản sách có hai lượt mượn đang hiệu lực (BR-03-05).
  - Extension `unaccent` bỏ dấu tiếng Việt, kể cả chữ "đ"; `pg_trgm` tạo index cho tìm kiếm chứa chuỗi. Đáp ứng tìm kiếm không phân biệt hoa thường và dấu (FR mục 4.10) trong thời gian yêu cầu (NFR-01-02).
  - Lệnh thay đổi cấu trúc (DDL) chạy trong giao dịch: migration lỗi giữa chừng được quay lui toàn bộ, không để cơ sở dữ liệu dở dang (NFR-06-04).
  - Kiểu `timestamptz` lưu thời điểm kèm múi giờ (NFR-10-04).
  - Chọn 18 thay vì 19: bản 19 mới phát hành ngày 19/11/2026 (19.0); bản 18 đã qua nhiều bản vá và được hỗ trợ đến năm 2030.
- **nginx:** reverse proxy phổ biến, tài liệu đầy đủ; đặt cả frontend và API dưới cùng một tên miền nên cookie phiên đăng nhập hoạt động mà không cần cấu hình CORS.
- **VPS tự quản lý:** chi phí thấp, nhóm toàn quyền kiểm soát.
- **Docker chỉ cho môi trường phát triển:** thành viên mới dựng được PostgreSQL và các dịch vụ phụ trợ bằng một lệnh, không phải cài từng thứ (NFR-06-05).
- **Không dùng Docker khi chạy thật:** bớt một tầng trung gian và tài nguyên trên VPS; nhóm vận hành trực tiếp các dịch vụ quen thuộc (Node.js, PostgreSQL, nginx) và xem log, khởi động lại bằng công cụ của hệ điều hành.

## Hệ quả

**Tích cực:**

- Một ngôn ngữ cho toàn bộ hệ thống; hai thành viên có thể hỗ trợ nhau ở cả frontend lẫn backend.
- Đáp ứng các yêu cầu về giao dịch, toàn vẹn dữ liệu và HTTPS bằng công nghệ phổ biến, ít rủi ro.

**Tiêu cực và rủi ro:**

| Rủi ro | Giảm thiểu |
|---|---|
| Hai ứng dụng riêng (Next.js và NestJS) tốn công thiết lập hơn một ứng dụng full-stack, trong khi thời gian chỉ khoảng 1 tháng | Monorepo pnpm và gói dùng chung; dựng khung một lần trong Sprint 0 (#16, #17) |
| Hàm `unaccent` không được khai báo là bất biến (IMMUTABLE) nên không dùng trực tiếp trong biểu thức index | Tạo hàm bọc bất biến hoặc cột tìm kiếm đã chuẩn hóa (bỏ dấu, chữ thường) có index `pg_trgm`; kiểm chứng trong #14 |
| Nhóm cần làm quen vận hành PostgreSQL (cấu hình kết nối, quyền, sao lưu) | ORM che phần lớn khác biệt khi viết mã; ghi hướng dẫn cài đặt và sao lưu trong #18 |
| TypeScript bản mới nhất có thể chưa tương thích hoàn toàn với decorator của NestJS | Chỉ dùng phiên bản TypeScript được NestJS và Next.js hỗ trợ chính thức; chốt và kiểm tra trong #16 |
| Tự quản lý VPS: nhóm chịu trách nhiệm cập nhật bảo mật, sao lưu, theo dõi; một máy chủ duy nhất là điểm lỗi đơn | Sao lưu tự động và diễn tập khôi phục (NFR-11); theo dõi và cảnh báo (NFR-09); mục tiêu sẵn sàng 99,5% đã tính tới một máy chủ |
| Next.js gọi API NestJS phía máy chủ cần chuyển tiếp cookie phiên đăng nhập | Thiết kế luồng xác thực trong #13 |
| Môi trường phát triển (Docker) và môi trường thật (cài trực tiếp) có thể lệch phiên bản hoặc cấu hình, gây lỗi chỉ xuất hiện khi triển khai | Dùng cùng dòng phiên bản; môi trường kiểm thử trên VPS cài giống hệt môi trường thật và được triển khai thử trước mỗi lần phát hành; viết script hoặc tài liệu cài đặt lặp lại được (#18) |
| Không có container nên việc cài đặt và nâng cấp trên VPS phải làm thủ công | Script cài đặt và triển khai có phiên bản trong repo (#18); trình quản lý tiến trình tự khởi động lại ứng dụng (NFR-03-02) |

## Phương án đã cân nhắc

| Phương án | Lý do không chọn |
|---|---|
| Chỉ dùng Next.js full-stack (API routes hoặc server actions) | Ít thành phần hơn, nhưng nhóm chọn NestJS để có backend tách biệt, cấu trúc rõ ràng cho nghiệp vụ mượn trả và phân quyền |
| MySQL 9.7 LTS | Lựa chọn ban đầu, đổi sang PostgreSQL trước khi viết mã. Đáp ứng được giao dịch và toàn vẹn dữ liệu, nhưng không có partial index (ràng buộc BR-03-05 phải dùng cột phụ), DDL tự commit nên migration lỗi có thể để lại cơ sở dữ liệu dở dang, và collation không dấu chưa chắc coi "đ" là "d" |
| PostgreSQL 19 | Mới phát hành 19/11/2026, mới có bản 19.0; chờ bản vá và hỗ trợ của ORM, extension. Nâng cấp sau bằng issue riêng theo chính sách phiên bản |
| Caddy thay cho nginx | Tự cấp HTTPS đơn giản hơn; nhóm chọn nginx vì phổ biến và tài liệu đầy đủ. HTTPS dùng Let's Encrypt với nginx |
| Dùng Docker cho cả môi trường thật | Môi trường giống hệt nhau giữa các nơi chạy; nhóm chọn cài trực tiếp để bớt tầng trung gian và tài nguyên trên VPS, và vận hành bằng công cụ quen thuộc |
| Dịch vụ cloud quản lý sẵn (PaaS) | Giảm công vận hành nhưng chi phí cao hơn và phụ thuộc nhà cung cấp; nhóm chọn VPS tự quản lý |

## Nguồn tra cứu phiên bản (28/11/2026)

- npm registry: `next` 16.4.6, `@nestjs/core` 12.6.3, `pnpm` 12.23.0.
- [Danh sách phát hành Node.js](https://nodejs.org/dist/index.json): v26.13.1 là bản LTS (Lithium) mới nhất.
- [PostgreSQL Versioning Policy](https://www.postgresql.org/support/versioning/): mỗi phiên bản chính được hỗ trợ 5 năm; bản vá ra hằng quý; 18.7 là bản vá mới nhất của dòng 18 (12/11/2026).
- [PostgreSQL 19 Released!](https://www.postgresql.org/about/news/postgresql-19-released-3449/): phát hành ngày 19/11/2026.
