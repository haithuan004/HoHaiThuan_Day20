# Dependency Map + Critical Path — AI Nurse Assistant

> **Sản phẩm:** AI Nurse Assistant · SafeAge AI
> **Người thực hiện:** Hồ Hải Thuận · 2A202600058
> **Nguyên tắc cốt lõi:** Mỗi Tier 1 dependency phải có Plan B sẵn sàng deploy trong 24 giờ.

---

## 1. External Dependencies — 3 rủi ro có thể giết dự án trong 30 ngày

---

### 🔴 Dependency 1 — Foundation Model API (OpenAI / Anthropic / Gemini)

**Tôi ký sinh trên:** API của OpenAI (GPT-4o) cho module tóm tắt incident report tự động và Gemini Flash cho classification fallback.

**Worst-case scenario:**
> OpenAI tăng giá gấp 3x đột ngột hoặc siết rate limit xuống còn 20% so với hiện tại (như vụ AI Legal startup 2024), khiến toàn bộ tính năng tóm tắt sự cố và alert tạm ngừng hoạt động trong giờ cao điểm.

**Plan B — Đã code, sẵn sàng switch trong 24 giờ:**
- Xây dựng **LLM Abstraction Layer** với interface chuẩn: một lớp wrapper duy nhất gọi API — không hard-code vendor
- Primary: `OpenAI GPT-4o-mini` (giá rẻ nhất cho summarization)
- Fallback 1: `Google Gemini 1.5 Flash` — đã có API key và tested
- Fallback 2: **Local model on-premise**: `Llama-3.2-3B-Instruct` chạy trên Jetson Orin hoặc server edge — không phụ thuộc cloud, phù hợp môi trường y tế cần bảo mật dữ liệu bệnh nhân
- **Caching layer**: 70% incident report dùng template cố định → không cần gọi API mỗi lần

**Cost Plan B:** 2 tuần dev (abstraction layer đã 60% xong). Local model: NVIDIA Jetson Orin NX 16GB ~12 triệu VNĐ/unit.

**Tier:** 🔴 Tier 1 — có thể giết product trong 1 ngày nếu không có fallback

---

### 🔴 Dependency 2 — Camera Integration (RTSP stream từ camera IP của cơ sở)

**Tôi ký sinh trên:** Camera IP sẵn có của cơ sở (Hikvision, Dahua, Ezviz) qua giao thức RTSP. Sản phẩm **không bán phần cứng** — đây là điểm khác biệt và cũng là rủi ro.

**Worst-case scenario:**
> Cơ sở nâng cấp camera lên model mới với chuẩn RTSP khác (hoặc vendor lock-in SDK riêng), hoặc firmware update của hãng camera phá vỡ RTSP stream format hiện tại → toàn bộ fall detection offline.

**Plan B — Đã xác định, cần 1 tuần để deploy:**
- Hỗ trợ **3 integration methods** song song: (1) RTSP standard, (2) ONVIF protocol, (3) SDK native của Hikvision/Dahua (top 2 vendor tại VN)
- **Fallback hardware option:** Nếu camera cơ sở không tương thích → cung cấp tùy chọn thuê thêm 1 camera IP chuẩn (Imou/Reolink ~800K/unit) gắn song song
- SLA cam kết: nếu integration lỗi → kỹ thuật viên onsite trong 4 giờ (Tier 1 SLA cho B2B)

**Cost Plan B:** 3 tuần dev (ONVIF SDK integration). Camera hardware fallback: 800K–1.5M VNĐ/phòng.

**Tier:** 🔴 Tier 1 — không có camera stream = không có product

---

### 🟡 Dependency 3 — Apple App Store / Google Play Store Review Policy

**Tôi ký sinh trên:** App mobile cho điều dưỡng được phân phối qua App Store (iOS) và Google Play (Android). Cơ sở y tế VN dùng 70% Android, 30% iOS.

**Worst-case scenario:**
> Apple thay đổi chính sách về app xử lý dữ liệu y tế (HealthKit-adjacent), yêu cầu thêm Medical Device Software compliance review — kéo dài 3–6 tháng. Hoặc app bị reject vì camera access policy thắt chặt.

**Plan B — Sẵn sàng deploy trong 3 ngày:**
- **Progressive Web App (PWA)** đã được build song song với native app — hoạt động trên mọi browser mobile, không cần App Store approval
- Push notification qua PWA (Web Push API) — không phụ thuộc APN/FCM
- Với Android: cũng có thể sideload APK trực tiếp cho cơ sở pilot (B2B không phải consumer)
- **Long-term:** Comply day-1 với Apple HealthKit guidelines để không bị reject

**Cost Plan B:** 1 tuần dev (PWA đã 80% feature parity). Zero additional cost.

**Tier:** 🟡 Tier 2 — có thể giết trong 1–4 tuần. Ít khẩn cấp hơn Tier 1 nhưng cần monitor.

---

## 2. Critical Path — Chuỗi task tuần tự không thể parallel

```
[Wk1-2]  Data Pipeline        →  [Wk2-4]  Legal Compliance   →  [Wk4-8]  Model Fine-tune
   Camera RTSP integration           Ký NDA với cơ sở              ST-GCN trên data VN
   Skeleton extraction pipeline      Data processing agreement     Validate precision > 85%
   Data annotation (8.000 tracks)    Nghị định 13/2023 PDPA                |
          |                                   |                             |
          └───────────────────────────────────┴─────────────────────────────┘
                                              ↓
                                   [Wk8-10]  API Integration
                                      Backend + Mobile App
                                      Push notification pipeline
                                              ↓
                                   [Wk10-12] Pilot Launch
                                      Deploy tại 1 viện dưỡng lão
                                      3 tháng thu thập feedback
```

**Critical Path (chuỗi đỏ — không thể trễ):**
`Data Pipeline → Legal Compliance → Model Fine-tune → API Integration → Pilot Launch`

**Non-critical tasks (có thể parallel — không ảnh hưởng ngày launch):**

| Task | Chạy song song với | Buffer |
|---|---|---|
| UI/UX Design (mobile app) | Legal Compliance | 3 tuần |
| Marketing materials & landing page | Model Fine-tune | 4 tuần |
| Analytics Dashboard | API Integration | 2 tuần |
| Documentation & training guide | Pilot Launch prep | 1 tuần |

---

## 3. Kết luận — Nguyên tắc áp dụng

> **Mọi engineering effort trong 3 tuần đầu phải tập trung vào Data Pipeline và Legal Compliance — hai task nằm trên Critical Path mà founder thường underestimate nhất.**

> Không để engineer làm UI polish khi Data Pipeline chưa xong. Không làm landing page khi Legal Compliance (NDA, PDPA) chưa clear.

> **Plan B không phải document. Là code đã viết, đã test, sẵn sàng switch.** Khi crisis — không có thời gian code Plan B từ đầu.

---

*Case study tham chiếu: AI Legal startup 2024 — đã có RICE, OKR, Roadmap đầy đủ nhưng bỏ qua Dependency Map → phá sản sau 4 tháng khi OpenAI siết rate limit.*
*Framework: Dependency Map Tier 1/2/3 · Critical Path Method (CPM) · Day 20 Handbook*
