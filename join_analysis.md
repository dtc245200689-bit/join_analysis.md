# Giải trình: Tại sao chọn COUNT(o.order_id) thay vì COUNT(*)

Trong câu lệnh `LEFT JOIN`, khi một khách hàng chưa mua hàng (như Charlie), toàn bộ các cột kế thừa từ bảng phụ `Orders` sẽ nhận giá trị `NULL`.

- Nếu dùng `COUNT(*)`, hàm sẽ đếm tổng số dòng được tạo ra trong kết quả tạm. Vì dòng chứa Charlie vẫn tồn tại, hệ thống sẽ tính là `1`, dẫn đến sai lệch thông tin nghiêm trọng (Charlie chưa mua gì nhưng báo cáo ghi có 1 đơn).
- Nếu dùng `COUNT(o.order_id)`, hàm COUNT sẽ chủ động bỏ qua tất cả các giá trị `NULL` trên cột chỉ định. Nhờ vậy, kết quả trả về cho khách hàng chưa phát sinh giao dịch sẽ hiển thị chính xác bằng `0`.
