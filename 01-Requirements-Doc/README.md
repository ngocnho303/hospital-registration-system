#  HỆ THỐNG QUẢN LÝ ĐĂNG KÝ KHÁM CHỮA BỆNH TRỰC TUYẾN
> **Bệnh viện Huyện Nhà Bè**

---

##  TỔNG QUAN DỰ ÁN

Thư mục này chứa toàn bộ **Tài liệu Phân tích và Thiết kế Hệ thống (bản PDF)** cho dự án **Quản lý Đăng ký Khám chữa bệnh Trực tuyến** tại Bệnh viện Đa khoa Nhà Bè.
Hệ thống được thiết kế nhằm tối ưu hóa quy trình tiếp nhận bệnh nhân, hỗ trợ bệnh nhân mới (chưa có mã HIS) đăng ký trực tuyến, tự động xác thực BHYT và liên thông dữ liệu hai chiều với Hệ thống Thông tin Bệnh viện (HIS).

---

##  TÀI LIỆU BÁO CÁO

* **[Xem / Tải về Tài liệu Báo cáo Đầy đủ (PDF)](./System_Documentation.pdf)** 

---

##  NỘI DUNG CHÍNH TRONG BÁO CÁO

## 1. Khảo Sát Hiện Trạng & Đề Xuất Hệ Thống Mới

### Kết quả khảo sát thực tế
* **Thời gian thực hiện:** 5 ngày (29/06/2026 – 03/07/2026) trên 138 lượt bệnh nhân trực tiếp.
* **Thời gian tiếp nhận:**
  * Bệnh nhân mới chưa có mã HIS: **~6 phút 30 giây** tại quầy.
  * Bệnh nhân đăng ký trước: **~2 phút 05 giây**.
  * *Rủi ro:* Bệnh nhân bỏ về nếu thời gian chờ kéo dài trên 25 phút.
* **Tỷ lệ bệnh nhân mới:** Ghi nhận khoảng **62%** (ở ca khảo sát đầu tiên) chưa có mã bệnh nhân trên hệ thống HIS, phải khai báo thủ tục trực tiếp.
* **Xác thực BHYT & Chi phí:** 
  * 100% trường hợp BHYT phải kiểm tra thủ công.
  * 19% ca phải tra cứu/nhập lại thông tin do sai sót thẻ hoặc định danh.
  * Chưa hỗ trợ thông báo chi phí khám dự kiến trước khi đăng ký.
* **Điểm nghẽn chính:** Quá tải cục bộ giờ cao điểm (7:00 – 9:30 sáng), nhập liệu thủ công lặp đi lặp lại, nền tảng YouMed hiện tại chỉ hỗ trợ bệnh nhân cũ đã có mã HIS.

### Đề xuất giải pháp
* Xây dựng nền tảng đăng ký trực tuyến hỗ trợ cả bệnh nhân mới và cũ chọn trước khoa, bác sĩ, ngày và ca khám.
* Tự động xác thực thẻ BHYT và quyền lợi hưởng qua Cổng Giám định BHYT (BHXH Việt Nam).
* Tích hợp đồng bộ dữ liệu 2 chiều với HIS (cấp mới/trả về `MaBenhNhanHIS`, số tiếp nhận, STT khám).
* Áp dụng **28 Quy tắc nghiệp vụ** (BR01 - BR28) và **07 Nguyên tắc nghiệp vụ** (NP01 - NP07).

---

## 2. Phân Tích & Mô Hình Hóa Hệ Thống (SADT)

### Biểu đồ Phân rã Chức năng (BPC)
Hệ thống gồm **5 phân hệ chức năng lớn** và **20 chức năng lá**:

