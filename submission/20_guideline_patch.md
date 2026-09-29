# Guideline patch

- **Rule mới đề xuất:**
  1. **Quy định Tight-fit & Ngưỡng 40px:** Bắt buộc vẽ Bounding Box ôm khít điểm cực hạn của vật thể. Ngưỡng loại bỏ < 40px phải xét trên box ôm sát thực tế này. Nghiêm cấm việc vẽ nới lỏng box lấn vào background để ép vật thể vượt ngưỡng 40px.
  2. **Vẽ toàn bộ đối tượng:** Bounding box phải bao trọn tất cả các phần nhìn thấy của xe, tuyệt đối không khoanh cục bộ một bộ phận (như chỉ khoanh bánh xe sau).
  3. **Vật thể sát mép (Edge/Truncated) & Bị che khuất (Occluded):** Bắt buộc dán nhãn các đối tượng lấp ló ở mép ảnh (đánh dấu `truncated`) và các xe đỗ phía sau bị che khuất (đánh dấu `occluded`), nghiêm cấm bỏ sót.
  4. **Phân loại Truck/Car:** Cụ thể hóa định nghĩa: gán nhãn `Truck` cho các dòng xe chở hàng nhỏ (mini-truck, xe van/xe thùng); không gán `Car`.
  5. **Tách biệt người dắt xe:** Làm rõ lại: Người đi bộ đứng dưới đất đẩy/dắt xe phải vẽ tách rời thành `Pedestrian` và `Bike`. Chỉ gộp chung thành `Rider` khi đối tượng thực sự ngồi trên yên.
- **Áp dụng cho:** Tất cả các class (`Pedestrian`, `Bike`, `Truck`, `Car`, `ThreeWheeler`, `Rider`) và các thuộc tính `occluded`, `truncated`.
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** Luật hiện hành quá lỏng lẻo về độ khít của BBox tạo kẽ hở nới box ăn gian kích thước. Thiếu hướng dẫn cụ thể về việc phải bao trọn xe hay xử lý các ca vật thể ở sát mép, lấp ló phía sau. Đồng thời, không có định nghĩa rõ ràng để phân loại xe tải nhỏ so với xe con, và đội ngũ tạo Reference đang hoàn toàn hiểu sai luật gộp Rider khi dắt xe.
- **`rules_version` mới:** v1.1.0
- **Hiệu lực từ:** r2