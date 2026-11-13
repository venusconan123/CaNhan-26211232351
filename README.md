# Men Hair Booking — Báo cáo tiến độ lần 2

**Đề tài:** Xây dựng hệ thống quản lý và đặt lịch dịch vụ làm đẹp nam tích hợp thanh toán trực tuyến.

**Mã sinh viên:** 26211232351

**GVHD:** ThS. Trần Thị Thanh Lan

**Cập nhật tiến độ:** 13/11/2026

**Mốc kiểm tra lần 2:** 17:00 ngày 14/11/2026, giờ Việt Nam.

Ứng dụng Flutter cho khách hàng, nhân viên và quản trị viên, sử dụng Firebase
Authentication/Cloud Firestore thật và backend Cloudflare Worker online.
Bản này là bản demo đồ án; VNPAY dùng môi trường Sandbox, không thu tiền thật.

## Tiến độ theo bốn mốc của khoa

| Lần | Mốc kiểm tra | Nội dung và trạng thái |
| --- | --- | --- |
| 1 | 31/10/2026 — 17:00 | Đã nộp nền tảng Flutter/Firebase; tài khoản khách, xác minh email, hồ sơ, danh mục dịch vụ, mẫu tóc và thông tin salon. Giữ nguyên hai commit cũ, bản source tại `7cc8f1b`. |
| 2 | 14/11/2026 — 17:00 | Cập nhật bản hiện tại: đặt lịch, quản trị, nhân viên, phân ca, phục vụ, ghi nhận thanh toán, thống kê, bản đồ, đánh giá thật và trợ lý AI. VNPAY Sandbox đang chờ hỗ trợ lỗi 71. |
| 3 | 28/11/2026 — 17:00 | Dự kiến kiểm thử nhiều vai trò trên Firebase thật, xử lý tích hợp VNPAY, kiểm thử và hoàn thiện APK Android. |
| 4 | 05/12/2026 — 17:00 | Dự kiến sửa lỗi cuối, kiểm thử hồi quy, chốt APK, hướng dẫn sử dụng và kịch bản bàn giao/demo. |

## Nội dung đã hoàn thiện trong lần 2

### Khách hàng

- Đăng ký, đăng nhập, xác minh email, quên mật khẩu và cập nhật hồ sơ.
- Xem dịch vụ, giá/thời lượng, nhân viên, mẫu tóc và thông tin các chi nhánh.
- Đặt lịch theo chi nhánh, dịch vụ, thợ và giờ còn trống; backend kiểm tra ca,
  thời lượng và lịch hẹn khác để chặn trùng giờ.
- Chọn thanh toán tại salon hoặc mở cổng VNPAY Sandbox; theo dõi, hủy lịch theo điều kiện.
- Voucher, tích lũy, thông báo, đánh giá và chat hỗ trợ với admin.
- Xem chi nhánh trên bản đồ và mở Google Maps để chỉ đường.
- Trợ lý AI tư vấn dịch vụ, chuyên môn nhân viên và giờ trống từ dữ liệu Firebase;
  không tự đặt lịch hoặc tự xác nhận có chỗ khi chưa tra cứu.

### Nhân viên

- Admin tạo tài khoản email gắn với đúng hồ sơ và chi nhánh; chặn email đã sử dụng.
- Đăng nhập vào tab Lịch làm; xem lịch hẹn được giao và đổi mật khẩu.
- Bắt đầu phục vụ sớm trong cùng ngày khi khách đã đến, đang trong ca và không
  chồng lịch khác; không phục vụ hai khách đồng thời. Lưu riêng giờ bắt đầu thực tế.
- Xác nhận hoàn thành dịch vụ. **Với lịch thanh toán tại quầy, xác nhận hoàn thành
  cũng xác nhận đã nhận đủ tiền**, tự ghi nhận thanh toán và cập nhật thống kê.
  Giữ nguyên khoản đã thanh toán online; thao tác lặp không tạo thêm khoản thu.
- Lọc lịch theo hôm nay, 7 ngày, 30 ngày, một ngày và khoảng ngày.
- Thống kê cá nhân theo ngày hẹn giờ Việt Nam, tách giá trị dịch vụ và số đã thanh toán.

### Quản trị viên

- Quản lý lịch hẹn, dịch vụ, nhân viên, mẫu tóc, hotline, voucher, tích lũy,
  thông báo, tin nhắn và báo cáo.
- Quản lý tài khoản nhân viên theo ba chi nhánh; phân ca tháng, OFF và đổi ca,
  bao gồm đổi giữa hai nhân viên trong cùng ngày, có kiểm tra xung đột/lịch khách.
- Xem dashboard theo hôm nay, 7 ngày, 30 ngày, ngày tùy chọn, khoảng ngày hoặc tất cả.
  Dashboard hiện lọc theo **ngày tạo lịch**; màn hình có chú thích để phân biệt với
  thống kê nhân viên lọc theo **ngày hẹn**.
- Xem biên nhận tự ghi khi hoàn thành; vẫn ghi nhận thu tiền cho lịch cũ đã hoàn thành
  nhưng chưa thanh toán sau khi đối chiếu đã nhận tiền.
- Điểm và số lượt đánh giá tính từ đánh giá hợp lệ gắn với lịch hoàn thành;
  admin không nhập tay số liệu này.

## Vấn đề đang chờ hỗ trợ: VNPAY Sandbox

**Trạng thái tại lần nộp 2: chưa xác nhận thanh toán thành công qua cổng Sandbox hiện tại.**

- Đã tích hợp tạo URL thanh toán, ký HMAC-SHA512, Return URL và IPN.
- Đã đối chiếu URL backend thực tế: `vnp_TmnCode` trùng mã trong email VNPAY cấp.
- Khi mở cổng thanh toán, VNPAY trả **lỗi 71: “Website này chưa được phê duyệt”**.
- Đang chờ VNPAY hỗ trợ kiểm tra trạng thái terminal/website. Chưa có bằng chứng
  mã đã hết hạn, và không tự thay sang mã website khác.
- Chưa ghi nhận lỗi này là đã sửa; kết quả unit test không thay thế một giao dịch
  Sandbox thành công. Không tự đánh dấu `paid` cho giao dịch online đang lỗi.
- Luồng thanh toán tại salon và tự ghi nhận khi hoàn thành vẫn dùng được cho demo.

Cấu hình và hướng dẫn xử lý: [VNPAY_SETUP.md](VNPAY_SETUP.md).


