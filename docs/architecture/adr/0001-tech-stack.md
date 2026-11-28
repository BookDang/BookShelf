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
| NFR-06-05 | Lập trình viên mới chạy được hệ thống trong 30 phút | Môi trường đóng gói, tái tạo được |

## Quyết định

| Thành phần | Lựa chọn | Phiên bản | Vai trò |
|---|---|---|---|
| Ngôn ngữ | TypeScript | Phiên bản được Next.js và NestJS hỗ trợ chính thức; chốt trong #16 | Dùng chung cho frontend, backend và gói dùng chung |
| Môi trường chạy | Node.js | **26 LTS** (Lithium) | Chạy Next.js, NestJS và công cụ |
| Frontend | Next.js | **16.x** (React 19) | Giao diện cho nhân viên và độc giả |
| Backend | NestJS | **12.x** | API, xác thực, phân quyền, nghiệp vụ |
| Cơ sở dữ liệu | MySQL (InnoDB, `utf8mb4`) | **9.7 LTS**, bản vá mới nhất khi cài đặt (9.7.4 tại ngày quyết định) | Lưu trữ dữ liệu nghiệp vụ |
| Reverse proxy | nginx | Nhánh **stable** mới nhất | HTTPS; định tuyến cùng một tên miền: `/` → Next.js, `/api` → NestJS |
| Quản lý gói | pnpm (workspace) | **12.x** | Quản lý monorepo `apps/web`, `apps/api`, `packages/shared` |
| Đóng gói và chạy | Docker, Docker Compose | Bản ổn định mới nhất | Môi trường local và VPS giống nhau |
| Hạ tầng | VPS tự quản lý | — | Môi trường kiểm thử và môi trường thật |

**Chính sách phiên bản:**

- Ghi cố định phiên bản chính (major) trong `package.json` và image Docker; cho phép cập nhật bản vá (patch) và bản nhỏ (minor) sau khi CI chạy qua.
- Node.js và MySQL luôn dùng dòng **LTS**. Không dùng dòng MySQL Innovation (26.x) cho môi trường thật vì mỗi bản chỉ được hỗ trợ đến khi có bản kế tiếp.
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
| Hệ điều hành và cấu hình VPS | #18 |

## Lý do

- **TypeScript cho cả hai phía:** nhóm đã quen; kiểu dữ liệu và schema kiểm tra đầu vào dùng chung qua `packages/shared`, giảm lỗi lệch giữa frontend và backend.
- **NestJS:** cấu trúc module rõ ràng, có sẵn dependency injection, guard, pipe, interceptor. Guard dùng chung giúp kiểm tra quyền ở mọi yêu cầu (NFR-05-07); pipe dùng chung giúp kiểm tra dữ liệu đầu vào thống nhất (GEN-01, GEN-03).
- **Next.js:** định tuyến và render phía máy chủ cho hai nhóm giao diện (nhân viên và độc giả) trong cùng một ứng dụng.
- **MySQL 9.7 LTS:**
  - InnoDB hỗ trợ giao dịch và khóa dòng `SELECT … FOR UPDATE`, đáp ứng NFR-04-03 và NFR-04-04.
  - Ràng buộc duy nhất và khóa ngoại ở tầng dữ liệu (NFR-10-01, NFR-10-05).
  - Collation `utf8mb4_0900_ai_ci` không phân biệt hoa thường và dấu, là điểm khởi đầu cho tìm kiếm tiếng Việt (cần kiểm chứng, xem mục Hệ quả).
  - 9.7 là dòng LTS mới nhất, có thời gian hỗ trợ dài.
- **nginx:** reverse proxy phổ biến, tài liệu đầy đủ; đặt cả frontend và API dưới cùng một tên miền nên cookie phiên đăng nhập hoạt động mà không cần cấu hình CORS.
- **VPS và Docker Compose:** chi phí thấp, nhóm toàn quyền kiểm soát; cùng một tệp Compose cho local và VPS nên môi trường tái tạo được (NFR-06-05).

