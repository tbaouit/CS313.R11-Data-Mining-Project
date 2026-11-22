# Team handoff: TV1 + TV2 (K1-POI, seed 42)

Gói này gộp kết quả tái lập của hai thành viên theo **cùng một cấu trúc**, tách thành hai phần để so sánh với nhau và với paper.

```
team_handoff_TV1_TV2/
├── TV1/        kết quả của TV1, giữ nguyên bản gốc (reports/team_handoff_20261119)
├── TV2/        kết quả của TV2, cùng cấu trúc với TV1
│   ├── experiment_setup.csv, data_verification.json, dataset_statistics.csv
│   ├── ablation_reranker.csv, baseline_comparison.csv
│   └── evidence/{CA,NYC,TKY}/  report.md, final_metrics.json, run_config.json, status.json,
│                              data_manifest.json, training_history.csv, figures/, logs/training.log
└── comparison/ so sánh TV1 ↔ TV2 ↔ paper
    ├── tv1_vs_tv2_summary.md         đọc file này trước
    ├── tv1_vs_tv2_vs_paper.csv       30 dòng: TV1, TV2, paper và các độ chênh (pp)
    ├── tv1_vs_tv2_run_checks.csv     kiểm tra mức chạy: lịch sử, log, epoch tốt nhất, cấu hình, thời gian
    ├── baseline_comparison_all.csv   bảng baseline của paper + TV1 + TV2 (cột `member`)
    └── figures/                      tv1_tv2_paper_{CA,NYC,TKY}, delta_vs_paper (png và pdf)
```

## Nguồn gốc các file của TV2

| File | Cách tạo |
|---|---|
| `evidence/*/report.md` | bản sao nguyên văn báo cáo `*_seed42_mine_*.md` do script của repo ghi (TV1 cũng làm như vậy) |
| `evidence/*/logs/training.log` | bản sao nguyên văn log huấn luyện |
| `evidence/*/training_history.csv`, `final_metrics.json` | trích từ log và báo cáo trên, cùng schema với TV1 |
| `evidence/*/figures/` | vẽ lại bằng script khác theo cùng kiểu với TV1 (bốn hình: loss, val Acc@1, val MRR, so sánh với paper), nên chi tiết nhỏ có thể khác |
| `evidence/*/run_config.json` | dựng từ dòng `Wrapper invocation` trong báo cáo và từ `run_status_seed42.json` |
| `evidence/*/status.json`, `experiment_setup.csv` | `elapsed_seconds` = số phút trong `run_status_seed42.json` × 60 (độ chính xác ≈ 6 giây) |
| `ablation_reranker.csv`, `baseline_comparison.csv` | cùng schema với TV1; các dòng của paper giữ nguyên, dòng đo được thay bằng số của TV2 |
| `dataset_statistics.csv` | **sao chép từ TV1, không tính lại.** Vì file dữ liệu đã xử lý có cùng sha256 nên thống kê giống hệt (cột `provenance` ghi rõ) |
| `data_verification.json` | sha256 lấy từ output `sha256sum` trong notebook của TV2. Có thêm hai khóa: `matches_tv1` và `matches_review_regeneration` (chạy lại `data_process.py` trên `raw.tar.gz` ở một môi trường khác cho cùng hash) |

## Khác biệt nhỏ so với TV1

- `data_verification.json`: TV1 có khóa `matches_kaggle` và `source_archive`; TV2 dùng `matches_tv1`, `matches_review_regeneration` và `source` vì hash của TV2 vốn đã lấy từ Kaggle.
- `run_config.json`: `command` của TV2 chỉ gồm các tham số script (báo cáo không ghi đường dẫn Python và cờ `-X utf8 -u`). Commit của repo nhóm tại thời điểm chạy không được ghi lại; `upstream_commit` là commit code gốc mà repo nhóm import.
- Checkpoint (`.ckpt`) **không** nằm trong gói này (TV1 cũng không có). Checkpoint của TV2 nằm trong file zip kết quả gốc.

## Kết quả ngắn gọn

Xem `comparison/tv1_vs_tv2_summary.md`. Tóm tắt: 30/30 metric test của TV1 và TV2 giống nhau đến 4 chữ số thập phân, và cách paper tối đa 0.69 pp (trung bình 0.16 pp). Vì cả hai dùng seed 42 nên kết quả xác nhận khả năng tái lập chứ chưa đo được độ dao động giữa các seed.
