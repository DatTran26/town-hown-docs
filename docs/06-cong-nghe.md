# 6. Công nghệ sử dụng

Ứng dụng đang chạy: <https://staging.wpcteam.shop/>.

## Stack

| Tầng | Công nghệ |
| --- | --- |
| Web app | Next.js 16 (App Router, standalone), React 19, TypeScript strict |
| Giao diện | Tailwind CSS 4, shadcn, Base UI, Lucide icons, Framer Motion, next-themes |
| Form và validate | React Hook Form, Zod |
| Dữ liệu | Supabase: PostgreSQL, Auth, Row Level Security, Storage, RPC |
| Xử lý nền | Supabase Edge Functions (Deno) |
| AI | OpenAI SDK, Google GenAI SDK (Gemini) |
| Vision | FastAPI, InsightFace/ArcFace, Ultralytics YOLO, Gemini Vision, Pytesseract |
| Email | Nodemailer (SMTP, mật khẩu mã hóa khi lưu) |
| Chống bot | Cloudflare Turnstile qua Supabase Auth CAPTCHA |
| Tài liệu và xuất file | pdf-parse, mammoth, jsPDF, ExcelJS, xlsx, python-docx |
| Hiển thị | react-markdown, CodeMirror, react-big-calendar, DOMPurify |
| Đóng gói | Docker multi-stage, Docker Compose, GitHub Container Registry |
| CI/CD | GitHub Actions |

## Nhóm API của BFF

Tất cả API nằm dưới `/api/*` cùng origin với giao diện.

| Nhóm | Endpoint chính |
| --- | --- |
| Xác thực | `register`, `face-login`, `face-register`, `face` |
| Tuyển dụng | `recruitment/*` (applications, cv, jd-parse, interviews, interview-room, report, sessions…) |
| Đánh giá | `tests`, `question-bank`, `results`, `scoring`, `templates`, `followup-sessions` |
| Nhân tài | `persons`, `positions`, `skills`, `skill-categories`, `skill-evaluations`, `person-skills`, `groups` |
| Tài liệu | `documents`, `document-sources`, `document-topics`, `ocr` |
| AI | `ai/*`, `ai-usage` |
| Vision | `attendance`, `behavior`, `vision-controller` |
| Công việc | `tasks`, `notes`, `tags`, `entity-tags` |
| Quản trị | `users`, `settings`, `emails`, `versions`, `activity-logs`, `export`, `app-build` |
| Vận hành | `health` |

## Cấu hình

| Biến | Phạm vi | Ghi chú |
| --- | --- | --- |
| `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Public | In vào bundle lúc build |
| `NEXT_PUBLIC_APP_URL` | Public | Origin tuyệt đối, ví dụ `https://staging.wpcteam.shop` |
| `NEXT_PUBLIC_ENABLE_TURNSTILE`, `NEXT_PUBLIC_TURNSTILE_SITE_KEY` | Public | Bật CAPTCHA đăng nhập |
| `SUPABASE_SERVICE_ROLE_KEY` | Server | Chỉ dùng ở server |
| `DATABASE_URL` | Server | Kết nối PostgreSQL trực tiếp |
| `OPENAI_API_KEY`, `OPENAI_MODEL` | Server | Nhà cung cấp AI |
| `GEMINI_API_KEY`, `GEMINI_MODEL` | Server | Gemini cho AI và OCR |
| `VISION_AI_URL`, `VISION_OCR_URL` | Server | Địa chỉ nội bộ của service vision |
| `SMTP_PASSWORD_ENCRYPTION_KEY` | Server | Mã hóa mật khẩu SMTP lưu trong DB |
| `FACE_MODEL_NAME`, `FACE_MATCH_THRESHOLD` | Vision AI | Mô hình và ngưỡng nhận diện |
| `BEHAVIOR_MODEL_PATH`, `BEHAVIOR_CONFIDENCE`, `BEHAVIOR_LABELS` | Vision AI | Mô hình hành vi |

Biến có tiền tố `NEXT_PUBLIC_*` có thể xuất hiện ở trình duyệt, nên không bao
giờ chứa secret.