## Hệ quả

**Tích cực:**

- Một ngôn ngữ cho toàn bộ hệ thống; hai thành viên có thể hỗ trợ nhau ở cả frontend lẫn backend.
- Đáp ứng các yêu cầu về giao dịch, toàn vẹn dữ liệu và HTTPS bằng công nghệ phổ biến, ít rủi ro.

**Tiêu cực và rủi ro:**

| Rủi ro | Giảm thiểu |
|---|---|
| Hai ứng dụng riêng (Next.js và NestJS) tốn công thiết lập hơn một ứng dụng full-stack, trong khi thời gian chỉ khoảng 1 tháng | Monorepo pnpm và gói dùng chung; dựng khung một lần trong Sprint 0 (#16, #17) |
| Collation `utf8mb4_0900_ai_ci` có thể không coi "đ" và "d" là như nhau | Kiểm chứng trong #14; nếu không đạt, thêm cột tìm kiếm đã chuẩn hóa (bỏ dấu, đổi "đ" thành "d") |
| TypeScript bản mới nhất có thể chưa tương thích hoàn toàn với decorator của NestJS | Chỉ dùng phiên bản TypeScript được NestJS và Next.js hỗ trợ chính thức; chốt và kiểm tra trong #16 |
| Tự quản lý VPS: nhóm chịu trách nhiệm cập nhật bảo mật, sao lưu, theo dõi; một máy chủ duy nhất là điểm lỗi đơn | Sao lưu tự động và diễn tập khôi phục (NFR-11); theo dõi và cảnh báo (NFR-09); mục tiêu sẵn sàng 99,5% đã tính tới một máy chủ |
| Next.js gọi API NestJS phía máy chủ cần chuyển tiếp cookie phiên đăng nhập | Thiết kế luồng xác thực trong #13 |

## Phương án đã cân nhắc

| Phương án | Lý do không chọn |
|---|---|
| Chỉ dùng Next.js full-stack (API routes hoặc server actions) | Ít thành phần hơn, nhưng nhóm chọn NestJS để có backend tách biệt, cấu trúc rõ ràng cho nghiệp vụ mượn trả và phân quyền |
| PostgreSQL | Có sẵn `unaccent` và `pg_trgm` cho tìm kiếm không dấu; nhóm chọn MySQL. Yêu cầu giao dịch và toàn vẹn dữ liệu đều đáp ứng được với MySQL |
| MySQL 8.4 LTS | Vẫn được hỗ trợ, nhưng 9.7 là dòng LTS mới hơn, thời gian hỗ trợ dài hơn cho dự án mới |
| Caddy thay cho nginx | Tự cấp HTTPS đơn giản hơn; nhóm chọn nginx vì phổ biến và tài liệu đầy đủ. HTTPS dùng Let's Encrypt với nginx |
| Dịch vụ cloud quản lý sẵn (PaaS) | Giảm công vận hành nhưng chi phí cao hơn và phụ thuộc nhà cung cấp; nhóm chọn VPS tự quản lý |

## Nguồn tra cứu phiên bản (28/11/2026)

- npm registry: `next` 16.4.6, `@nestjs/core` 12.6.3, `pnpm` 12.23.0.
- [Danh sách phát hành Node.js](https://nodejs.org/dist/index.json): v26.13.1 là bản LTS (Lithium) mới nhất.
- [MySQL 9.7.0 LTS Is Now Available](https://blogs.oracle.com/mysql/mysql-9-7-0-lts-is-now-available-expanded-community-capabilities-and-dynamic-data-masking-for-enterprise) và [MySQL October 2026 GA Releases](https://blogs.oracle.com/mysql/mysql-october-2026-ga-releases-now-available): 9.7.4 LTS là bản vá mới nhất của dòng 9.7.
- [MySQL Release Models: LTS, Innovation, and Single Release](https://blogs.oracle.com/mysql/mysql-release-models-lts-innovation-and-single-release).
