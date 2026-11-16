# NYC pipeline check

## Provenance

- Upstream: https://github.com/XZJIsme/k1-poi
- Source commit: `234bf2cef65d06746e0ec324a788ef770eb2fd58`
- Run date: 2026-11-16.
- Platform: Windows, Python 3.13.3, PyTorch 2.14.0+cu126.
- GPU: NVIDIA GeForce RTX 3050 Laptop GPU, 4 GB VRAM.
- Raw datasets: the upstream `data/raw/raw.tar.gz` archive.
- Preprocessing completed for NYC, TKY, and CA. Only NYC was trained in this check.
- Training and the search wrapper completed with exit code 0; a checkpoint and report were generated locally.

## Reproduce the check

Run from the repository root. Preprocessing commands:

```text
tar -xzf data/raw/raw.tar.gz -C data/raw
python data/data_process.py
```

The run used the environment variables `PYTHONUTF8=1`, `OMP_NUM_THREADS=4`, and `MKL_NUM_THREADS=4`. Training/search invocation (one line, compatible with PowerShell):

```text
python -X utf8 -u exp_scripts/run_st_prior_reranker_hparam_search_parallel_trials.py --exp_id nyc_pipeline_check_2epochs --data_path_list data/processed/NYC_excluding_cold.pkl --epochs 2 --window_size_list 1 --devices 0 --eval_batch_size 512 --self_attn_d_model 128 --self_attn_num_layers 2 --self_attn_num_heads 4 --poi_ecl_negative_source topk --st_prior_candidate_k 200 --search_trials 40 --search_eval_samples 2000 --search_top_m 5 --st_prior_num_parallel_trials 2
```

## Measured results

NYC test metrics from the final wrapper report:

- Without reranker: Acc@1=0.0531, Acc@5=0.1505, Acc@10=0.2056, Acc@20=0.2691, MRR=0.1015.
- With validation-selected reranker: Acc@1=0.0950, Acc@5=0.2290, Acc@10=0.2914, Acc@20=0.3503, MRR=0.1570.
- Validation set size: 9,458; stage-1 search used 2,000 instances and 40 trials; the best 5 were evaluated on full validation.
- Selected weights: time=0.5569, user=0.6846, distance=0.8429, contrastive similarity=0.7760; minimum radius=0.30 km; distance scale approximately 2.68 km.

Local evidence paths:

- Report: `exp_scripts/results/nyc_pipeline_check_2epochs_20261116_233007.md`.
- Training log: `.tmp/logs_st_prior_hparam_search_train_20261116_232331/processed_NYC_excluding_cold_k1.log`.
- Checkpoint: `exp_scripts/results/checkpoints/st_prior_backbone_processed_NYC_excluding_cold_k1_20261116_232331.ckpt`.

These generated artifacts remain local under the upstream ignore rules; the measured results are recorded here for traceability.

## Scope

This check confirms that the provided preprocessing, training, validation search, checkpoint loading, and test evaluation pipeline executes on this machine. It does not reproduce the full paper protocol: this run used 2 rather than 100 epochs, 40 rather than the README's 20,000 search trials, and evaluation batch size 512. The paper reports NYC Acc@1=0.2289 and MRR=0.3626 for its full default model. No full-budget run or TKY/CA training has been completed locally.
