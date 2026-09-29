# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B3 | MISSING | 4 |
| center | B3 | SPURIOUS | 4 |
| center | B3 | WRONG_CLASS | 1 |
| center | C0 | SPURIOUS | 2 |
| edge | B3 | MISSING | 2 |
| edge | B3 | SPURIOUS | 3 |
| mid | B3 | MISSING | 7 |
| mid | B3 | SPURIOUS | 5 |

## Top defects
- SPURIOUS: 14 (ví dụ frame adasind_019560.jpg)
- MISSING: 13 (ví dụ frame adasind_152940.jpg)
- WRONG_CLASS: 1 (ví dụ frame adasind_167700.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy: Lỗi nổi bật nhất là hàng loạt ca bị đánh `MISSING` và `SPURIOUS` oan do chất lượng của Reference (mã `E0_reference_defect`). Cụ thể, Reference có xu hướng vi phạm quy tắc bounding box ôm khít (tight-fit) để cố ép các vật thể nhỏ lọt qua ngưỡng 40px (ví dụ: đối tượng `R6` ở frame `adasind_152940.jpg` kích thước thật chỉ 25x35.5px nhưng Reference tự nới lỏng để bắt lỗi MISSING). Ngoài ra, Reference làm ẩu ở vùng rìa (bỏ sót `L6` ở `adasind_167700.jpg` khiến nhãn đúng của Annotator bị báo SPURIOUS) và sai định nghĩa hành vi (gộp sai người dắt xe thành Bike ở `adasind_019560.jpg`).
- Cách sửa và ai nhận việc (`owner`): 
  + Cách sửa: QA phải rà soát và làm lại tập Reference, kiên quyết xóa bỏ các box < 40px (như R6) và bổ sung các vật thể lề (như L6). Đồng thời, cần vá Guideline để siết chặt quy định về độ tight-fit và phân biệt rõ hành vi "dắt xe" vs "lái xe".
  + Owner (Người nhận việc): QA (chịu trách nhiệm sửa Reference) và Guideline Owner (chịu trách nhiệm vá luật).
- Bằng chứng (ảnh trong `screenshots/`, dòng findings, rule): Ảnh chụp màn hình đo pixel thực tế của `R6` (25x35.5px) trong frame `adasind_152940.jpg`; ảnh người áo đỏ dắt xe ở `adasind_019560.jpg`; các dòng ghi nhận mã lỗi `E0_reference_defect` với action `keep_with_reason` trong `findings.csv`; và Rule quy định ngưỡng loại bỏ 40px trong Guideline.
