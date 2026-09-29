# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 10 | 2 | 1 | 2 | 3 | WRONG_CLASS (1) |
| mid | 6 | 3 | 1 | 2 | 3 | MISSING (3) |
| edge | 2 | 0 | 0 | 2 | 3 | — |

## Nhận xét

- Zone nào người (L) và model (M) gãy nhiều nhất, dẫn số ở bảng trên: Người (L) gãy nhiều nhất ở zone `mid` (L missing = 3 trên n_ref = 6, sai 50%). Model (M) gãy nặng nhất ở zone `edge` (M missing = 2 trên n_ref = 2, trượt 100%, kèm theo 3 ca M thừa/nhận diện giả).
- Giả thuyết vì sao (méo fisheye, box lỏng, thiếu `ego_body`, ...) và giới hạn của slice ba frame: Lỗi của L ở zone `mid` do Guideline lỏng lẻo phần tight-fit gây bất đồng khi ước lượng ngưỡng 40px; lỗi của M ở zone `edge` là do méo quang học fisheye ở rìa làm hỏng đặc trưng ảnh. Giới hạn của slice ba frame: Kích thước mẫu quá nhỏ, chỉ giúp chẩn đoán nguyên nhân lỗi cục bộ (error pattern) chứ không đại diện thống kê được tỷ lệ lỗi cho cả dự án.