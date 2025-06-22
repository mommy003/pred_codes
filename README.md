# pred_codes

#### Example codes to run boltLMM
  
```
./bolt --bed ukbb_reference.bed --bim ukbb_reference.bim --fam ukbb_reference.fam --phenoFile=HDL_cholesterol_ukbb_british_250k.phen_bolt --phenoCol=HDL --LDscoresFile=/data/alh-admmdm/softwares/BOLT-LMM_v2.4/tables/LDSCORE.1000G_EUR.tab.gz --modelSnps=british_50k_ld.prune.in --lmm --numThreads=6 --statsFile=Bolt_HDL_sumstat_250k --predBetasFile=Bolt_HDL_250k
```

#### Example codes to run polypred
  
```
./bolt --bed ukbb_reference.bed --bim ukbb_reference.bim --fam ukbb_reference.fam --phenoFile=HDL_cholesterol_ukbb_british_250k.phen_bolt --phenoCol=HDL --LDscoresFile=/data/alh-admmdm/softwares/BOLT-LMM_v2.4/tables/LDSCORE.1000G_EUR.tab.gz --modelSnps=british_50k_ld.prune.in --lmm --numThreads=6 --statsFile=Bolt_HDL_sumstat_250k --predBetasFile=Bolt_HDL_250k
python munge_polyfun_sumstats.py --sumstats Bolt_HDL_sumstat_250k --out output2/Bolt_HDL_sumstat_250k.munged.parquet --n 258000
python create_finemapper_jobs.py --sumstats output2/Bolt_HDL_sumstat_250k.munged.parquet --n 258000 --method susie --non-funct --max-num-causal 2 --out-prefix output2/Bolt_HDL_sumstat_250k_output --jobs-file output2/jobs_HDL.txt
bash output2/jobs_HDL.txt 
python aggregate_finemapper_results.py --out-prefix output2/Bolt_HDL_sumstat_250k_output --sumstats output2/Bolt_HDL_sumstat_250k.munged.parquet --allow-missing-jobs --out output2/polyfun_HDL_output.agg.txt.gz --adjust-beta-freq
python polypred.py --combine-betas --betas Bolt_HDL_sumstat_250k,polyfun_HDL_250_output.agg.txt.gz --pheno HDL_choles_adj_ethnicity3.bolt --output-prefix output2/polypred_asian_HDL --plink-exe /data/alh-admmdm/polyfun-master/plink1.9 ethnicity3.bed
```
