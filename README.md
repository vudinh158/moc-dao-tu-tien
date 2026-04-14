# 🌱 Mộc Đạo Tu Tiên (Flora Cultivation)

> **"Biến hành trình chăm sóc cây xanh thành con đường tu tiên đắc đạo."**

**Mộc Đạo Tu Tiên** là một hệ thống IoT kết hợp Gamification đột phá, giúp việc chăm sóc cây cảnh tại nhà không còn là một công việc nhàm chán mà trở thành một hành trình "Tu Tiên" đầy thú vị.

---

## 🌟 Tổng quan dự án

Dự án sử dụng các thiết bị IoT gắn trực tiếp vào chậu cây để thu thập dữ liệu môi trường (độ ẩm đất, ánh sáng, nhiệt độ...). Chất lượng chăm sóc cây thực tế sẽ được chuyển hóa trực tiếp thành điểm **Tu Vi (EXP)**.

- **Môi trường tốt:** Cây tích lũy Tu Vi, thăng cấp lên các **Cảnh Giới** cao hơn.
- **Môi trường xấu:** Cây bị tổn hao Tu Vi, thậm chí có thể "tẩu hỏa nhập ma" (giảm rank) nếu bị bỏ bê lâu ngày.

---

## ✨ Tính năng nổi bật

### 🌌 Hệ thống "Tu Tiên" (Gamification)
- **Tu Vi (EXP):** Tích lũy liên tục theo thời gian dựa trên các chỉ số môi trường sống.
- **Cảnh Giới (Rank):** Cây có thể đột phá qua các tầng thứ (Luyện Khí, Trúc Cơ, Kim Đan...) khi đủ Tu Vi.
- **Bảng Xếp Hạng:** So tài chăm sóc cây với các "đạo hữu" khác trên toàn hệ thống.

### 📡 Kết nối IoT Real-time
- **Đo lường chính xác:** Cảm biến độ ẩm đất và ánh sáng cập nhật dữ liệu liên tục.
- **Phân loại môi trường:** Đánh giá chất lượng sống của cây theo 5 mức (Tốt -> Nguy hiểm).
- **Cảnh báo thông minh:** Thông báo ngay trên Dashboard khi cây đang gặp tình trạng xấu hoặc thiết bị mất kết nối.

### 📊 Dashboard & Phân tích
- **Giao diện trực quan:** Hiển thị trạng thái cây bằng màu sắc và icon sinh động.
- **Biểu đồ xu hướng:** Theo dõi lịch sử thay đổi của môi trường và so sánh với ngưỡng lý tưởng.
- **Hồ sơ linh hoạt:** Dễ dàng đặt tên và thay đổi loại cây cho chậu cây đã liên kết.

### 🛠️ Quản trị tối ưu (Admin Suite)
- **Cấu hình động:** Admin có thể điều chỉnh ngưỡng lý tưởng, hệ số Tu Vi và mốc Cảnh Giới ngay trên UI.
- **Quản lý thiết bị:** Giám sát trạng thái hoạt động của toàn bộ thiết bị IoT trong hệ thống.

---

## 📂 Cấu trúc dự án

Toàn bộ dự án được chia thành các phân hệ chính sau, mỗi thư mục đều có `README.md` cấu hình riêng biệt:

- 📄 **[docs/](./docs/):** Lưu trữ tài liệu phân tích, kỹ thuật, và báo cáo (BRD, PRD, SRS, Hardware Spec).
- 🖥️ **[backend/](./backend/):** Mã nguồn Backend (RESTful API, Telemetry Xử lý, tính toán Tu Vi, Admin Suite).
- 🌐 **[frontend/](./frontend/):** Mã nguồn Frontend (Web App Gamification, Dashboard).
- 🔌 **[firmware/](./firmware/):** Mã nguồn IoT Firmware (đọc cảm biến, gửi dữ liệu, xác thực thiết bị).

---

## 🚀 Bắt đầu

1. **Kết nối:** Cắm thiết bị IoT vào chậu cây.
2. **Đăng ký:** Truy cập web app, đăng nhập bằng Google.
3. **Liên kết:** Nhập **Plant Code** và **Verify Code** được in trên thiết bị.
4. **Tu luyện:** Chăm sóc cây thật tốt để đạt đến đỉnh cao Mộc Đạo!

