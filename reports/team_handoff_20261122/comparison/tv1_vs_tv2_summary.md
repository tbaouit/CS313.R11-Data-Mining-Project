# So sánh TV1 vs TV2 vs paper (K1-POI, seed 42)

Nguồn: `tv1_vs_tv2_vs_paper.csv` (30 dòng = 3 dataset × 2 biến thể × 5 metric). Δ tính bằng điểm phần trăm (pp), dương nghĩa là số đo được cao hơn.

## 1. Kết luận chính

1. **TV1 và TV2 trùng khớp hoàn toàn:** cả 30 metric test giống nhau đến 4 chữ số thập phân (chênh lệch tối đa 0.00 pp). Ngoài ra, toàn bộ lịch sử huấn luyện 100 epoch của 3 dataset, epoch tốt nhất (NYC 65, CA 91, TKY 99), cấu hình reranker tìm được và metric val đều giống nhau. File `training_history.csv` của hai người giống nhau từng byte.
2. **Ý nghĩa:** cùng code, cùng dữ liệu (sha256 trùng), cùng seed 42 thì quy trình cho ra kết quả như nhau dù chạy ở phiên Kaggle khác, GPU khác (cuda:0 và cuda:1) và có chạy song song. Điều này xác nhận *khả năng tái lập*, nhưng **không cho biết độ dao động giữa các seed**, vì hai bên dùng chung seed. Muốn đo độ dao động cần chạy seed khác (ví dụ 0 và 1).
3. **So với paper:** chênh lệch rất nhỏ. Trung bình |Δ| = 0.16 pp trên 30 metric, lớn nhất là 0.69 pp (CA, w/o reranker, Acc@1: 0.1608 so với 0.1539).
4. **Tác dụng của reranker** có cùng xu hướng với paper: Acc@1 và MRR tăng ở cả 3 dataset (xem mục 3).

## 2. Kết quả test theo từng dataset

### CA

**K1-POI w/o Reranker**

| | Acc@1 | Acc@5 | Acc@10 | Acc@20 | MRR |
|---|---|---|---|---|---|
| Paper | 0.1539 | 0.3465 | 0.4342 | 0.5178 | 0.2472 |
| TV1 | 0.1608 | 0.3474 | 0.4351 | 0.5200 | 0.2527 |
| TV2 | 0.1608 | 0.3474 | 0.4351 | 0.5200 | 0.2527 |
| TV2 − TV1 (pp) | +0.00 | +0.00 | +0.00 | +0.00 | +0.00 |
| TV1 − paper (pp) | +0.69 | +0.09 | +0.09 | +0.22 | +0.55 |
| TV2 − paper (pp) | +0.69 | +0.09 | +0.09 | +0.22 | +0.55 |

**K1-POI**

| | Acc@1 | Acc@5 | Acc@10 | Acc@20 | MRR |
|---|---|---|---|---|---|
| Paper | 0.1739 | 0.3576 | 0.4442 | 0.5242 | 0.2632 |
| TV1 | 0.1777 | 0.3602 | 0.4438 | 0.5280 | 0.2663 |
| TV2 | 0.1777 | 0.3602 | 0.4438 | 0.5280 | 0.2663 |
| TV2 − TV1 (pp) | +0.00 | +0.00 | +0.00 | +0.00 | +0.00 |
| TV1 − paper (pp) | +0.38 | +0.26 | -0.04 | +0.38 | +0.31 |
| TV2 − paper (pp) | +0.38 | +0.26 | -0.04 | +0.38 | +0.31 |

### NYC

**K1-POI w/o Reranker**

| | Acc@1 | Acc@5 | Acc@10 | Acc@20 | MRR |
|---|---|---|---|---|---|
| Paper | 0.2129 | 0.5148 | 0.6397 | 0.7303 | 0.3496 |
| TV1 | 0.2105 | 0.5166 | 0.6425 | 0.7297 | 0.3480 |
| TV2 | 0.2105 | 0.5166 | 0.6425 | 0.7297 | 0.3480 |
| TV2 − TV1 (pp) | +0.00 | +0.00 | +0.00 | +0.00 | +0.00 |
| TV1 − paper (pp) | -0.24 | +0.18 | +0.28 | -0.06 | -0.16 |
| TV2 − paper (pp) | -0.24 | +0.18 | +0.28 | -0.06 | -0.16 |

**K1-POI**

| | Acc@1 | Acc@5 | Acc@10 | Acc@20 | MRR |
|---|---|---|---|---|---|
| Paper | 0.2289 | 0.5247 | 0.6415 | 0.7288 | 0.3626 |
| TV1 | 0.2286 | 0.5255 | 0.6417 | 0.7282 | 0.3618 |
| TV2 | 0.2286 | 0.5255 | 0.6417 | 0.7282 | 0.3618 |
| TV2 − TV1 (pp) | +0.00 | +0.00 | +0.00 | +0.00 | +0.00 |
| TV1 − paper (pp) | -0.03 | +0.08 | +0.02 | -0.06 | -0.08 |
| TV2 − paper (pp) | -0.03 | +0.08 | +0.02 | -0.06 | -0.08 |

