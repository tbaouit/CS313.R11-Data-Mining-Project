# TKY_seed42_mine

- Code snapshot root: `.tmp/st_prior_reranker_hparam_search_snapshot_20261122_051655`
- Wrapper invocation: `exp_scripts/run_st_prior_reranker_hparam_search_parallel_trials.py --exp_id TKY_seed42_mine --data_path_list data/processed/TKY_excluding_cold.pkl --epochs 100 --window_size_list 1 --devices 0 --batch_size 1024 --eval_batch_size 512 --lr 0.0003 --weight_decay 5e-06 --dtype fp32 --seed 42 --search_trials 20000 --search_eval_samples 20000 --search_top_m 400 --st_prior_num_parallel_trials 2`
- Training logs dir: `.tmp/logs_st_prior_hparam_search_train_20261122_051655`
- Checkpoints dir: `exp_scripts/results/checkpoints`
- Search device: `cuda:0`

## Summary

### TKY, k=1

|  | Acc@1 | Acc@5 | Acc@10 | Acc@20 | MRR |
| --- | --- | --- | --- | --- | --- |
| w/o reranker | 0.2396 | 0.5017 | 0.6051 | 0.6848 | 0.3593 |
| w/ reranker | 0.2508 | 0.5127 | 0.6106 | 0.6875 | 0.3694 |

## Results

### processed_TKY_excluding_cold k=1

- status: ok
- data_path: `data/processed/TKY_excluding_cold.pkl`
- checkpoint_path: `exp_scripts/results/checkpoints/st_prior_backbone_processed_TKY_excluding_cold_k1_20261122_051655.ckpt`
- train_device: cuda:0 returncode=0 log=.tmp/logs_st_prior_hparam_search_train_20261122_051655/processed_TKY_excluding_cold_k1.log
- score_terms: cl_sim, dist, time, user
- tau_p75_km: 6.04  (tau_km used: 12.08)
- best_cfg: lambda_time=0.9248 lambda_user=0.1652 lambda_dist=0.0409 lambda_cl_sim=0.5110 sigma_min_km=1.00 tau_km=12.08
- search: trials=20000 stage1_eval_samples=20000 val_size=35232
- stage1_parallel_trials: 2
- val(base): Acc@1=0.2142 Acc@5=0.4741 Acc@10=0.5804 Acc@20=0.6656 MRR=0.3337
- val(rerank best): Acc@1=0.2266 Acc@5=0.4820 Acc@10=0.5840 Acc@20=0.6652 MRR=0.3442
- test(base): Acc@1=0.2396 Acc@5=0.5017 Acc@10=0.6051 Acc@20=0.6848 MRR=0.3593
- test(rerank final once): Acc@1=0.2508 Acc@5=0.5127 Acc@10=0.6106 Acc@20=0.6875 MRR=0.3694
- test(rerank score w/o base): Acc@1=0.0464 Acc@5=0.1365 Acc@10=0.2037 Acc@20=0.3039 MRR=0.1035

