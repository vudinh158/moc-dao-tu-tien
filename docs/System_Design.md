# Technical Design (System Design)
# Dự án: Mộc Đạo Tu Tiên (Flora Cultivation)

> **Cập nhật:** 2026-05-20

Tài liệu này tập trung vào các thông số kỹ thuật, mô hình dữ liệu và các thuật toán cốt lõi của hệ thống.

---

## 1. Kiến trúc dữ liệu (Database Schema)

### 1.1. Sơ đồ thực thể (ERD)

Hệ thống sử dụng PostgreSQL với các thực thể chính sau:

- **Users:** Thông tin định danh người dùng (Google OAuth).
- **Devices:** Quản lý thiết bị IoT qua `plant_code` và `verify_hash`.
- **Plants:** Trung tâm của hệ thống, liên kết User và Device, lưu trữ Tu Vi và Cảnh Giới.
- **SensorReadings:** Dữ liệu lịch sử cảm biến (Time-series).
- **ExpLogs & BreakthroughEvents:** Nhật ký thay đổi điểm số và cấp bậc.
- **Config (ExpConfig, RankConfig, Thresholds):** Các bảng cấu hình động.

### 1.2. Logic Cảnh Giới (Rank) mặc định

| # | Cảnh Giới | Tu Vi tối thiểu |
|---|-----------|----------------|
| 1 | Phàm Mộc | 0 |
| 2 | Luyện Khí | 100 |
| 3 | Trúc Cơ | 500 |
| 4 | Kim Đan | 1,500 |
| 5 | Nguyên Anh | 4,000 |
| 6 | Hóa Thần | 8,000 |
| 7 | Đại Thừa | 15,000 |
| 8 | Độ Kiếp | 30,000 |

---

## 2. Thuật toán & Logic cốt lõi

### 2.1. Cơ chế Anti-Spam & Tính điểm Tu Vi
Để đảm bảo công bằng, hệ thống giới hạn tần suất cộng điểm:
- **Chu kỳ tiêu chuẩn:** 60 giây/lần.
- **Dung sai (Grace Period):** 5 giây. 
- **Quy tắc:** Nếu `(now - last_exp_reward_time) < 55s`, hệ thống vẫn lưu dữ liệu cảm biến nhưng **không** thực hiện tính toán cộng/trừ Tu Vi.

### 2.2. Phân loại môi trường tổng hợp
Mức độ môi trường của cây được tính bằng mức **xấu nhất** trong tất cả các cảm biến hiện có:
- Thang đo: `EXCELLENT` (Tốt nhất) > `GOOD` > `FAIR` > `POOR` > `DANGER` (Xấu nhất).
- Ví dụ: Nếu độ ẩm là `GOOD` nhưng ánh sáng là `POOR` -> Mức tổng hợp là `POOR`.

### 2.3. Thuật toán Đột phá
Đột phá được kiểm tra ngay sau khi cộng điểm Tu Vi. Hệ thống cho phép "đột phá vượt cấp" nếu điểm Tu Vi tăng vọt vượt qua nhiều mốc cảnh giới trong một chu kỳ.

---

## 3. Giao diện lập trình (API Summary)

### 3.1. Thiết bị IoT (Device API)
- `POST /api/devices/{plant_code}/telemetry`: Gửi dữ liệu cảm biến.
  - Auth: `X-Plant-Code` trong Header.

### 3.2. Ứng dụng Web (Client API)
- **Auth:** `/api/auth/google`, `/api/auth/refresh`.
- **Plant:** 
  - `POST /api/plants/pair`: Liên kết thiết bị.
  - `GET /api/plants/me/dashboard`: Lấy trạng thái hiện tại.
  - `GET /api/plants/me/history`: Truy vấn biểu đồ.
  - `PUT /api/plants/me`: Đổi tên/loại cây.
- **Social:** `GET /api/leaderboard`: Bảng xếp hạng.

### 3.3. Quản trị (Admin API)
- `GET /api/admin/dashboard`: Thống kê hệ thống.
- `CRUD /api/admin/plant-types`: Quản lý ngưỡng lý tưởng.
- `GET/PUT /api/admin/exp-config`: Cấu hình game balance.
- `POST /api/admin/devices`: Cấp phát mã thiết bị mới (Provisioning).

---

## 4. Đặc tả Cảm biến (Key-Value)

Hệ thống lưu trữ dữ liệu theo dạng linh hoạt để dễ mở rộng:

| Cảm biến | Key | Đơn vị | Dải đo |
|---|---|---|---|
| Độ ẩm đất | `soil_moisture` | % | 0 - 100 |
| Ánh sáng | `light` | lux | 0 - 65535 |
| Nhiệt độ | `temperature` | °C | -40 - 80 |
| Độ ẩm KK | `humidity` | % | 0 - 100 |
