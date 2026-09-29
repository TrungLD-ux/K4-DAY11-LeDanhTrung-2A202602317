# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| **r1, B3-center** (adasind_152940.jpg, adasind_167700.jpg) | Tổng 6 ca: 4 MISSING (2 do Annotator sót, 2 do Reference ép size/bọc thiếu), 1 SPURIOUS (Reference bỏ sót rìa), 1 WRONG_CLASS (Car/Truck). | Lát cắt này bộc lộ lỗ hổng hệ thống của Reference trong việc đánh giá ngưỡng 40px (vẽ nới lỏng box), khoanh thiếu bộ phận xe (chỉ khoanh bánh sau) và bỏ sót vật ở lề ảnh. Trực tiếp làm sai lệch đặc trưng học của AI. | Screenshot R6 (box 25x35.5px) ở frame 152940; Screenshot R2 (chỉ bọc bánh xe sau) ở frame 167700; Log `findings.csv`. |
| **calib, C0** (adasind_019560.jpg) | Tổng 2 ca: 2 SPURIOUS (Reference gộp sai Pedestrian/Bike thành Rider, bỏ sót xe occluded phía sau). | Lát cắt này vi phạm cốt lõi Guideline về định nghĩa hành vi (người dắt xe dưới đất). Nếu không review sớm và chấn chỉnh, AI sẽ hoàn toàn mất khả năng phân biệt giữa người đi bộ dắt xe và người đang điều khiển xe. | Screenshot frame 019560 (thể hiện rõ người áo đỏ đang đứng dưới đất dắt xe); Log `findings.csv` vòng calib. |

Giới hạn của kết luận từ ba frame ADASIND: Việc phân tích chỉ trên 3 frame (019560, 152940, 167700) tạo ra kích thước mẫu (sample size) quá nhỏ, không đại diện thống kê cho toàn bộ dataset. Kết luận ở đây chỉ giúp phát hiện các "mẫu hình lỗi hệ thống" (error patterns) của Reference để vá Guideline, chứ không thể dùng để ngoại suy hay tính toán tỷ lệ lỗi (error rate) tổng thể của toàn dự án.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv` (kể cả tránh đếm nhiều frame liền nhau trong cùng cảnh
như nhiều ca độc lập), và vì sao kế hoạch đó chỉ giúp tìm ca cần soi, chưa đo được tỷ lệ lỗi: 
- **Cách soát độ phủ:** Việc lấy mẫu phải đảm bảo tính phân tán trên nhiều điều kiện (thời tiết, ánh sáng, góc camera). Phải loại bỏ việc lấy các frame quá sát nhau về mặt thời gian (VD: 30 frame/giây) trong cùng một video, vì các frame liền kề chứa bối cảnh và đối tượng gần như y hệt nhau, không mang lại giá trị gia tăng về độ phủ thông tin (redundant data).
- **Vì sao chưa đo được tỷ lệ lỗi:** Kế hoạch này là dạng "lấy mẫu có chủ đích" (Targeted/Stratified Sampling) để đi tìm các ca biên (edge cases) và phơi bày lỗi, chứ không phải "lấy mẫu ngẫu nhiên" (Random Sampling). Để đo lường tỷ lệ lỗi thực tế một cách chính xác trên toàn cục, cần một tập mẫu ngẫu nhiên đủ lớn để tính toán khoảng tin cậy (Confidence Interval).