# RICE Matrix — AI Nurse Assistant (SafeAge AI · B2B)

> **Sản phẩm:** AI Nurse Assistant — hệ thống giám sát thông minh tích hợp vào camera hiện có, giúp điều dưỡng phát hiện sự cố ngã tức thì và tự động hóa hồ sơ an toàn bệnh nhân tại viện dưỡng lão & bệnh viện tư.
>
> **Người thực hiện:** Hồ Hải Thuận · 2A202600058
> **Ngày:** Day 20

---

## 1. Bảng RICE — 5 tính năng cốt lõi

| # | Tính năng | R (Reach / quý) | I (Impact) | C (Confidence) | E (Effort / person-month) | **RICE Score** |
|---|---|:---:|:---:|:---:|:---:|:---:|
| 1 | **Fall Detection real-time** — Phát hiện ngã từ camera IP & push notification < 30 giây | 150 | 3 | 0.80 | 3 | **120** |
| 2 | **Incident Report PDF** — Tự động tạo báo cáo sự cố PDF có timestamp, phòng, clip | 120 | 2 | 0.80 | 2 | **96** |
| 3 | **Management Dashboard** — Lịch sử sự cố, timeline, xem lại clip cho quản lý | 100 | 1 | 0.80 | 2 | **40** |
| 4 | **Analytics & Insights** — Thống kê pattern ngã, shift nguy hiểm nhất, khuyến nghị phòng ngừa | 60 | 2 | 0.50 | 3 | **20** |
| 5 | **Gait Risk Prediction** — Phân tích dáng đi dự báo nguy cơ ngã trước khi xảy ra | 40 | 3 | 0.50 | 6 | **10** |

### Ghi chú chấm điểm

| Yếu tố | Logic |
|---|---|
| **Reach** | Số cơ sở × nhân sự tiếp xúc tính năng/quý. TAM = ~1.600 cơ sở tư nhân VN. Discounted 50% (Mixpanel benchmark: 20–40% adoption). |
| **Impact** | 3 = massive (giảm rủi ro pháp lý + nhân mạng); 2 = high (hồ sơ tự động); 1 = medium (dashboard xem lại); 0.5 = low |
| **Confidence** | Fall Detection & Report: đã có prototype + phỏng vấn 3 quản lý viện dưỡng lão → 80%. Analytics & Gait: chưa có user validation → 50% MAX |
| **Effort** | Nhân 1.5x so với estimate ban đầu (cộng QA, integration, bug-fix) |

---

## 2. 2×2 Value-Effort Matrix

```
                    Effort
              Low (≤ 2 PM)   High (> 3 PM)
           ┌──────────────┬──────────────┐
    High   │  QUICK WINS  │  STRATEGIC   │
   Value   │  • Incident  │    BETS      │
           │    PDF (#2)  │  • Fall Det  │
           │  • Dashboard │    real-time │
           │    (#3)      │    (#1)      │
           ├──────────────┼──────────────┤
    Low    │  FILL-INS    │NON-STARTERS  │
   Value   │              │  • Gait Risk │
           │              │    Predict   │
           │              │    (#5)      │
           │  Analytics   │              │
           │  Insights(#4)│              │
           └──────────────┴──────────────┘
```

### Phân loại & Chiến lược

| Quadrant | Tính năng | Chiến lược |
|---|---|---|
| ⚡ **Quick Wins** | Incident PDF (#2), Management Dashboard (#3) | Làm ngay — lấy đà, build trust với pilot |
| 🏆 **Strategic Bets** | Fall Detection real-time (#1) | Core moat — đầu tư dài hạn, bắt đầu từ NOW |
| 📋 **Fill-ins** | Analytics & Insights (#4) | Làm khi NEXT phase rảnh tay |
| 🗑️ **Non-starters** | Gait Risk Prediction (#5) | **Loại bỏ** — Confidence 50%, Effort 6 PM, chưa có user validation |

### Kết luận prioritize

> **Làm trước (NOW):** Fall Detection + Incident PDF (RICE top 2) — đây là core value proposition để pilot 1 viện dưỡng lão trong 3 tháng.
>
> **Không làm trong MVP:** Gait Risk Prediction — RICE score thấp nhất (10), Effort cao nhất (6 PM), chưa có data validation.

---

*Nguồn tham chiếu: PRD Day 17 · MVP Boundary Day 17 · Intercom RICE Framework (Sean McBride, 2015)*
