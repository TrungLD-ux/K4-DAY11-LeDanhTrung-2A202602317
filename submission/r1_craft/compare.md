# So sánh L với R

Chỉ số L/R là thứ tự box cao ≥ H=40 trong từng frame, theo thứ tự XML; bắt đầu từ 1.
Box L trong ignore_region được báo IGNORE_SCOPE, không tính SPURIOUS.

## adasind_152940.jpg
- R5 mid MISSING
- R6 mid MISSING
## adasind_167700.jpg
- L7 mid IGNORE_SCOPE
- L8 mid IGNORE_SCOPE
- L4+R4 center WRONG_CLASS
- L6 mid SPURIOUS
- R2 mid MISSING
- R8 center MISSING
## adasind_212280.jpg

## Theo zone
| zone | n_ref | matched | missing | spurious |
|---|---|---|---|---|
| center | 10 | 8 | 2 | 1 |
| mid | 6 | 3 | 3 | 1 |
| edge | 2 | 2 | 0 | 0 |
