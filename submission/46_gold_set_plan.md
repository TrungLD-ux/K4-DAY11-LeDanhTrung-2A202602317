# Đề xuất gold set theo camera — tình huống giả lập

**Đầu bài:** 50.000 frame từ bốn camera SVM, ngân sách chọn 200 frame để review/gold. Đây là tình huống trên slide,
**không phải** 50.000 frame có trong repo. Phân bổ đúng 200 ở `45_sampling_plan.csv` cho bốn camera, mỗi camera có
normal và hard slice. “Gold set” ở đây là **kế hoạch tạo** reference sau kiểm chứng, không phải teaching reference
ADASIND hoặc nhãn bạn vừa vẽ. Nếu cần, dùng `notebooks/day11-svm360-colab.ipynb` để thử tổng phân bổ; notebook
không làm thay phần lý do.

| camera_id | Hard case cần chọn | Vì sao dễ sai | Annotation space / calibration cần giữ | Cách review trước khi gọi là gold |
|---|---|---|---|---|
| front | Xe tạt đầu ở ngã tư, ngược sáng (glare). | Box khó ôm khít (tight-fit) khi xe đang quay ngang; biến dạng quang học fisheye ở mép. | Giữ toạ độ gốc trên ảnh fisheye 2D; bảo lưu thông số biến dạng (distortion) để mapping sang BEV. | QA kiểm tra độ tight-fit bằng tay, đối chiếu luật bỏ qua vật thể < 40px. |
| rear | Xe máy lách lên bám sát đuôi xe. | Bị che khuất (occlusion) rất nặng, chỉ thấy một phần, dễ nhầm class hoặc bỏ sót. | Ảnh fisheye gốc, cần metadata chiều cao camera để nội suy khoảng cách. | Đối chiếu frame trước/sau (temporal) để xác minh định danh (identity) và loại xe. |
| left | Xe máy chạy song song vượt lên cắt qua vùng seam trái-trước. | Vật thể bị chia cắt, méo nặng ở lề, dễ sinh lỗi Duplicate ID hoặc sai zone (mid/edge). | Calibration vùng chồng lấp (seam) với camera front, đồng bộ timestamp. | Đặt frame trái và trước cạnh nhau (cùng timestamp) để rà soát sự thống nhất của Track ID. |
| right | Người đi bộ hoặc xe đạp đi sát lề phải, bị bóng râm che. | Vật thể quá nhỏ ở rìa ảnh, dễ bị phân loại nhầm hành vi hoặc biến mất đột ngột. | Tham số góc lắp đặt (pitch/yaw/roll) để chuẩn hóa kích thước trên mặt phẳng. | Soi kỹ bằng công cụ phóng to, đối chiếu policy xử lý vật thể ngoài mép (Outside). |

- Khi nào cần refresh gold set (đổi camera, calibration hoặc rule): Khi có sự thay đổi về phần cứng (đổi loại ống kính fisheye, thay đổi góc lắp đặt/calibration làm thay đổi độ méo ảnh), hoặc khi dự án cập nhật Guideline (đổi ngưỡng pixel, định nghĩa lại class hành vi như tách/gộp Rider/Pedestrian).
- Một ca seam/cross-camera cần policy và evidence trước khi ghép hai box: Khi một vật thể nằm ngay vùng chồng lấp (seam) xuất hiện đồng thời trên hai camera thành hai box khác nhau. Bằng chứng cần có: sự trùng khớp tuyệt đối về timestamp, thông số calibration chuẩn giữa hai camera. Policy cần xác định rõ output đích của model là gì (hợp nhất trên 3D/BEV hay để hệ thống sau tự ghép) để quyết định giữ 1 hay cả 2 box.
- Vì sao peer agreement hoặc quality report trên ảnh một camera chưa chứng minh gold set đúng cho cả bốn camera: Vì hệ thống SVM 360 yêu cầu tính nhất quán về không gian và ID giữa các góc nhìn. Hai người gán nhãn có thể đồng thuận 100% (peer agreement cao) trên từng luồng camera độc lập, nhưng khi ghép 4 camera lại thành góc nhìn chim bay (BEV), các box ở vùng seam có thể bị vênh toạ độ, đứt gãy Track ID hoặc sai lệch kích thước do không được review theo ngữ cảnh toàn cục (cross-camera).