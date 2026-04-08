# Product Requirements Document (PRD)
# Dự án: Mộc Đạo Tu Tiên (Flora Cultivation)

> **Phiên bản:** 1.0  
> **Ngày tạo:** 2026-04-09  

---

## 1. Tổng quan sản phẩm

**Mộc Đạo Tu Tiên** là một sản phẩm IoT kết hợp Gamification, giúp người trồng cây tại nhà theo dõi môi trường sống của cây và nhận phản hồi dưới dạng điểm **Tu Vi (EXP)**. Sản phẩm gồm hai thành phần chính:

| Thành phần | Mô tả |
|---|---|
| **Thiết bị IoT** | Cắm vào chậu cây thật, đo Độ ẩm đất & Ánh sáng, gửi dữ liệu lên hệ thống |
| **Dashboard** | Giao diện để người dùng xem trạng thái cây, chỉ số môi trường, và điểm Tu Vi |

## 2. Đối tượng người dùng & Persona

### Persona: Người trồng cây tại nhà

| Thuộc tính | Mô tả |
|---|---|
| **Nhu cầu** | Muốn chăm sóc cây tốt hơn nhưng thiếu động lực hoặc thiếu kiến thức đánh giá môi trường |
| **Hành vi** | Kiểm tra cây không thường xuyên, dễ quên tưới nước hoặc điều chỉnh ánh sáng |
| **Kỳ vọng** | Hệ thống tự động đánh giá và cho phản hồi rõ ràng, dễ hiểu, có yếu tố thú vị |

## 3. Yêu cầu tính năng

### F-01: Đăng nhập & Xác thực

| Mục | Nội dung |
|---|---|
| **Mô tả** | Người dùng đăng nhập bằng tài khoản Google để truy cập hệ thống |
| **Đầu vào** | Tài khoản Google |
| **Đầu ra** | Phiên đăng nhập hợp lệ, truy cập Dashboard |

**User Stories:**
- Là người dùng, tôi muốn đăng nhập bằng Google để không cần tạo tài khoản riêng.
- Là người dùng, tôi muốn hệ thống ghi nhớ phiên đăng nhập để không phải đăng nhập lại mỗi lần mở.

---

### F-02: Liên kết chậu cây (Plant Code)

| Mục | Nội dung |
|---|---|
| **Mô tả** | Người dùng nhập Plant Code (in trên thiết bị IoT) để liên kết chậu cây với tài khoản |
| **Đầu vào** | Plant Code |
| **Đầu ra** | Chậu cây được gắn với tài khoản; Dashboard hiển thị dữ liệu cây |
| **Ràng buộc** | Mỗi tài khoản liên kết tối đa **1 chậu cây** |

**User Stories:**
- Là người dùng, tôi muốn nhập Plant Code để hệ thống biết chậu cây nào là của tôi.
- Là người dùng, tôi muốn được thông báo lỗi rõ ràng nếu Plant Code không hợp lệ hoặc đã được sử dụng.

---

### F-03: Đo lường môi trường

| Mục | Nội dung |
|---|---|
| **Mô tả** | Thiết bị IoT thu thập dữ liệu Độ ẩm đất và Ánh sáng, gửi lên hệ thống liên tục |
| **Chỉ số đo** | Độ ẩm đất, Ánh sáng |
| **Tần suất** | Liên tục theo chu kỳ (phút) |

**User Stories:**
- Là người dùng, tôi muốn xem chỉ số Độ ẩm đất và Ánh sáng hiện tại của cây trên Dashboard.

---

### F-04: Phân loại chất lượng môi trường

| Mục | Nội dung |
|---|---|
| **Mô tả** | Hệ thống so sánh dữ liệu thực tế với ngưỡng lý tưởng theo loại cây và phân loại chất lượng |
| **Các mức** | Rất tốt · Tốt · Bình thường · Xấu · Nguy hiểm |
| **Cơ sở** | Ngưỡng lý tưởng được cấu hình sẵn theo loại cây |

