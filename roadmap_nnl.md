# Roadmap Now / Next / Later — AI Nurse Assistant

> **Sản phẩm:** AI Nurse Assistant · SafeAge AI
> **Người thực hiện:** Hồ Hải Thuận · 2A202600058
> **Framework:** Problem-first · Không có ngày tháng cố định · La bàn, không phải hợp đồng

---

## NOW — Đang giải quyết ngay bây giờ

### Vấn đề 1 — Phát hiện ngã quá chậm, phòng tối không ai biết
**Vấn đề:** Điều dưỡng tại viện dưỡng lão chỉ tuần tra mỗi 1–2 giờ. Bệnh nhân ngã ban đêm phải nằm trên sàn trung bình 40–60 phút trước khi được phát hiện — dẫn đến biến chứng thứ phát nghiêm trọng và nguy cơ pháp lý cho cơ sở.

**Đang làm:** Tích hợp mô hình ST-GCN (skeleton-based fall detection) vào luồng RTSP từ camera IP hiện có. Gửi push notification đến app điều dưỡng trong < 30 giây khi phát hiện ngã. Hỗ trợ tối đa 20 camera/cơ sở trong phiên bản pilot.

---

### Vấn đề 2 — Không có bằng chứng sự cố khi bị khiếu nại
**Vấn đề:** Khi gia đình bệnh nhân khiếu nại, cơ sở y tế không có bằng chứng tự động về thời điểm xảy ra, ai phản ứng, và trong bao lâu. Hồ sơ thủ công dễ bỏ sót hoặc bị chỉnh sửa.

**Đang làm:** Tự động tạo báo cáo sự cố PDF (thời gian, phòng, loại sự cố, clip 10 giây) ngay khi cảnh báo được xác nhận. Dashboard lịch sử cho quản lý truy xuất và xuất báo cáo kiểm toán.

---

## NEXT — Giải quyết sau khi NOW hoàn thành

### Vấn đề 3 — Quản lý không biết pattern rủi ro của từng ca trực
**Vấn đề:** Sau khi tích lũy dữ liệu sự cố, câu hỏi tự nhiên của giám đốc viện dưỡng lão là: "Ca trực nào nguy hiểm nhất? Phòng nào hay xảy ra sự cố? AI đang sai ở đâu?" Nhưng hiện tại không có công cụ phân tích aggregated.

**Sẽ làm:** Analytics dashboard — thống kê sự cố theo ca trực, phòng, loại hành động. Sentiment/accuracy tracking để đội ngũ biết AI đang hoạt động ở mức nào.

---

### Vấn đề 4 — Mở rộng sang cơ sở thứ 2, 3 mà không cần onboarding thủ công
**Vấn đề:** Onboarding cơ sở mới hiện cần kỹ thuật viên cài đặt trực tiếp. Không thể scale B2B nếu mỗi deployment tốn 2–3 ngày onsite.

**Sẽ làm:** Self-serve onboarding flow — cơ sở tự thêm camera RTSP, tự cấu hình phòng và threshold qua giao diện web. Giảm thời gian onboarding từ 3 ngày xuống < 4 giờ.

---

## LATER — Tầm nhìn dài hạn (có thể bỏ nếu market không xác nhận)

### Vấn đề 5 — Phòng ngừa ngã trước khi xảy ra
**Vấn đề:** Phát hiện ngã là reactive — sự cố đã xảy ra rồi mới cảnh báo. Vision xa hơn là phân tích dáng đi (gait analysis) để nhận diện bệnh nhân có nguy cơ cao và cảnh báo điều dưỡng chủ động.

**Có thể làm:** Xây dựng gait risk scoring model từ skeleton data tích lũy. Cần tối thiểu 10.000 track dáng đi có nhãn từ môi trường thực tế VN — hiện chưa đủ. **Có thể bỏ nếu cost thu thập data quá cao.**

---

## Quy tắc áp dụng

| Quy tắc | Áp dụng |
|---|---|
| ❌ Không ngày tháng cố định | Không cam kết "tháng 8 launch" — chỉ thứ tự ưu tiên |
| ✅ Mỗi ô là vấn đề, không phải tính năng | "Phát hiện ngã quá chậm" → không phải "Xây dựng ST-GCN model" |
| ✅ LATER honest | Gait Prediction có thể bị cắt nếu data cost quá cao |
| ✅ NOW giới hạn 1–3 vấn đề | Tránh overcommit, focus toàn lực vào pilot |

---

*Framework: Now/Next/Later · Janna Bastow (ProdPad) · Ưu tiên từ RICE Matrix Workshop 1*
