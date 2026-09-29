# Escalation ticket

## Ticket 1 [Escalated]

- **Frame:** adasind_152940.jpg
- **Ảnh chụp:** submission/screenshots/adasind_152940_R6.png
- **Expected impact:** Đánh giá sai lỗi MISSING cho Annotator. Gây nhiễu dữ liệu huấn luyện do bounding box vẽ quá lỏng lẻo.
- **Owner:** qa
- **Recommendation:** Yêu cầu QA xóa đối tượng R6 khỏi Reference vì kích thước thực tế nhỏ hơn 40px.
- **Status:** escalated

## Ticket 2 [Open]

- **Frame:** adasind_167700.jpg
- **Ảnh chụp:** submission/screenshots/adasind_167700_R2.png
- **Expected impact:** AI học sai đặc trưng của xe đạp.
- **Owner:** qa
- **Recommendation:** Sửa lại nhãn R2, bắt buộc bounding box phải bao trọn toàn bộ xe.
- **Status:** open

## Ticket 3 [Open]

- **Frame:** adasind_019560.jpg
- **Ảnh chụp:** submission/screenshots/adasind_019560_L1.png
- **Expected impact:** Mâu thuẫn trực tiếp với Guideline về phân loại hành vi.
- **Owner:** guideline
- **Recommendation:** Tách riêng nhãn Pedestrian và Bike khi dắt xe.
- **Status:** open

## Ticket 4 [Open]

- **Frame:** adasind_167700.jpg
- **Ảnh chụp:** submission/screenshots/adasind_167700_L4.png
- **Expected impact:** Gán sai phân loại class (Car thay vì Truck).
- **Owner:** guideline
- **Recommendation:** Cập nhật lại định nghĩa nhãn phân biệt giữa Truck và Car.
- **Status:** open