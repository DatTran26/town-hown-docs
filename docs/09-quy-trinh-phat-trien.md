# 9. Quy trình phát triển

Mọi thay đổi trên nhánh `develop` được triển khai lên
<https://staging.wpcteam.shop/>.

## GitFlow

```text
develop-dat | develop-hieu | develop-kien | develop-thanh
    ->  PR  ->  develop  ->  release/x.y.z  ->  main
```

- Nhánh cá nhân và `feature/<slug>` chỉ PR vào `develop`, không vào `main`.
- `release/x.y.z` cắt từ `develop` rồi merge vào `main`.
- Hotfix bắt đầu từ `main`.
- Không force-push `main` hoặc `develop`.
- Commit theo Conventional Commits, tiếng Anh, mỗi commit một mục đích.

## Quy tắc code

### TypeScript
- Giữ `strict: true`; dữ liệu chưa biết bắt đầu từ `unknown`, không dùng `any`
  để bỏ qua validate.
- Import từ `src` dùng alias `@/*`.
- File mới ưu tiên kebab-case.

### React / Next.js
- Server Component là mặc định; `use client` chỉ khi cần tương tác.
- Dữ liệu nhạy cảm được lọc ở server; không đẩy cả bản ghi xuống client.
- Tái sử dụng component UI có sẵn trước khi tạo mới.
- UI có trạng thái loading, rỗng, lỗi, hỗ trợ bàn phím và responsive.

### API
Thứ tự: parse input → xác định auth → kiểm tra vai trò/sở hữu/phạm vi → gọi
domain → trả response không lộ nội bộ → ghi audit nếu cần.

### Cơ sở dữ liệu
- Dùng đúng client browser/server/admin.
- Thay đổi schema, RLS, index, function phải qua migration mới.
- Truy vấn danh sách có filter, phạm vi và phân trang.

### AI, email và file
- Phản hồi AI được parse, validate, có timeout và đường xử lý lỗi.
- Credential SMTP và AI key chỉ ở server.
- Kiểm tra loại file, kích thước, quyền truy cập tại biên.

## Pattern bắt buộc

- Chuyển trạng thái tuyển dụng đi qua state machine dùng chung.
- Optimistic UI phải rollback được; không dùng cho quyết định quan trọng.
- Điểm suy diễn được tính lại từ dữ liệu nguồn.
- Xuất CSV/PDF chỉ chứa trường đã được phân quyền và escape dữ liệu người dùng.

## Kiểm tra

```bash
npm run lint
npm run build
npm run test:report   # test báo cáo tuyển dụng và xuất Excel
```

Thứ tự kiểm tra:

1. Kiểm tra hẹp nhất cho hành vi thay đổi.
2. Lint.
3. Build khi hợp đồng dùng chung thay đổi.
4. API: thành công, input lỗi, chưa đăng nhập, không đủ quyền, đúng chủ sở hữu.
5. UI: loading/rỗng/lỗi, bàn phím, responsive.
6. Migration: áp dụng trên staging, kiểm tra RLS và rollback.
7. AI provider: output lỗi, timeout, lỗi một phần, log đã che.

## Checklist review

- Thay đổi đúng nơi sở hữu và đúng phạm vi chưa?
- Input, auth, phân quyền đã được kiểm ở server và dữ liệu chưa?
- Client, log, file xuất có lộ secret hoặc dữ liệu thừa không?
- Thay đổi schema có migration, backup, RLS và kế hoạch phục hồi chưa?
- Lỗi AI có an toàn và có đường review không?
- Tài liệu người dùng, cài đặt hay bảo mật có cần cập nhật không?

## Quy trình đặc tả tính năng

```text
PRD -> brainstorm -> URD -> SRS -> ERD -> triển khai -> kiểm thử
```

Mã yêu cầu dùng tiền tố theo tính năng: `FR-`, `NFR-`, `BR-`, `E-`, `SC-`. Xem
[quy ước đặc tả](features/README.md).
