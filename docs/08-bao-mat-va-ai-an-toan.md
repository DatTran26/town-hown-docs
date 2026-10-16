# 8. Bảo mật và AI an toàn

Áp dụng cho mọi môi trường, bao gồm <https://staging.wpcteam.shop/>.

## Tài sản cần bảo vệ

Hồ sơ nhân viên và ứng viên, CV, bài đánh giá, transcript, bản ghi âm, dữ liệu
khuôn mặt, email, tài liệu tổ chức và các quyết định tác động đến con người. Mô
hình bảo mật ưu tiên tính bí mật, phân quyền theo phạm vi, provenance, khả năng
audit và bước review của con người.

## Dữ liệu không tin cậy

- Request body, params, query và token public.
- Trạng thái phía trình duyệt.
- File upload, CV, âm thanh/video, transcript, ảnh khuôn mặt.
- Phản hồi từ AI provider.
- Biến trong mẫu email và payload webhook.

Luồng xử lý chuẩn:

```text
input chưa biết -> parse/validate -> phân quyền -> hành động domain
                -> lưu / audit -> response tối thiểu
```

## Định danh và phân quyền

1. Middleware chỉ bảo vệ route và session, không thay thế phân quyền.
2. API kiểm tra danh tính, vai trò, quyền sở hữu và phạm vi cho từng hành động.
3. RLS là lớp bảo vệ dữ liệu cuối khi truy cập bằng client của người dùng.
4. Service role chỉ dùng ở server cho hành động đã được phân quyền cụ thể.
5. Token bài đánh giá public chỉ cấp quyền tối thiểu cho đúng tài nguyên chia sẻ.
6. Xuất file, báo cáo và thông báo áp cùng phạm vi quyền với màn hình nguồn.
7. Thao tác quản trị nhạy cảm có thể yêu cầu xác thực lại bằng khuôn mặt.
8. Đăng nhập được bảo vệ bằng CAPTCHA Cloudflare Turnstile.

Không dựa vào việc ẩn nút, route khó đoán hay UUID để bảo vệ dữ liệu.

## Quản lý secret

- Không commit `.env*`, API key, service-role key, mật khẩu SMTP, khóa SSH hay
  credential cơ sở dữ liệu.
- Không đặt secret trong biến `NEXT_PUBLIC_*`.
- Không log, chụp màn hình hay đưa secret vào tài liệu và test fixture.
- Mật khẩu SMTP được mã hóa trước khi lưu.
- Khi nghi ngờ lộ secret: thu hồi và xoay vòng trước, điều tra sau.

## Dữ liệu nhạy cảm

| Nhóm | Rủi ro | Biện pháp |
| --- | --- | --- |
| Hồ sơ nhân viên/ứng viên | Lộ PII, dùng sai mục đích | Quyền tối thiểu, giới hạn mục đích, audit |
| CV/tài liệu | Mã độc, OCR sai, lưu quá lâu | Kiểm tra file, review kết quả, chính sách lưu giữ |
| Bài đánh giá/điểm | Phân biệt đối xử, lộ đáp án | Evidence, reviewer override, giới hạn xuất |
| Ghi âm/transcript | Thu thập không đồng ý | Đồng ý rõ ràng, kiểm soát truy cập và xóa |
| Dữ liệu khuôn mặt | Giả mạo, lạm dụng sinh trắc | Chống giả mạo, lưu embedding thay vì ảnh, quyền xóa |
| Camera giám sát | Giám sát xâm phạm riêng tư | Chỉ khu vực đã công bố, quản lý xác nhận, giới hạn lưu giữ |
| Email/thông báo | Gửi nhầm người, lộ ngữ cảnh | Kiểm tra người nhận, nội dung tối thiểu, nhật ký |

## Nguyên tắc AI an toàn

- AI chỉ hỗ trợ trích xuất, đề xuất, chấm điểm, tóm tắt và soạn thảo.
- AI không tự tuyển, loại, kỷ luật hay kết luận phẩm chất con người.
- Output có cấu trúc phải được parse và validate; output lỗi có đường xử lý riêng.
- Nhận định quan trọng phải trỏ về evidence nguồn khi có thể.
- Người có thẩm quyền review và override; override có lý do và audit.
- Chỉ gửi dữ liệu tối thiểu cần thiết tới AI provider.
- JSON hợp lệ không có nghĩa là nội dung đúng.

## Log và audit

- **Log vận hành:** request, hành động, kết quả, thời gian; che secret và PII.
- **Audit:** người thực hiện, đối tượng, trước/sau, lý do, thời điểm.
- **AI usage:** mô hình, tính năng, mức dùng; mặc định không lưu prompt mật.
- **Nhật ký email:** người nhận, trạng thái, mẫu; giới hạn nội dung nhạy cảm.

## Báo cáo lỗ hổng

Vui lòng không mở issue công khai cho lỗ hổng chưa được vá. Hãy dùng tính năng
private vulnerability reporting của GitHub hoặc liên hệ trực tiếp maintainer,
kèm mô tả tác động, phạm vi và các bước tái hiện tối thiểu. Không gửi secret hay
dữ liệu cá nhân thật trong báo cáo.
