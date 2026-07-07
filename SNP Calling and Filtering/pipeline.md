# SNP Calling and Filtering
Performed read quality control, variant calling, phasing, imputation, and functional annotation to generate a high-quality genome-wide variant dataset from fastq files for downstream analysis.
## Using filtered files like chr1.clean.SNP.vcf.gz to impute, the script like this
```
for i in {1..29}
do
	echo $i
	echo "#!/bin/bash" > $i.imput.sh
	echo "export beagle=beagle.27Jan18.7e1.jar" >> $i.imput.sh
	echo "export Finalsnp=/input path/" >> $i.imput.sh
	echo "java -Xmx100g -Xss128m -jar \$beagle chrom=$i gtgl=\$Finalsnp/$i.clean.SNP.vcf.gz out=chr$i.imp gprobs=true niterations=10 nthreads=48" >> $i.imput.sh
	echo "java -Xmx100g -Xss128m -jar \$beagle gt=chr${i}.imp.vcf.gz out=chr${i}.imp.phase gprobs=true niterations=10 nthreads=48 " >> $i.imput.sh
done 
```
## Annotation
```
for i in {1..29}
do
java -Xmx64g -jar \
snpEff ARS-UCD1.2 \
${i}.snp.vcf.gz > ${i}.snp.eff \
-csvStats ${i}.snp.eff.csv -stats ${1}.snp.eff.html
done
```
