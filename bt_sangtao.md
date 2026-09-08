# [SÁNG TẠO] Thiết kế phân hệ "Yêu cầu Đổi trả & Hoàn tiền (Refund)"

---

## Phần 1 – Định nghĩa nghiệp vụ

### 3 Quy tắc nghiệp vụ cốt lõi

**Quy tắc 1: Thời hạn yêu cầu đổi trả**
Khách hàng chỉ được phép tạo yêu cầu đổi trả/hoàn tiền trong vòng **7 ngày** kể từ ngày nhận hàng (tính theo ngày hệ thống ghi nhận "Đã giao thành công"). Sau 7 ngày, hệ thống tự động từ chối và khóa chức năng tạo yêu cầu.

**Quy tắc 2: Bắt buộc cung cấp bằng chứng**
Khách hàng phải upload **ít nhất 1 video hoặc 3 ảnh** chụp sản phẩm lỗi/sai mô tả tại thời điểm bóc hàng. Yêu cầu không có bằng chứng hợp lệ sẽ bị từ chối tự động. Định dạng chấp nhận: MP4, MOV, JPG, PNG (tối đa 100MB).

**Quy tắc 3: RikkeiShop cử Shipper đến thu hồi hàng**
Sau khi yêu cầu hoàn tiền được duyệt, RikkeiShop sẽ chủ động cử Shipper đến địa chỉ của khách để **thu hồi hàng trong vòng 48 giờ làm việc**. Khách không cần tự gửi hàng ra bưu điện. Hoàn tiền chỉ được thực hiện sau khi hàng đã về đến kho và được kiểm định đạt yêu cầu.

---

### 1 Edge Case (Bẫy dữ liệu)

**Kịch bản: Hàng gửi về kho bị hỏng nặng do Shipper trong quá trình vận chuyển**

Khách hàng gửi yêu cầu hoàn tiền với lý do "hàng lỗi nhà sản xuất", video bóc hàng hợp lệ, yêu cầu được duyệt. Tuy nhiên, khi Shipper vận chuyển hàng từ nhà khách về kho, sản phẩm bị hỏng thêm do va đập trong quá trình vận chuyển. Nhân viên kho khi kiểm định phát hiện hàng bị hỏng nặng hơn mô tả ban đầu, không xác định được nguyên nhân.

**Xử lý:** Hệ thống yêu cầu Shipper cung cấp ảnh tình trạng hàng khi nhận tại nhà khách và khi giao về kho. Bộ phận nghiệp vụ xem xét và vẫn tiến hành hoàn tiền đầy đủ cho khách (vì khách không có lỗi), đồng thời ghi nhận sự cố để xử lý nội bộ với đơn vị vận chuyển.
