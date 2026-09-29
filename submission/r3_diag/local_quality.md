# Đối chiếu chất lượng cục bộ — rectangle

Teaching reference, không phải gold set đã phê duyệt; không có điểm đạt tự động.
Nguồn: export r1_craft đã khóa SHA256 `09b0fdb3d880991b121e2e4ac559d15f4be20bc16f203543cba69f7fb5e4c8fe`; slice `B3-center`.
Ghép hình học greedy một-một theo IoU ≥ 0.50, rồi so class; H ≥ 40 px.
Box trái nằm chủ yếu trong ignore_region reference không tính. Polygon, polyline, track không được chấm.
Đây là phép tính offline của lab, không phải báo cáo hay kết quả tương đương CVAT Premium.

Frame được tính: adasind_152940.jpg, adasind_167700.jpg, adasind_212280.jpg. Frame thiếu trong export: không.
TP=13; FP=2; FN=5; số lần đối chiếu=19; mean IoU của TP=0.819.

| Chỉ số | Micro | Macro | Nhãn thấp nhất |
|---|---:|---:|---:|
| accuracy | 0.684 | 0.939 | 0.842 |
| precision | 0.867 | 0.694 | 0.000 |
| recall | 0.722 | 0.646 | 0.000 |
| jaccard | 0.650 | 0.601 | 0.000 |
| dice | 0.788 | 0.667 | 0.000 |

| Nhãn | TP | FP | FN | Accuracy | Precision | Recall | Jaccard | Dice |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bike | 7 | 0 | 1 | 0.947 | 1.000 | 0.875 | 0.875 | 0.933 |
| Bus | 1 | 0 | 0 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 |
| Car | 0 | 0 | 1 | 0.947 | 0.000 | 0.000 | 0.000 | 0.000 |
| Pedestrian | 2 | 0 | 0 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 |
| ThreeWheeler | 1 | 1 | 1 | 0.895 | 0.500 | 0.500 | 0.333 | 0.500 |
| Truck | 2 | 1 | 2 | 0.842 | 0.667 | 0.500 | 0.400 | 0.571 |

| Frame | TP | FP | FN | Accuracy | Precision | Recall |
|---|---:|---:|---:|---:|---:|---:|
| adasind_152940.jpg | 4 | 0 | 2 | 0.667 | 1.000 | 0.667 |
| adasind_167700.jpg | 6 | 2 | 3 | 0.600 | 0.750 | 0.667 |
| adasind_212280.jpg | 3 | 0 | 0 | 1.000 | 1.000 | 1.000 |

Confusion matrix: hàng = teaching reference; cột = export đã khóa.
`<missing>` là thiếu box; `<extra>` là box thừa. Xem `local_quality_confusion.csv`.

| Reference \ Export | Bike | Bus | Car | Pedestrian | ThreeWheeler | Truck | <missing> |
|---|---:|---:|---:|---:|---:|---:|---:|
| Bike | 7 | 0 | 0 | 0 | 0 | 0 | 1 |
| Bus | 0 | 1 | 0 | 0 | 0 | 0 | 0 |
| Car | 0 | 0 | 0 | 0 | 0 | 1 | 0 |
| Pedestrian | 0 | 0 | 0 | 2 | 0 | 0 | 0 |
| ThreeWheeler | 0 | 0 | 0 | 0 | 1 | 0 | 1 |
| Truck | 0 | 0 | 0 | 0 | 0 | 2 | 2 |
| <extra> | 0 | 0 | 0 | 0 | 1 | 0 | 0 |

Chi tiết xung đột trong `local_quality_conflicts.csv`; dữ liệu máy đọc trong `local_quality.json`.
Mismatching label đóng góp một FP cho class vẽ và một FN cho class reference; attribute khác được báo riêng.
Micro accuracy đếm mỗi cặp ghép sai class là một lần đối chiếu; Jaccard đếm cả FP và FN.
Macro/worst bỏ nhãn không xuất hiện ở cả hai phía; chỉ số không có mẫu là N/A.
