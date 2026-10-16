# 3. Danh mục tính năng

Trải nghiệm trực tiếp tại <https://staging.wpcteam.shop/>.

Town Hown gồm 39 tính năng chia thành 7 nhóm. Mỗi tính năng có bộ đặc tả riêng
trong [`features/`](features/README.md):

- **URD** — nhu cầu, hành trình và kết quả theo góc nhìn người dùng.
- **SRS** — yêu cầu kiểm thử được, business rule, lỗi, phụ thuộc, tiêu chí thành công.
- **ERD** — mô hình dữ liệu khái niệm phục vụ SRS.
- **Brainstorm** — các phương án đã cân nhắc và quyết định đang chờ xác nhận.

Mức ưu tiên theo MoSCoW: **Must** là phạm vi pilot v1; **Should**/**Could** là
lộ trình mở rộng. Danh mục mô tả phạm vi mục tiêu, không khẳng định mọi tính năng
đã hoàn tất trong mã nguồn.

## Bảng tổng hợp

| # | Tính năng | Nhóm | Người dùng | Ưu tiên | Phụ thuộc | Đặc tả |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | Quản lý tài khoản và truy cập | Identity & Governance | Tất cả | Must | Không | [URD](features/account-access/account-access-urd.md) · [SRS](features/account-access/srs/account-access-spec.md) · [ERD](features/account-access/srs/account-access-erd.md) |
| 2 | Quản lý tổ chức, quyền và audit | Identity & Governance | Admin, quản lý | Must | 1 | [URD](features/org-governance/org-governance-urd.md) · [SRS](features/org-governance/srs/org-governance-spec.md) · [ERD](features/org-governance/srs/org-governance-erd.md) |
| 3 | Quản lý hồ sơ nhân viên | Core HR | HR, nhân viên | Should | 2 | [URD](features/employee-profiles/employee-profiles-urd.md) · [SRS](features/employee-profiles/srs/employee-profiles-spec.md) · [ERD](features/employee-profiles/srs/employee-profiles-erd.md) |
| 4 | Quản lý vòng đời và tài liệu nhân sự | Core HR | HR, quản lý | Could | 3 | [URD](features/employment-lifecycle/employment-lifecycle-urd.md) · [SRS](features/employment-lifecycle/srs/employment-lifecycle-spec.md) · [ERD](features/employment-lifecycle/srs/employment-lifecycle-erd.md) |
| 5 | Lập và phê duyệt nhu cầu tuyển dụng | Recruitment | HR, quản lý | Must | 2 | [URD](features/recruitment-planning/recruitment-planning-urd.md) · [SRS](features/recruitment-planning/srs/recruitment-planning-spec.md) · [ERD](features/recruitment-planning/srs/recruitment-planning-erd.md) |
| 6 | Tiếp nhận và chuẩn hóa CV | Recruitment | HR, ứng viên | Must | 5, 17, 18 | [URD](features/cv-intake/cv-intake-urd.md) · [SRS](features/cv-intake/srs/cv-intake-spec.md) · [ERD](features/cv-intake/srs/cv-intake-erd.md) |
| 7 | Đối chiếu ứng viên với vị trí | Recruitment | HR | Must | 5, 6 | [URD](features/candidate-matching/candidate-matching-urd.md) · [SRS](features/candidate-matching/srs/candidate-matching-spec.md) · [ERD](features/candidate-matching/srs/candidate-matching-erd.md) |
| 8 | Điều phối pipeline ứng viên | Recruitment | HR | Must | 6 | [URD](features/candidate-pipeline/candidate-pipeline-urd.md) · [SRS](features/candidate-pipeline/srs/candidate-pipeline-spec.md) · [ERD](features/candidate-pipeline/srs/candidate-pipeline-erd.md) |
| 9 | Lập lịch và điều phối phỏng vấn | Recruitment | HR, interviewer | Must | 8 | [URD](features/interview-management/interview-management-urd.md) · [SRS](features/interview-management/srs/interview-management-spec.md) · [ERD](features/interview-management/srs/interview-management-erd.md) |
| 10 | Ghi nhận và tổng hợp đánh giá phỏng vấn | Recruitment | Interviewer, HR | Must | 9 | [URD](features/interview-evaluation/interview-evaluation-urd.md) · [SRS](features/interview-evaluation/srs/interview-evaluation-spec.md) · [ERD](features/interview-evaluation/srs/interview-evaluation-erd.md) |
| 11 | Tạo và theo dõi offer | Recruitment | HR, ứng viên | Should | 8, 10 | [URD](features/offer-management/offer-management-urd.md) · [SRS](features/offer-management/srs/offer-management-spec.md) · [ERD](features/offer-management/srs/offer-management-erd.md) |
| 12 | Thực hiện onboarding | Recruitment | HR, nhân viên | Should | 3, 11 | [URD](features/employee-onboarding/employee-onboarding-urd.md) · [SRS](features/employee-onboarding/srs/employee-onboarding-spec.md) · [ERD](features/employee-onboarding/srs/employee-onboarding-erd.md) |
| 13 | Quản lý cuộc họp và transcript | Meetings & Work | Nhân viên, quản lý | Should | 1 | [URD](features/meeting-records/meeting-records-urd.md) · [SRS](features/meeting-records/srs/meeting-records-spec.md) · [ERD](features/meeting-records/srs/meeting-records-erd.md) |
| 14 | Tạo và xác nhận biên bản bằng AI | Meetings & Work | Chủ trì | Should | 13 | [URD](features/ai-meeting-minutes/ai-meeting-minutes-urd.md) · [SRS](features/ai-meeting-minutes/srs/ai-meeting-minutes-spec.md) · [ERD](features/ai-meeting-minutes/srs/ai-meeting-minutes-erd.md) |
| 15 | Chuyển biên bản thành công việc | Meetings & Work | Chủ trì, assignee | Should | 14, 16 | [URD](features/meeting-to-tasks/meeting-to-tasks-urd.md) · [SRS](features/meeting-to-tasks/srs/meeting-to-tasks-spec.md) · [ERD](features/meeting-to-tasks/srs/meeting-to-tasks-erd.md) |
| 16 | Quản lý Kanban và bàn giao công việc | Meetings & Work | Nhân viên, quản lý | Should | 2 | [URD](features/kanban-workspaces/kanban-workspaces-urd.md) · [SRS](features/kanban-workspaces/srs/kanban-workspaces-spec.md) · [ERD](features/kanban-workspaces/srs/kanban-workspaces-erd.md) |
| 17 | Tiếp nhận và xử lý tài liệu | Document AI | HR, admin | Must | 2 | [URD](features/document-intake/document-intake-urd.md) · [SRS](features/document-intake/srs/document-intake-spec.md) · [ERD](features/document-intake/srs/document-intake-erd.md) |
| 18 | Trích xuất và xác nhận dữ liệu tài liệu | Document AI | HR, reviewer | Must | 17 | [URD](features/document-review/document-review-urd.md) · [SRS](features/document-review/srs/document-review-spec.md) · [ERD](features/document-review/srs/document-review-erd.md) |
| 19 | Quản lý ngân hàng câu hỏi | Assessment & Talent | HR, interviewer | Must | 2 | [URD](features/question-bank/question-bank-urd.md) · [SRS](features/question-bank/srs/question-bank-spec.md) · [ERD](features/question-bank/srs/question-bank-erd.md) |
| 20 | Sinh câu hỏi từ tài liệu bằng AI | Assessment & Talent | HR, interviewer | Should | 17, 18, 19 | [URD](features/ai-question-generation/ai-question-generation-urd.md) · [SRS](features/ai-question-generation/srs/ai-question-generation-spec.md) · [ERD](features/ai-question-generation/srs/ai-question-generation-erd.md) |
| 21 | Tạo và phát hành bài đánh giá | Assessment & Talent | HR, interviewer | Must | 19 | [URD](features/assessment-authoring/assessment-authoring-urd.md) · [SRS](features/assessment-authoring/srs/assessment-authoring-spec.md) · [ERD](features/assessment-authoring/srs/assessment-authoring-erd.md) |
| 22 | Thực hiện bài đánh giá | Assessment & Talent | Ứng viên, nhân viên | Must | 21 | [URD](features/candidate-assessment/candidate-assessment-urd.md) · [SRS](features/candidate-assessment/srs/candidate-assessment-spec.md) · [ERD](features/candidate-assessment/srs/candidate-assessment-erd.md) |
| 23 | Chấm điểm và phân tích năng lực | Assessment & Talent | HR, interviewer | Must | 22 | [URD](features/assessment-grading/assessment-grading-urd.md) · [SRS](features/assessment-grading/srs/assessment-grading-spec.md) · [ERD](features/assessment-grading/srs/assessment-grading-erd.md) |
| 24 | Ghi âm và tóm tắt phiên phỏng vấn | Assessment & Talent | Interviewer | Should | 9, 10 | [URD](features/interview-recording/interview-recording-urd.md) · [SRS](features/interview-recording/srs/interview-recording-spec.md) · [ERD](features/interview-recording/srs/interview-recording-erd.md) |
| 25 | Tạo báo cáo và cảnh báo quản trị | Insights & Integrations | Quản lý, lãnh đạo | Should | 2, 8, 16, 22, 23 | [URD](features/management-reporting/management-reporting-urd.md) · [SRS](features/management-reporting/srs/management-reporting-spec.md) · [ERD](features/management-reporting/srs/management-reporting-erd.md) |
| 26 | Gửi thông báo theo ngữ cảnh | Insights & Integrations | Tất cả | Must | 1, 2 | [URD](features/contextual-notifications/contextual-notifications-urd.md) · [SRS](features/contextual-notifications/srs/contextual-notifications-spec.md) · [ERD](features/contextual-notifications/srs/contextual-notifications-erd.md) |
| 27 | Kết nối lịch, webhook và công cụ ngoài | Insights & Integrations | HR, admin | Should | 2 | [URD](features/external-integrations/external-integrations-urd.md) · [SRS](features/external-integrations/srs/external-integrations-spec.md) · [ERD](features/external-integrations/srs/external-integrations-erd.md) |
| 28 | Quản lý cấu hình nền tảng | Identity & Governance | Admin | Should | 1, 2 | [URD](features/platform-configuration/platform-configuration-urd.md) · [SRS](features/platform-configuration/srs/platform-configuration-spec.md) · [ERD](features/platform-configuration/srs/platform-configuration-erd.md) |
| 29 | Theo dõi vận hành nhân viên minh bạch | Insights & Integrations | Quản lý, nhân viên | Could | 2, 16, 25 | [URD](features/workforce-monitoring/workforce-monitoring-urd.md) · [SRS](features/workforce-monitoring/srs/workforce-monitoring-spec.md) · [ERD](features/workforce-monitoring/srs/workforce-monitoring-erd.md) |
| 30 | Quản lý thư viện và phiên bản tài liệu | Document AI | HR, content editor | Should | 17, 18 | [URD](features/document-library/document-library-urd.md) · [SRS](features/document-library/srs/document-library-spec.md) · [ERD](features/document-library/srs/document-library-erd.md) |
| 31 | Quản lý mẫu bài đánh giá | Assessment & Talent | Admin, HR | Should | 19, 21 | [URD](features/assessment-templates/assessment-templates-urd.md) · [SRS](features/assessment-templates/srs/assessment-templates-spec.md) · [ERD](features/assessment-templates/srs/assessment-templates-erd.md) |
| 32 | Quản lý khung kỹ năng và kỳ vọng vị trí | Assessment & Talent | HR, quản lý | Should | 2, 3 | [URD](features/talent-framework/talent-framework-urd.md) · [SRS](features/talent-framework/srs/talent-framework-spec.md) · [ERD](features/talent-framework/srs/talent-framework-erd.md) |
| 33 | Đánh giá năng lực nhân viên | Assessment & Talent | Quản lý, nhân viên | Should | 22, 23, 32 | [URD](features/employee-evaluation/employee-evaluation-urd.md) · [SRS](features/employee-evaluation/srs/employee-evaluation-spec.md) · [ERD](features/employee-evaluation/srs/employee-evaluation-erd.md) |
| 34 | Phân tích độ phủ và khoảng trống kỹ năng | Assessment & Talent | HR, quản lý | Should | 3, 32, 33 | [URD](features/skill-gap-analysis/skill-gap-analysis-urd.md) · [SRS](features/skill-gap-analysis/srs/skill-gap-analysis-spec.md) · [ERD](features/skill-gap-analysis/srs/skill-gap-analysis-erd.md) |
| 35 | Gửi email nghiệp vụ có mẫu và nhật ký | Insights & Integrations | HR, admin | Should | 2, 26 | [URD](features/operational-email/operational-email-urd.md) · [SRS](features/operational-email/srs/operational-email-spec.md) · [ERD](features/operational-email/srs/operational-email-erd.md) |
| 36 | Công bố phiên bản và thông báo thay đổi | Identity & Governance | Admin, người dùng | Could | 1, 2, 28 | [URD](features/release-announcements/release-announcements-urd.md) · [SRS](features/release-announcements/srs/release-announcements-spec.md) · [ERD](features/release-announcements/srs/release-announcements-erd.md) |
| 37 | Theo dõi mức sử dụng AI | Identity & Governance | Admin | Should | 2, 28 | [URD](features/ai-usage-monitoring/ai-usage-monitoring-urd.md) · [SRS](features/ai-usage-monitoring/srs/ai-usage-monitoring-spec.md) · [ERD](features/ai-usage-monitoring/srs/ai-usage-monitoring-erd.md) |
| 38 | Giám sát sự kiện vi phạm bằng Computer Vision | Insights & Integrations | Quản lý, admin | Could | 2, 16, 25, 26, 27 | [URD](features/cv-event-monitoring/cv-event-monitoring-urd.md) · [SRS](features/cv-event-monitoring/srs/cv-event-monitoring-spec.md) · [ERD](features/cv-event-monitoring/srs/cv-event-monitoring-erd.md) |
| 39 | Bóc tách văn bản từ ảnh có con người xác nhận | Document AI | HR | Should | Không | [URD](features/vision-ocr/vision-ocr-urd.md) · [SRS](features/vision-ocr/srs/vision-ocr-spec.md) · [ERD](features/vision-ocr/srs/vision-ocr-erd.md) |

## Theo nhóm

### Identity & Governance
Quản lý tài khoản và truy cập, tổ chức/quyền/audit, cấu hình nền tảng, công bố
phiên bản, theo dõi mức sử dụng AI. Đảm bảo mọi hành động đều gắn với một danh
tính, một vai trò và để lại dấu vết.

### Core HR
Hồ sơ nhân viên, vòng đời và tài liệu nhân sự. Hồ sơ là điểm hội tụ của dữ liệu
từ tuyển dụng, onboarding và đánh giá.

### Recruitment
Từ nhu cầu tuyển dụng đã duyệt → tiếp nhận CV → so khớp → pipeline → phỏng vấn →
đánh giá phỏng vấn → offer → onboarding. Pipeline dùng state machine cố định
(xem [Vai trò và hành trình](04-vai-tro-va-hanh-trinh.md)).

### Meetings & Work
Cuộc họp và transcript, biên bản do AI đề xuất và người chủ trì xác nhận, chuyển
biên bản thành công việc, bảng Kanban và bàn giao.

### Document AI
Tiếp nhận tài liệu, trích xuất và xác nhận dữ liệu, thư viện và phiên bản tài
liệu, OCR ảnh có con người xác nhận (xem [Các module AI](05-module-ai.md)).

### Assessment & Talent
Ngân hàng câu hỏi, sinh câu hỏi từ tài liệu bằng AI, soạn/phát hành/làm/chấm bài
đánh giá, mẫu bài đánh giá, ghi âm và tóm tắt phỏng vấn, khung kỹ năng, đánh giá
năng lực nhân viên, phân tích khoảng trống kỹ năng.

### Insights & Integrations
Báo cáo quản trị, thông báo theo ngữ cảnh, email nghiệp vụ có mẫu và nhật ký, kết
nối lịch/webhook, theo dõi vận hành minh bạch, giám sát sự kiện bằng computer
vision.

## Màn hình chính trên staging

| Khu vực | Đường dẫn | Mục đích |
| --- | --- | --- |
| Trang chủ | [`/`](https://staging.wpcteam.shop/) | Giới thiệu và lối vào |
| Đăng nhập | [`/login`](https://staging.wpcteam.shop/login) | Đăng nhập email/mật khẩu hoặc Face ID |
| Đăng ký | [`/register`](https://staging.wpcteam.shop/register) | Tạo tài khoản |
| Dashboard | `/dashboard` | Tổng quan theo vai trò (HR, interviewer, quản lý, admin) |
| Tuyển dụng | `/dashboard/recruitment` | Pipeline ứng viên, CV, JD, phỏng vấn |
| Phỏng vấn | `/dashboard/interviews`, `/dashboard/interview-room` | Lịch và phòng phỏng vấn |
| Bài đánh giá | `/dashboard/tests`, `/dashboard/question-bank`, `/dashboard/results`, `/dashboard/templates` | Soạn, phát hành, chấm, mẫu |
| Nhân tài | `/dashboard/persons`, `/dashboard/positions`, `/dashboard/skills`, `/dashboard/groups` | Hồ sơ, vị trí, kỹ năng, nhóm |
| Document AI | `/dashboard/document-ai`, `/dashboard/ocr` | Tài liệu, OCR, Nghị định 30 Studio |
| Chấm công | `/dashboard/attendance`, `/dashboard/faces`, `/dashboard/my-face` | Điểm danh, quản lý và đăng ký khuôn mặt |
| Giám sát hành vi | `/dashboard/behavior`, `/dashboard/model-controller` | Sự kiện vi phạm và cấu hình mô hình |
| Quản trị | `/dashboard/users`, `/dashboard/settings`, `/dashboard/emails`, `/dashboard/versions` | Người dùng, cấu hình, email, phiên bản |

Các trang trong `/dashboard` yêu cầu đăng nhập; nội dung hiển thị phụ thuộc vai
trò.
