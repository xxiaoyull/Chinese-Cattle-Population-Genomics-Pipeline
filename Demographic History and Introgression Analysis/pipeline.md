# Demographic History and Introgression Analysis
Reconstructed demographic history and investigated admixture patterns using fastsimcoal2, D statistics and f3 statistics.
## statistics
```
#!/bin/bash
qp3Pop -p f3stats.par > f3stats.result
qpDstat -p Dstats.par > Dstats_result

```
## fastsimcoal2
```
easySFS.py -i 50.polarized.vcf.recode.vcf -p pops_file.txt --preview -a

sfsput=fastsimcoal2
input=03.fastsimcoal
for i in {51..100}
do

mkdir $i
cp $input/2PopExpInst20Mb.est $input/$i/$i.est
cp $input/2PopExpInst20Mb.tpl $input/$i/$i.tpl
cp $sfsput/final_filtered_variants_jointMAFpop1_0.obs $input/$i/${i}_jointMAFpop1_0.obs
cp $sfsput/final_filtered_variants_jointMAFpop2_0.obs $input/$i/${i}_jointMAFpop2_0.obs
cp $sfsput/final_filtered_variants_jointMAFpop2_1.obs $input/$i/${i}_jointMAFpop2_1.obs
cp $sfsput/final_filtered_variants_jointMAFpop3_0.obs $input/$i/${i}_jointMAFpop3_0.obs
cp $sfsput/final_filtered_variants_jointMAFpop3_1.obs $input/$i/${i}_jointMAFpop3_1.obs
cp $sfsput/final_filtered_variants_jointMAFpop3_2.obs $input/$i/${i}_jointMAFpop3_2.obs
cp $sfsput/final_filtered_variants_jointMAFpop4_0.obs $input/$i/${i}_jointMAFpop4_0.obs
cp $sfsput/final_filtered_variants_jointMAFpop4_1.obs $input/$i/${i}_jointMAFpop4_1.obs
cp $sfsput/final_filtered_variants_jointMAFpop4_2.obs $input/$i/${i}_jointMAFpop4_2.obs
cp $sfsput/final_filtered_variants_jointMAFpop4_3.obs $input/$i/${i}_jointMAFpop4_3.obs

export DIR=$input/$i
cd $DIR
mkdir log
jsub -J ${i}.fast -n 10 -e log/${i}.e -o log/${i}.o bash fsc26.sh ${i}
cd ..
done
```


# Admixture Proportion and Timing Estimation
Estimated admixture proportions and timing using fastGLOBETROTTER and MALDER based on phased haplotypes.
```
#!/bin/bash
fastsimcoal2 -t my_parameter_file.par -n 100000 -m -e
malder -p ${i}.alder.par > ${i}.alder.result
```