### TKY

**K1-POI w/o Reranker**

| | Acc@1 | Acc@5 | Acc@10 | Acc@20 | MRR |
|---|---|---|---|---|---|
| Paper | 0.2393 | 0.5010 | 0.6044 | 0.6842 | 0.3586 |
| TV1 | 0.2396 | 0.5017 | 0.6051 | 0.6848 | 0.3593 |
| TV2 | 0.2396 | 0.5017 | 0.6051 | 0.6848 | 0.3593 |
| TV2 − TV1 (pp) | +0.00 | +0.00 | +0.00 | +0.00 | +0.00 |
| TV1 − paper (pp) | +0.03 | +0.07 | +0.07 | +0.06 | +0.07 |
| TV2 − paper (pp) | +0.03 | +0.07 | +0.07 | +0.06 | +0.07 |

**K1-POI**

| | Acc@1 | Acc@5 | Acc@10 | Acc@20 | MRR |
|---|---|---|---|---|---|
| Paper | 0.2496 | 0.5121 | 0.6100 | 0.6872 | 0.3682 |
| TV1 | 0.2508 | 0.5127 | 0.6106 | 0.6875 | 0.3694 |
| TV2 | 0.2508 | 0.5127 | 0.6106 | 0.6875 | 0.3694 |
| TV2 − TV1 (pp) | +0.00 | +0.00 | +0.00 | +0.00 | +0.00 |
| TV1 − paper (pp) | +0.12 | +0.06 | +0.06 | +0.03 | +0.12 |
| TV2 − paper (pp) | +0.12 | +0.06 | +0.06 | +0.03 | +0.12 |

## 3. Mức tăng nhờ reranker (w/ trừ w/o, pp)

| Dataset | Acc@1 (paper) | Acc@1 (TV1 = TV2) | MRR (paper) | MRR (TV1 = TV2) |
|---|---|---|---|---|
| CA | +2.00 | +1.69 | +1.60 | +1.36 |
| NYC | +1.60 | +1.81 | +1.30 | +1.38 |
| TKY | +1.03 | +1.12 | +0.96 | +1.01 |

Ở K lớn, reranker gần như không đổi và trên NYC còn giảm nhẹ: Acc@10 −0.08 pp, Acc@20 −0.15 pp (cả TV1 và TV2).

## 4. Kiểm tra mức chạy (`tv1_vs_tv2_run_checks.csv`)

| Dataset | Ô lịch sử khác nhau | Dòng log khác nhau* | Epoch tốt nhất TV1 / TV2 | Cấu hình reranker giống | Thời gian TV1 → TV2 (giây) | GPU TV1 → TV2 |
|---|---|---|---|---|---|---|
| CA | 0 / 900 | 0 / 257 | 91 / 91 | có | 5103 → 5202 (+1.9%) | cuda:0 → cuda:1 |
| NYC | 0 / 900 | 0 / 262 | 65 / 65 | có | 2329 → 2322 (-0.3%) | cuda:0 → cuda:1 |
| TKY | 0 / 900 | 0 / 274 | 99 / 99 | có | 7669 → 7860 (+2.5%) | cuda:0 → cuda:0 |

\* So sánh sau khi bỏ qua ba thứ vốn khác nhau giữa hai phiên: tên thiết bị (cuda:N), thời gian `elapsed` và đường dẫn checkpoint. Thời gian của TV2 lấy từ `run_status_seed42.json` (làm tròn 0.1 phút ≈ 6 giây), nên chỉ mang tính tham khảo. Số ô lịch sử so sánh = 100 epoch × 9 cột. Hai lần chạy của TV2 chạy song song trên 2 GPU, còn TV1 chạy tuần tự từng dataset trên một GPU (theo mốc thời gian của các file kết quả).

## 5. Lưu ý khi đọc

- Dòng `Final test (best epoch …)` trong `training.log` **không phải** số ở bảng Summary (ví dụ NYC Acc@1 0.2163 so với 0.2105 và 0.2286). Theo tiêu đề biểu đồ validation của TV1 (“fixed-prior reranker”), log huấn luyện đánh giá với reranker có trọng số cố định mặc định, chứ không phải cấu hình đã search. Số dùng để báo cáo là bảng Summary trong `report.md`.
- Mọi số đều từ **một seed (42)**. Độ lệch so với paper (tối đa 0.69 pp) chưa thể tách thành nhiễu seed hay khác biệt thật nếu chưa chạy thêm seed.
