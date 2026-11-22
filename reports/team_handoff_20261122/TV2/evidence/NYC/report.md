# NYC_seed42_mine

- Code snapshot root: `.tmp/st_prior_reranker_hparam_search_snapshot_20261122_051715`
- Wrapper invocation: `exp_scripts/run_st_prior_reranker_hparam_search_parallel_trials.py --exp_id NYC_seed42_mine --data_path_list data/processed/NYC_excluding_cold.pkl --epochs 100 --window_size_list 1 --devices 1 --batch_size 1024 --eval_batch_size 512 --lr 0.0003 --weight_decay 5e-06 --dtype fp32 --seed 42 --search_trials 20000 --search_eval_samples 20000 --search_top_m 400 --st_prior_num_parallel_trials 2`
- Training logs dir: `.tmp/logs_st_prior_hparam_search_train_20261122_051715`
- Checkpoints dir: `exp_scripts/results/checkpoints`
- Search device: `cuda:1`

## Summary

### NYC, k=1

|  | Acc@1 | Acc@5 | Acc@10 | Acc@20 | MRR |
| --- | --- | --- | --- | --- | --- |
| w/o reranker | 0.2105 | 0.5166 | 0.6425 | 0.7297 | 0.3480 |
| w/ reranker | 0.2286 | 0.5255 | 0.6417 | 0.7282 | 0.3618 |

## Results

### processed_NYC_excluding_cold k=1

- status: ok
- data_path: `data/processed/NYC_excluding_cold.pkl`
- checkpoint_path: `exp_scripts/results/checkpoints/st_prior_backbone_processed_NYC_excluding_cold_k1_20261122_051715.ckpt`
- train_device: cuda:1 returncode=0 log=.tmp/logs_st_prior_hparam_search_train_20261122_051715/processed_NYC_excluding_cold_k1.log
- score_terms: cl_sim, dist, time, user
- tau_p75_km: 5.37  (tau_km used: 10.73)
- best_cfg: lambda_time=0.9670 lambda_user=0.0644 lambda_dist=0.6361 lambda_cl_sim=0.9707 sigma_min_km=0.50 tau_km=10.73
- search: trials=20000 stage1_eval_samples=9458 val_size=9458
- stage1_parallel_trials: 2
- val(base): Acc@1=0.2295 Acc@5=0.5319 Acc@10=0.6506 Acc@20=0.7360 MRR=0.3648
- val(rerank best): Acc@1=0.2435 Acc@5=0.5429 Acc@10=0.6590 Acc@20=0.7406 MRR=0.3767
- test(base): Acc@1=0.2105 Acc@5=0.5166 Acc@10=0.6425 Acc@20=0.7297 MRR=0.3480
- test(rerank final once): Acc@1=0.2286 Acc@5=0.5255 Acc@10=0.6417 Acc@20=0.7282 MRR=0.3618
- test(rerank score w/o base): Acc@1=0.0558 Acc@5=0.2033 Acc@10=0.3080 Acc@20=0.4367 MRR=0.1376

