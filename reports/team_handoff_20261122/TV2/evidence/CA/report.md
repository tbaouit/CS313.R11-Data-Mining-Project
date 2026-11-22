# CA_seed42_mine

- Code snapshot root: `.tmp/st_prior_reranker_hparam_search_snapshot_20261122_055606`
- Wrapper invocation: `exp_scripts/run_st_prior_reranker_hparam_search_parallel_trials.py --exp_id CA_seed42_mine --data_path_list data/processed/CA_excluding_cold.pkl --epochs 100 --window_size_list 1 --devices 1 --batch_size 1024 --eval_batch_size 512 --lr 0.0003 --weight_decay 5e-06 --dtype fp32 --seed 42 --search_trials 20000 --search_eval_samples 20000 --search_top_m 400 --st_prior_num_parallel_trials 2`
- Training logs dir: `.tmp/logs_st_prior_hparam_search_train_20261122_055607`
- Checkpoints dir: `exp_scripts/results/checkpoints`
- Search device: `cuda:1`

## Summary

### CA, k=1

|  | Acc@1 | Acc@5 | Acc@10 | Acc@20 | MRR |
| --- | --- | --- | --- | --- | --- |
| w/o reranker | 0.1608 | 0.3474 | 0.4351 | 0.5200 | 0.2527 |
| w/ reranker | 0.1777 | 0.3602 | 0.4438 | 0.5280 | 0.2663 |

## Results

### processed_CA_excluding_cold k=1

- status: ok
- data_path: `data/processed/CA_excluding_cold.pkl`
- checkpoint_path: `exp_scripts/results/checkpoints/st_prior_backbone_processed_CA_excluding_cold_k1_20261122_055607.ckpt`
- train_device: cuda:1 returncode=0 log=.tmp/logs_st_prior_hparam_search_train_20261122_055607/processed_CA_excluding_cold_k1.log
- score_terms: cl_sim, dist, time, user
- tau_p75_km: 6.32  (tau_km used: 12.65)
- best_cfg: lambda_time=0.9945 lambda_user=0.0036 lambda_dist=0.0173 lambda_cl_sim=0.9569 sigma_min_km=0.50 tau_km=12.65
- search: trials=20000 stage1_eval_samples=16091 val_size=16091
- stage1_parallel_trials: 2
- val(base): Acc@1=0.1654 Acc@5=0.3723 Acc@10=0.4596 Acc@20=0.5430 MRR=0.2635
- val(rerank best): Acc@1=0.1872 Acc@5=0.3844 Acc@10=0.4675 Acc@20=0.5461 MRR=0.2808
- test(base): Acc@1=0.1608 Acc@5=0.3474 Acc@10=0.4351 Acc@20=0.5200 MRR=0.2527
- test(rerank final once): Acc@1=0.1777 Acc@5=0.3602 Acc@10=0.4438 Acc@20=0.5280 MRR=0.2663
- test(rerank score w/o base): Acc@1=0.0677 Acc@5=0.1545 Acc@10=0.2085 Acc@20=0.2843 MRR=0.1189

