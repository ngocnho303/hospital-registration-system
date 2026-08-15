# HỆ THỐNG QUẢN LÝ ĐĂNG KÝ KHÁM BỆNH - BỆNH VIỆN NHÀ BÈ
> **Môn học:** Phân tích & Thiết kế Hệ thống Thông tin (PTTKHT)  
> **Dự án:** Phân tích & Thiết kế Hệ thống Đăng ký Khám bệnh tại Bệnh viện Nhà Bè

---

## TỔNG QUAN DỰ ÁN

Dự án tập trung nghiên cứu, phân tích và thiết kế **Hệ thống Quản lý Đăng ký Khám bệnh** nhằm tối ưu hóa quy trình tiếp nhận bệnh nhân, quản lý lịch khám của bác sĩ và tự động hóa khâu thanh toán/check-in.

Cơ sở dữ liệu của hệ thống được thiết kế theo chuẩn dạng chuẩn 3 (3NF) để loại bỏ dư thừa dữ liệu, đảm bảo tính toàn vẹn và tránh các dị thường khi thao tác (Insert/Update/Delete Anomalies).

---

## CẤU TRÚC TÀI LIỆU DỰ ÁN

Hồ sơ thiết kế hệ thống được tổ chức chi tiết theo 4 thư mục:

### 1. Thư mục 01: Yêu Cầu Hệ Thống (01-Requirements-Doc/)
* **Nội dung:** Chứa tài liệu báo cáo tổng hợp và đặc tả yêu cầu hệ thống (Requirements Specification), bao gồm yêu cầu chức năng và phi chức năng.
* **Chi tiết:** Xem tại [`01-Requirements-Doc/README.md`](./01-Requirements-Doc/README.md)

### 2. Thư mục 02: Mô Hình Sơ Đồ Nghiệp Vụ (02-Process-Models/)
* **Nội dung:** Chứa các sơ đồ mô hình hóa quy trình nghiệp vụ bao gồm  Biểu đồ Phân rã Chức năng (BFD), Biểu đồ luồng dữ liệu (DFD).
* **Chi tiết:** Xem tại [`02-Process-Models/README.md`](./02-Process-Models/README.md)

### 3. Thư mục 03: Mô Hình Dữ Liệu & CSDL (03-Data-Models/)
* **Nội dung:** Thiết kế Cơ sở dữ liệu logic bao gồm Biểu đồ Thực thể - Liên kết (ERD) và Mô hình Quan hệ (RD) đã chuẩn hóa 3NF.
* **Chi tiết:** Xem tại [`03-Data-Models/README.md`](./03-Data-Models/README.md)

### 4. Thư mục 04: Thiết Kế Giao Diện UI/UX (04-UI-UX-Prototypes/)
* **Nội dung:** Các bản vẽ mô phỏng giao diện người dùng tiêu biểu (UI/UX Mockups) từ Đăng nhập, Dashboard, Quản lý Bệnh nhân, Bác sĩ, Lịch làm việc, Lịch hẹn đến Thanh toán.
* **Chi tiết:** Xem tại [`04-UI-UX-Prototypes/README.md`](./04-UI-UX-Prototypes/README.md)

---

## TÓM TẮT KIẾN TRÚC HỆ THỐNG

* **Thực thể cốt lõi (7 thực thể):** `BENH_NHAN`, `NHAN_VIEN`, `BAC_SI`, `KHOA_KHAM`, `LICH_LAM_VIEC`, `LICH_HEN`, `THANH_TOAN`.
* **Luồng nghiệp vụ chính:**
  1. Đăng ký & Tra cứu thông tin hồ sơ Bệnh nhân.
  2. Quản lý Khoa khám & Lịch làm việc/Ca khám của Bác sĩ.
  3. Đặt lịch hẹn & Check-in lịch khám.
  4. Quản lý & Xử lý thanh toán chi phí khám bệnh.

---

## CÔNG CỤ SỬ DỤNG
* **ERDPlus / Draw.io**: Thiết kế sơ đồ nghiệp vụ (BPC, DFD) và mô hình thực thể - liên kết (ERD).
* **Figma**: Thiết kế và mô phỏng giao diện người dùng (UI/UX Mockups).
* **Claude AI**: Hỗ trợ chuẩn hóa dữ liệu mẫu (Mock Data) hiển thị trên giao diện và gợi ý bố cục thành phần (UI Layout) theo chuẩn UX.
