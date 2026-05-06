# OKRs — AI Nurse Assistant · Q1 Pilot

> **Người thực hiện:** Hồ Hải Thuận · 2A202600058
> **Phạm vi:** 1 Objective + 3 Key Results cho quý NOW của Roadmap
> **Framework:** Leading + Lagging + Quality · Aspirational 70% rule

---

## Objective

### 🏥 Trở thành công cụ an toàn bệnh nhân không thể thiếu tại 5 viện dưỡng lão tư nhân đầu tiên ở TP.HCM

*Đủ truyền cảm hứng để đọc to mỗi sáng. Match với vấn đề cột NOW: phát hiện ngã nhanh + bằng chứng sự cố tự động.*

---

## Key Results

### KR1 — Leading: Hành vi sử dụng thực tế (dự báo tương lai)

> **50 điều dưỡng trực tại 5 cơ sở pilot mở app để xác nhận cảnh báo ≥ 4 ngày/tuần trong tháng thứ 3**

**Logic:**
- Đây là "Aha Moment" metric — điều dưỡng chủ động phản ứng với alert (không phải bị ép dùng)
- Nếu < 4 ngày/tuần → product chưa đủ tin cậy để thay đổi behavior
- Baseline hiện tại: 0 (chưa có pilot) → target 4 ngày/tuần là aspirational nhưng đạt được nếu precision > 85%
- **Không đo:** số model calls, latency, accuracy — đây là output, không phải outcome

---

### KR2 — Lagging: Kết quả kinh doanh (xác nhận tác động)

> **Ký được 5 hợp đồng pilot trả phí ≥ 5 triệu VNĐ/tháng/cơ sở trước cuối quý**

**Logic:**
- "Trả phí" = signal mạnh nhất của Product-Market Fit (không phải POC miễn phí)
- ARPU 5 triệu VNĐ/tháng = 60 triệu/năm/cơ sở — thấp hơn 1 nhân công điều dưỡng (15–20 triệu/tháng)
- 5 cơ sở = SOM tối thiểu để validate model kinh doanh trước khi scale
- Từ Day 18 Excel: Base ARPU 600.000 VNĐ/tháng (B2C) → B2B cơ sở target 5 triệu VNĐ (8 × premium)

---

### KR3 — Quality: Sức khỏe bền vững (bảo vệ tăng trưởng)

> **True positive rate ≥ 85% và false alarm ≤ 2 lần/ca trực trong điều kiện môi trường thực tế tại cơ sở pilot**

**Logic:**
- Đây là "Riskiest Assumption" từ PRD Day 17: model có đạt precision > 85% trong điều kiện ánh sáng thấp, góc camera không chuẩn, trang phục bệnh nhân VN không?
- False alarm > 2 lần/ca → điều dưỡng tắt thông báo → product mất giá trị → churn ngay tháng 1
- Nếu không đạt KR3 → phải quay lại retrain model trước khi scale → đây là quality gate bảo vệ KR2

---

## Bảng tóm tắt

| | **KR** | **Loại** | **Tại sao số đó?** |
|---|---|---|---|
| KR1 | 50 điều dưỡng dùng ≥ 4 ngày/tuần | Leading | Behavior metric — dự báo retention |
| KR2 | 5 hợp đồng trả phí ≥ 5M VNĐ/tháng | Lagging | Revenue — xác nhận willingness-to-pay |
| KR3 | True positive ≥ 85%, false alarm ≤ 2/ca | Quality | Model accuracy gate — bảo vệ trust |

---

## Quy tắc 70%

> Hoàn thành 70% của các KR trên = thành công thực sự:
> - KR1: 35/50 điều dưỡng active 4 ngày/tuần → đủ để validate product fit
> - KR2: 3–4/5 hợp đồng → đủ doanh thu để survive và tiếp tục iterate
> - KR3: 80% precision, 2.5 false alarm/ca → threshold để cân nhắc retrain

*Nếu đạt 100% cả 3 KR → set target quý sau cao hơn 1.5x. OKR không phải KPI — là la bàn.*

---

*Framework: OKRs by John Doerr · Google Chrome case (Sundar Pichai, 2008) · Leading/Lagging/Quality mix*
