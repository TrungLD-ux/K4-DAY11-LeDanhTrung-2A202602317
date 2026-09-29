# Exit ticket

Đọc `docs/10-svm360-reading-vi.md` trước khi trả lời câu 1–2. Các câu về zone, `why`, rework, parking và sampling
đã nằm trong file tương ứng nên không hỏi lại ở đây.

1. Một vật ở vùng seam giữa hai camera thật xuất hiện với hai box khác nhau: đó là lỗi `DUPLICATE` hay cần một quy
   tắc riêng? Vì sao?
   - **Trả lời:** Không có đáp án chuẩn tuyệt đối, nhưng trường hợp này **cần một quy tắc riêng** thay vì coi tự động coi là lỗi `DUPLICATE`.
   - **Vì sao:** Theo tài liệu, 4 camera quanh xe có vùng nhìn chồng lên nhau (seam). Một vật ở đây hoàn toàn có thể xuất hiện "đồng thời trên hai camera, với hai hộp khác nhau, hai zone bán kính khác nhau". Hệ thống thực tế phải có quy tắc riêng để "quyết định: giữ box nào, hợp nhất ra sao, hay giữ cả hai và để tầng sau xử lý" chứ không thể tự động xoá đi 1 box.

2. Một vật đi qua nhiều frame trên cùng camera: khi nào giữ cùng track ID, khi nào thêm keyframe hoặc trạng thái
   Outside? Nêu bằng chứng sẽ cần trước khi nối track qua hai camera.
   - **Trên cùng camera:**
     - **Giữ cùng track ID (identity):** Khi vật thể đó vẫn còn quan sát được.
     - **Thêm keyframe:** Khi đối tượng có sự "thay đổi hình học lớn".
     - **Trạng thái Outside:** Khi "vật ra khỏi trường nhìn".
   - **Bằng chứng để nối track qua hai camera:** Hai camera có thể thấy cùng một vật ở vùng chồng nhưng không tự ghép track. Các bằng chứng cần thiết trước khi nối là: "timestamp, calibration và policy về output đích".

3. Nhìn lại cả buổi: một chỗ bạn tin nhãn mình đúng nhưng reference hoặc người soát nghĩ khác (dẫn frame/`object_ref`),
   bạn đã xử lý thế nào, và nếu làm lại slice này bạn sẽ đổi gì trong cách làm?
   - **Chỗ tôi tin mình đúng:** Tại frame `adasind_152940.jpg` (đối tượng `R6` - ThreeWheeler), Reference đánh lỗi MISSING. Nhưng tôi vẽ box ôm khít thì kích thước chỉ là 25x35.5px (< 40px), theo luật là phải bỏ qua, do Reference tự nới lỏng box sai luật để vượt ngưỡng. Hoặc frame `adasind_167700.jpg` (đối tượng `R2` - Bike), Reference vẽ sai khi chỉ bọc mỗi cái bánh xe sau.
   - **Cách xử lý:** Tôi dùng mã `E0_reference_defect` trong `findings.csv` để giữ vững lập trường (action: `keep_with_reason`). Đồng thời, ghi lỗi này vào `30_escalation_ticket.md` để báo cáo QA.
   - **Nếu làm lại:** Tôi sẽ kiểm tra kích thước (pixel) của các vật thể ở xa bằng cách vẽ box khít ngay từ đầu để đối chiếu ngưỡng 40px, tránh việc nhìn bằng mắt thường dễ bị nhầm lẫn, và chủ động soi kỹ các vật thể sát mép (edge) để không bị sót.