**User Stories:**
- Là người dùng, tôi muốn biết môi trường hiện tại của cây đang ở mức nào (tốt hay xấu) để biết có cần điều chỉnh không.

---

### F-05: Hệ thống Tu Vi (Điểm EXP)

| Mục | Nội dung |
|---|---|
| **Mô tả** | Điểm Tu Vi được tích lũy liên tục theo chất lượng môi trường mỗi chu kỳ |
| **Quy tắc** | Môi trường tốt → **cộng điểm**; Môi trường xấu/nguy hiểm → **trừ điểm** |
| **Tích lũy** | Điểm cộng dồn qua thời gian, phản ánh lịch sử chăm sóc tổng thể |

**User Stories:**
- Là người dùng, tôi muốn thấy tổng điểm Tu Vi của cây để biết mình chăm sóc tốt đến mức nào.
- Là người dùng, tôi muốn điểm Tu Vi tăng khi môi trường tốt và giảm khi môi trường xấu để có động lực cải thiện.

---

### F-06: Dashboard (Giao diện trạng thái)

| Mục | Nội dung |
|---|---|
| **Mô tả** | Giao diện hiển thị tổng quan trạng thái cây cho người dùng |

**Thông tin hiển thị:**

| # | Nội dung | Mô tả |
|---|---|---|
| 1 | Chỉ số môi trường | Giá trị Độ ẩm đất và Ánh sáng hiện tại |
| 2 | Đánh giá chất lượng | Mức phân loại môi trường hiện tại (Rất tốt → Nguy hiểm) |
| 3 | Tổng điểm Tu Vi | Tổng EXP tích lũy của cây |

**User Stories:**
- Là người dùng, tôi muốn mở Dashboard và thấy ngay 3 thông tin trên trong một giao diện dễ đọc.
- Là người dùng, tôi muốn đánh giá chất lượng được hiển thị trực quan (ví dụ: màu sắc, icon) để nắm bắt nhanh.

## 4. User Flow chính

```
┌─────────────┐
│  Mở ứng dụng│
└──────┬──────┘
       ▼
┌──────────────┐    Chưa       ┌─────────────────┐
│ Đã đăng nhập?├──────────────►│ Đăng nhập Google│
└──────┬───────┘               └────────┬────────┘
       │ Rồi                            │
       ▼                                ▼
┌───────────────────┐   Chưa   ┌────────────────────┐
│ Đã liên kết cây?  ├─────────►│ Nhập Plant Code    │
└──────┬────────────┘          └────────┬───────────┘
       │ Rồi                            │
       ▼                                ▼
┌──────────────────────────────────────────┐
│              DASHBOARD                   │
│                                          │
│  ┌────────────┐ ┌────────────┐ ┌───────┐ │
│  │ Độ ẩm đất  │ │ Ánh sáng   │ │Tu Vi  │ │
│  │   65%      │ │  1200 lux  │ │ 2450  │ │
│  └────────────┘ └────────────┘ └───────┘ │
│                                          │
│  Đánh giá: ● Tốt                         │
└──────────────────────────────────────────┘
```

## 5. Yêu cầu phi chức năng

| # | Yêu cầu | Mô tả |
|---|---|---|
| NF-01 | **Cập nhật gần thời gian thực** | Dashboard phản ánh dữ liệu cảm biến với độ trễ chấp nhận được |
| NF-02 | **Dễ sử dụng** | Giao diện đơn giản, trực quan, không cần hướng dẫn phức tạp |
| NF-03 | **Ổn định** | Thiết bị IoT hoạt động liên tục, không cần khởi động lại thường xuyên |

## 6. Ngoài phạm vi (Out of Scope)

Các tính năng sau **không** nằm trong phiên bản này:

- Quản lý nhiều chậu cây trên một tài khoản
- Hệ thống cảnh báo / thông báo đẩy (Push notification)
- Lịch sử dữ liệu cảm biến (biểu đồ theo thời gian)
- Bảng xếp hạng giữa các người dùng (Leaderboard)
- Điều khiển tự động (tự tưới nước, tự bật đèn)
- Hỗ trợ đa ngôn ngữ