* **1.0 Quản lý hồ sơ bệnh nhân:** 1.1 Tra cứu | 1.2 Tiếp nhận mới | 1.3 Khởi tạo.
* **2.0 Đồng bộ danh mục khám:** 2.1 Đồng bộ bác sĩ | 2.2 Đồng bộ lịch làm việc | 2.3 Đồng bộ khoa khám
* **3.0 Quản lý đăng ký lịch khám:** 3.1 Đăng ký | 3.2 Thanh toán | 3.3 Phát hành phiếu điện tử | 3.4 Thay đổi lịch | 3.5 Hủy lịch | 3.6 Tra cứu lịch sử | 3.7 Nhắc lịch | 3.8 Đồng bộ trạng thái khám
* **4.0 Quản lý tiếp nhận bệnh nhân:** 4.1 Tiếp nhận | 4.2 Xác minh thông tin | 4.3 Cấp mã và phiếu khám
* **5.0 Giám sát và báo cáo:** 5.1 Giám sát lưu lượng | 5.2 Báo cáo doanh thu | 5.3 Báo cáo theo khoa

### Luồng Dữ liệu & Tác động Dữ liệu
* **Ma trận Thực thể - Chức năng:** Đánh giá mức độ tác động (Create, Read, Update) của các chức năng lá lên 6 hồ sơ dữ liệu chính (D1 – D6).
* **DFD:** Xây dựng từ Mức ngữ cảnh (Context Diagram), Mức 0 đến 5 sơ đồ DFD Mức 1 đại diện cho 5 phân hệ.

---

## 3. Thiết Kế Cơ Sở Dữ Liệu & Mô Hình Quan Hệ

### Sơ đồ Thực thể Liên kết (ERD)
Bao gồm 7 thực thể chính: `BENH_NHAN`, `NHAN_VIEN`, `LICH_HEN`, `KHOA_KHAM`, `BAC_SI`, `LICH_LAM_VIEC`, `THANH_TOAN`.

### Mô hình Quan hệ (RD - Chuẩn hóa 3NF)

| Bảng | Các trường dữ liệu (<u>PK</u> Khóa chính, **FK** Khóa ngoại) |
| :--- | :--- |
| **BENH_NHAN** | <u>(PK) MaBN</u>, HoTen, NgaySinh, GioiTinh, CCCD, SoDienThoai, DiaChi, SoTheBHYT, TyLeHuongBHYT, MaBNHIS, TrangThaiHoSo |
| **NHAN_VIEN** | <u>(PK) MaNhanVien</u>, HoTen, ChucVu, SoDienThoai, Email, TrangThaiLamViec |
| **LICH_HEN** | <u>(PK) MaLichHen</u>, LoaiHinhKham, NgayDangKy, TrangThaiLichHen, MaQR, **(FK) MaBN**, **(FK) MaNhanVien**, **(FK) MaLichLamViec** |
| **KHOA_KHAM** | <u>(PK) MaKhoa</u>, TenKhoa, MoTa, MucPhiKham, TrangThai |
| **BAC_SI** | <u>(PK) MaBS</u>, HoTenBS, HocHamHocVi, TrangThai, **(FK) MaKhoa** |
| **LICH_LAM_VIEC** | <u>(PK) MaLichLamViec</u>, NgayKham, CaKham, GioBatDau, GioKetThuc, SoLuongToiDa, TrangThaiLich, **(FK) MaBS** |
| **THANH_TOAN** | <u>(PK) MaThanhToan</u>, NgayThanhToan, ChiPhiDuKien, PhuongThucThanhToan, TrangThaiThanhToan, **(FK) MaLichHen** |

---

## 4. Thiết Kế Giao Diện Người Dùng (Mockup)

Hệ thống thiết kế 11 màn hình giao diện Web/Admin chính:

1. Giao diện Đăng nhập
2. Giao diện Trang chủ (Dashboard)
3. Giao diện Quản lý bệnh nhân
4. Giao diện Thêm bệnh nhân mới
5. Giao diện Quản lý bác sĩ
6. Giao diện Thêm bác sĩ mới
7. Giao diện Quản lý khoa khám
8. Giao diện Quản lý lịch làm việc
9. Giao diện Thêm lịch làm việc mới
10. Giao diện Quản lý lịch hẹn
11. Giao diện Quản lý thanh toán
