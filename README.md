# pred_codes

#### to run boltLMM
  
```
./bolt --bed ukbb_reference.bed --bim ukbb_reference.bim --fam ukbb_reference.fam --phenoFile=HDL_cholesterol_ukbb_british_250k.phen_bolt --phenoCol=HDL --LDscoresFile=/data/alh-admmdm/softwares/BOLT-LMM_v2.4/tables/LDSCORE.1000G_EUR.tab.gz --modelSnps=british_50k_ld.prune.in --lmm --numThreads=6 --statsFile=Bolt_HDL_sumstat_250k --predBetasFile=Bolt_HDL_250k
```
