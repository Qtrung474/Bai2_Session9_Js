# Phân tích lỗi & Bảng Test Cases (Bài 2)

## Phân tích lỗi
Trong đoạn mã trên có 3 lỗi sai logic nghiệp vụ:
1. **Lỗi truy cập thuộc tính bằng tên biến (`bookingReservation.priceKey`):**
   - **Nguyên nhân kỹ thuật:** Tương tự như bài 1, toán tử dấu chấm (`.`) sẽ tìm chính xác thuộc tính có tên là "priceKey", kết quả trả về `undefined` thay vì tìm thuộc tính "roomPrice". Kéo theo việc tính toán `earlySurcharge` và `totalAmount` trả về `NaN`.
   - **Cách khắc phục:** Đổi thành Bracket Notation: `bookingReservation[priceKey]`.
2. **Lỗi xóa thuộc tính không hoàn toàn (`bookingReservation.discountCode = undefined`):**
   - **Nguyên nhân kỹ thuật:** Gán giá trị `undefined` chỉ làm thay đổi giá trị của thuộc tính `discountCode` chứ không hề xóa bỏ thuộc tính đó khỏi đối tượng. Thuộc tính vẫn tồn tại trong đối tượng (khi kiểm tra `'discountCode' in bookingReservation` vẫn trả về `true`), điều này có thể gây lỗi logic khi ứng dụng kiểm tra xem thuộc tính có tồn tại hay không.
   - **Cách khắc phục:** Cần sử dụng toán tử `delete` để xóa hoàn toàn: `delete bookingReservation.discountCode;`.
3. **Lỗi duyệt vòng lặp (`bookingReservation.key`):**
   - **Nguyên nhân kỹ thuật:** Trong vòng lặp `for...in`, biến `key` đại diện cho tên các thuộc tính dưới dạng chuỗi (được lấy ra một cách linh động qua mỗi lần lặp). Việc sử dụng `bookingReservation.key` có nghĩa là liên tục tìm kiếm thuộc tính tên chữ "key" trong đối tượng, dẫn đến việc luôn trả về `undefined`.
   - **Cách khắc phục:** Phải sử dụng Bracket Notation: `bookingReservation[key]` để lấy giá trị của thuộc tính tương ứng với tên biến `key`.

## Bảng Test Cases

| Trường hợp kiểm thử | Dữ liệu đầu vào | Kết quả sai thực tế (khi có lỗi) | Kết quả đúng mong đợi |
| :--- | :--- | :--- | :--- |
| Hủy mã Voucher không hợp lệ | `isVoucherValid = false`, `discountCode` đang có trong object | Thuộc tính chỉ bị đổi thành undefined, kiểm tra `'discountCode' in bookingReservation` trả về `true` | Thuộc tính bị xóa hoàn toàn, `'discountCode' in bookingReservation` trả về `false` |
| In ra toàn bộ thông tin đối tượng bằng vòng lặp | Đối tượng `bookingReservation` có các thuộc tính | Vòng lặp in ra giá trị của mọi thuộc tính là `undefined` | Vòng lặp in ra đúng tên thuộc tính và giá trị thực tế của thuộc tính đó |
