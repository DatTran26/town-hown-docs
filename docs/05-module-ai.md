# 5. Các module AI

Dùng thử trên <https://staging.wpcteam.shop/> (cần đăng nhập).

Ngoài các tính năng AI trong BFF (phân tích JD, sinh câu hỏi, đánh giá cấp độ,
phân tích kết quả), Town Hown có ba service AI chạy độc lập bằng FastAPI. Web
gọi chúng qua BFF; trình duyệt không gọi trực tiếp.

## 5.1 AI trong ứng dụng web

| Nhóm API | Chức năng |
| --- | --- |
| `/api/ai/analyze-jd` | Phân tích mô tả công việc thành yêu cầu có cấu trúc |
| `/api/ai/generate`, `/api/ai/regenerate` | Sinh câu hỏi đánh giá |
| `/api/ai/generate-followup` | Sinh câu hỏi phỏng vấn bổ sung |
| `/api/ai/evaluate-level` | Đề xuất cấp độ năng lực |
| `/api/ai/analyze`, `/api/ai/analyze-result` | Phân tích bài làm và kết quả |
| `/api/ai/standardize-version` | Chuẩn hóa ghi chú phát hành |
| `/api/recruitment/cv-extract-info`, `/api/recruitment/jd-parse` | Bóc tách CV và JD |

Edge Functions xử lý nền: `cv-processor`, `extract-document-topics`,
`generate-questions-from-doc`. Mỗi lần gọi AI được ghi vào nhật ký sử dụng để
admin theo dõi chi phí.

## 5.2 Vision OCR và Nghị định 30 Studio

Bóc tách văn bản, chữ viết tay và bảng biểu từ ảnh hoặc PDF scan; soạn thảo,
thẩm định và xuất văn bản hành chính theo **Nghị định 30/2020/NĐ-CP**.

- **OCR đa tầng:** Google Gemini Vision, tự động dự phòng sang Pytesseract
  (tiếng Việt `vie` và tiếng Anh `eng`). Có bounding box để đối chiếu từng khối
  văn bản trên ảnh gốc.
- **Trợ lý soạn thảo:** nhận lệnh ngôn ngữ tự nhiên (ví dụ "bổ sung số CCCD
  …") và thay thế đúng vị trí trong văn bản thay vì chèn vào cuối.
- **Chuyển đổi mô hình tự động:** khi gặp giới hạn hạn ngạch (HTTP 429), service
  lần lượt thử các mô hình Gemini dự phòng.
- **Tra cứu pháp lý:** Google Search Grounding để đối chiếu văn bản pháp luật
  hiện hành.
- **Thẩm định thể thức:** kiểm tra 9 thành phần bắt buộc (Quốc hiệu - Tiêu ngữ,
  tên cơ quan, số/ký hiệu, địa danh/thời gian, tên loại/trích yếu, nội dung,
  chức vụ/chữ ký, dấu/chữ ký số, nơi nhận), chấm điểm trên thang 100 kèm khuyến
  nghị.
- **Xem trước A4 và xuất Word (.docx):** đúng lề, font Times New Roman, bảng nơi
  nhận và chữ ký.
- **Đồ thị tri thức pháp lý:** trực quan hóa liên kết giữa cơ quan ban hành, thẩm
  quyền ký, con dấu và văn bản pháp luật liên quan.

Nguyên tắc: ảnh giấy tờ chứa dữ liệu cá nhân chỉ được gửi tới AI provider ngoài
khi chính sách che/lọc dữ liệu được duyệt. Kết quả OCR luôn cần con người xác
nhận.

Đặc tả: [vision-ocr](features/vision-ocr/vision-ocr-urd.md).

## 5.3 Chấm công sinh trắc học và chống giả mạo

| Endpoint | Chức năng |
| --- | --- |
| `POST /api/face/enroll` | Đăng ký khuôn mặt (nhiều góc) |
| `DELETE /api/face/enroll/{user_id}` | Xóa dữ liệu khuôn mặt |
| `POST /api/face/verify` | Xác minh 1-1 (đăng nhập Face ID, xác thực lại) |
| `POST /api/face/identify` | Nhận diện 1-N (điểm danh) |
| `GET/POST /api/face/storage-config` | Cấu hình lưu trữ embedding |

- Mô hình **ArcFace/InsightFace** (`buffalo_l`), vector 512 chiều, ngưỡng so khớp
  mặc định 0.75.
- **Chống giả mạo hai lớp:** phân tích quang học thụ động và kiểm tra chuyển động
  tương tác (nháy mắt, quay đầu) để chặn ảnh in, màn hình điện thoại, video phát
  lại.
- Đăng ký 6 góc mặt; dữ liệu embedding lưu ở volume riêng của service.

## 5.4 Giám sát hành vi bằng Computer Vision

| Endpoint | Chức năng |
| --- | --- |
| `POST /api/behavior/detect` | Phát hiện sự kiện trên khung hình |
| `GET/POST /api/vision/controller/config` | Cấu hình mô hình, ngưỡng, nhãn |

- Mô hình **YOLO**, ngưỡng tin cậy mặc định 0.25.
- Nhãn mặc định: hút thuốc, điếu thuốc, ghế trống, bàn không người.
- Chỉ áp dụng tại khu vực đã công bố. Mỗi sự kiện là **cảnh báo** cho đến khi
  quản lý xác nhận; ảnh bằng chứng tuân theo chính sách lưu giữ.

Đặc tả: [cv-event-monitoring](features/cv-event-monitoring/cv-event-monitoring-urd.md).
