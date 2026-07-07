# Population Structure and Genetic Diversity
Characterized population structure and genetic diversity using PCA, ADMIXTURE, ROH, IBD, analysis.
## PCA analysis
```
smartpca -p bos_eigensoft_smartpca.par
```
## ROH analysis
We applied PLINK to detect ROH segments and Mclust.R to identify the different threshold value, like this.
```
#!/bin/bash
vcftools --gzvcf ./merge.vcf.gz --plink --chrom-map chrID --out merge
plink --file merge --make-bed --chr-set 29 --out merge
plink --bfile ./merge \
	--chr-set 29 \
	--homozyg-gap 1000 \
	--homozyg-kb 100 \
	--homozyg-snp 200 \
	--homozyg-window-het 1 \
	--homozyg-window-snp 100 \
	--homozyg-window-threshold 0.05 \
	--out all_ROH

```
```
Rscript Mclust.R ${POP}
```
