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

#### Example codes to run PRSice
  
```
./PRSice_linux --base cholesterol_ukbb_reference.assoc.linear --target ethnicity4p --pheno cholesterol_adj_ethnicity4_6sd --stat BETA --bar-levels 1e-8,1e-7,1e-6,1e-5,3e-5,1e-4,3e-4,0.001,0.003,0.01,0.03,0.1,0.3,1 --fastscore --out /data/alh-admmdm/prediction/african/choles_compari/prs_choles_ref_wb_target_afr_prsice 
```

#### Example codes to run PRScsx
  
```
python PRScsx.py --ref_dir=/data/alh-admmdm/softwares/PRScsx/reference_prscsx --bim_prefix=ethnicity4p --sst_file=cholesterol_ukbb_reference.assoc.Prscsx.txt --n_gwas=200000 --pop=EUR --phi=1e-2 --out_dir=PRScsx_test --out_name=choles_afr
```
