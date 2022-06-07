2. GENE PREDICTION PROTOCOL

The goal was to successfully predict genes using Braker using the RNAseq data and S. purpuratus protein files

2.1 First build a database for RepeatModeler in order to identify genomic repetitive elements

```
BuildDatabase -name spez_repeat_db spez.final.sqsort.rename.fasta
RepeatModeler -database spez_repeat_db -engine ncbi -pa 23 &>repeatmodel.out
RepeatMasker -engine ncbi -pa 23 -s -lib spez_repeat_db-families.fa  -gff -dir spez_repeat_db -xsmall spez.final.sqsort.rename.fasta
```

2.2 Prep the RNAseq data - clean and trim

java -jar /apps/pkg/trimmomatic/0.38/trimmomatic-0.38.jar PE -threads 10 -phred33 ./2018JAN12HiSeq_Run_Sample_Ecm_UNCC_Reitzel_GAGTGG_L002_R1_001.fastq.gz ./2018JAN12HiSeq_Run_Sample_Ecm_UNCC_Reitzel_GAGTGG_L002_R2_001.fastq.gz spez.trim.r1.fastq spez.trim.unpr.r1.fastq spez.trim.r2.fastq spez.trim.unpr.r2.fastq ILLUMINACLIP:/apps/pkg/trimmomatic/0.38/adapters/TruSeq3-PE.fa:2:30:10 LEADING:3 TRAILING:3 SLIDINGWINDOW:4:15 MINLEN:36

2.3 Align RNA reads to genome 

```
bwa index /scratch/rketchu1/Dovetail_Genome_EM/ANNOTATION/spez.final.sqsort.rename.fasta
bwa mem -t 23 /scratch/rketchu1/Dovetail_Genome_EM/ANNOTATION/spez.final.sqsort.rename.fasta spez.trim.r1.fastq spez.trim.r2.fastq > spez.final.sqsort.rename.rnaalign.sam
cat spez.final.sqsort.rename.rnaalign.sam | samtools view -S -bh - > spez.final.sqsort.rename.rnaalign.bam
samtools sort spez.final.sqsort.rename.rnaalign.bam -o spez.final.sqsort.rename.rnaalign.bam
```

2.4 Run Braker

```
braker.pl --cores=36 --genome=/scratch/rketchu1/Dovetail_Genome_EM/ANNOTATION/BRAKER/spez.final.sqsort.rename.fasta.masked --workingdir=/scratch/rketchu1/Dovetail_Genome_EM/ANNOTATION/BRAKER --prot_seq=/scratch/rketchu1/Dovetail_Genome_EM/ANNOTATION/BRAKER/spurp-v5.faa --bam=/scratch/rketchu1/Dovetail_Genome_EM/ANNOTATION/spez.final.sqsort.rename.rnaalign.bam --etpmode --softmasking --BAMTOOLS_PATH=${BAMTOOLS}/bin --AUGUSTUS_CONFIG_PATH=${HOME}/augustus_config --ALIGNMENT_TOOL_PATH=${PROTHINT}/bin 
```
