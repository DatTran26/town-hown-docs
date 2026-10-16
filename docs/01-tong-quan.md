# 1. Tổng quan sản phẩm

Hệ thống đang chạy thử tại <https://staging.wpcteam.shop/>.

## Định vị

Town Hown là nền tảng HRMS B2B tích hợp AI. Lát cắt thương mại v1 giúp đội
tuyển dụng đưa một hồ sơ từ lúc tiếp nhận đến quyết định đã được con người
review, đúng bước, có evidence và không thất lạc trạng thái.

## Vấn đề cần giải quyết

Doanh nghiệp thường quản lý hồ sơ nhân sự, tuyển dụng, phỏng vấn, bài đánh giá,
biên bản họp và giao việc trên nhiều file và công cụ rời. Hệ quả:

- dữ liệu bị nhập lại nhiều lần;
- trạng thái khó truy nguyên, người phụ trách bỏ sót hạn;
- evidence phân tán, quyết định khó giải thích;
- lãnh đạo không có góc nhìn thống nhất.

AI có thể giảm thao tác thủ công ở CV, tài liệu, câu hỏi, transcript và báo cáo.
Nhưng nếu thiếu phân quyền, evidence và bước review của con người, AI làm tăng
rủi ro quyết định sai hoặc lộ dữ liệu. Town Hown giải quyết cả hai vế.

## Giá trị khác biệt

- Một luồng dữ liệu liên thông từ CV, tài liệu, cuộc họp, bài test đến hồ sơ,
  quyết định và công việc, thay vì sao chép giữa các công cụ.
- AI hỗ trợ trích xuất, sinh nội dung, đối chiếu, tóm tắt; mọi kết quả đều có
  đường review, override và provenance.
- Quyền truy cập theo vai trò, tổ chức và phạm vi quản lý là ràng buộc sản phẩm.
- Tuyển dụng, đánh giá và mô hình nhân tài dùng chung `persons`, `positions`,
  `skills` và evidence, nên kết quả đánh giá luôn có ngữ cảnh.
- Audit và log vận hành được tách bạch; log không trở thành nguồn quyết định
  nhân sự.

## Mục tiêu

1. Chuẩn hóa quy trình nhân sự và tuyển dụng thành trạng thái, trách nhiệm, hạn
   và evidence rõ ràng.
2. Giảm nhập liệu và tổng hợp thủ công bằng AI có human review.
3. Chứng minh lát cắt tuyển dụng + đánh giá trước khi mở rộng sang Core HR, họp
   và công việc.
4. Cho lãnh đạo góc nhìn quản trị theo đúng phạm vi quyền.
5. Bảo vệ dữ liệu nhân sự và truy nguyên mọi quyết định tác động đến con người.

## Ngoài phạm vi (non-goals)

- AI không tự động tuyển, loại, kỷ luật hay kết luận phẩm chất con người.
- Không giám sát bí mật, keylogging hay thu thập hoạt động ngoài chính sách đã
  công bố.
- Không thay thế payroll, kế toán, thuế hay hệ thống pháp lý trong v1.
- Không tuyên bố tuân thủ PDPA/GDPR khi chưa có policy, retention và DPA được
  duyệt.
- Không xây marketplace hay nền tảng HR cho người tiêu dùng.

## Phạm vi v1

V1 cam kết 15 tính năng mức **Must**, tạo thành một hành trình tuyển dụng có
thể pilot: định danh và quản trị, lập nhu cầu tuyển dụng, tiếp nhận và review tài
liệu, tiếp nhận CV, so khớp, pipeline, ngân hàng câu hỏi, soạn/làm/chấm bài đánh
giá, quản lý và đánh giá phỏng vấn, thông báo nền.

| Kết quả v1 | Điều kiện hoàn thành |
| --- | --- |
| Thiết lập tenant pilot an toàn | Vai trò, phạm vi và audit cho hành động nhạy cảm được kiểm tra |
| Đưa CV thành application đã review | File hợp lệ; trích xuất có provenance; HR xác nhận dữ liệu |
| Điều phối application đến đánh giá/phỏng vấn | Trạng thái, người phụ trách, hạn và đường xử lý thủ công rõ ràng |
| Thu bài đánh giá không mất dữ liệu | Snapshot, autosave, hết hạn, số lần làm và nộp bài được kiểm chứng |
| Tạo quyết định có evidence | Điểm/đánh giá có reviewer; AI không tự pass/fail |
| Đo được pilot | North Star, guardrail và nguồn sự kiện được sponsor chấp nhận |

## Phạm vi dài hạn

| Nhóm | Mục tiêu |
| --- | --- |
| Identity & Governance | Xác định ai được làm gì và truy nguyên hành động |
| Core HR | Duy trì hồ sơ và vòng đời nhân sự có kiểm soát |
| Recruitment | Điều phối từ nhu cầu tuyển dụng đến onboarding |
| Meetings & Work | Biến trao đổi thành quyết định và công việc |
| Document AI | Chuyển file thành dữ liệu có provenance và review |
| Assessment & Talent | Tạo, thực hiện và phân tích đánh giá năng lực |
| Insights & Integrations | Thông báo, báo cáo và kết nối hệ thống ngoài |

## Chỉ số thành công

**North Star v1:** tỷ lệ application đủ điều kiện đi từ CV đã được HR xác nhận
đến quyết định tuyển dụng đã được con người review, trong SLA đã công bố.

| Chỉ số | Ý nghĩa |
| --- | --- |
| `M-IN-01` | Tỷ lệ application bị kẹt ở một trạng thái quá SLA |
| `M-IN-02` | Tỷ lệ bài đánh giá đã bắt đầu được nộp hợp lệ và có biên nhận |
| `M-IN-03` | Tỷ lệ trường CV do AI trích xuất được HR giữ nguyên |
| `M-GR-01` | Số sự cố truy cập vượt phạm vi quyền (mục tiêu: 0) |
| `M-GR-02` | Tỷ lệ quyết định bị đảo do gợi ý AI sai |
| `M-GR-03` | Số bài nộp bị mất câu trả lời đã được server xác nhận (mục tiêu: 0) |

Chi tiết đầy đủ, rủi ro và câu hỏi mở: [PRD](product/prd.md).
