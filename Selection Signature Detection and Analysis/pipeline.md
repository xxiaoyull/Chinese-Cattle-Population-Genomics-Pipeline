# Selection Signature Detection and Analysis
Identified genomic regions under selection using iHS, FST, XP-EHH, θπ ratio, and local ancestry inference (LOTER)

##  analysis
```
selscan --ihs --vcf pop.1.VCF.polarized.vcf.gz –map 1.map --cutoff 0.01 --out pop.chr --threads 20 norm --ihs --files HBZ.chr.ihs.out --bp-win --winsize 50000

vcftools --gzvcf all.SNP.vcf.gz --keep target.list --window-pi 50000 --window-pi-step 20000 --maf 0.05 --max-missing 0.90 –out target.pi

norm --xpehh --files indicine_taurine.chr.xpehh.xpehh.out --bp-win --winsize 50000


loter_cli -r ref1.npy ref2.npy -a target.npy -f npy -o ./output.npy -n 20 -v

vcftools --gzvcf all.SNP.vcf.gz --weir-fst-pop target.list --weir-fst-pop ref.list --fst-window-size 50000 --fst-window-step 20000 --out Fst-win --max-missing 0.9 --maf 0.05
```


