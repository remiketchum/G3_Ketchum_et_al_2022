3. PFAM ANALYSIS

The goal was to generate PFAM profiles to compare gene family representation across five different species of sea urchins. 
Downloaded: https://data.broadinstitute.org/Trinity/Trinotate_v3_RESOURCES/Trinotate_v3_RESOURCES/Pfam-A.hmm.gz

3.1 Prepare an HMM database to run hmmscan

```
hmmpress Pfam-A.hmm
```

3.2 Hmmscan searches a protein sequence against a protein profile hmm database (generated above)

```
hmmscan --cpu 23 --domtblout TrinotatePFAM.out Pfam-A.hmm spez.final.protein.fa
hmmscan --cpu 23 --domtblout TrinotatePFAM.Htub.out Pfam-A.hmm Htub.braker.pasa.transcripts_no_utr.protein.fa 
hmmscan --cpu 23 --domtblout TrinotatePFAM.Lvar.out Pfam-A.hmm Lvar.braker.pasa.transcripts_no_utr.protein.fa
hmmscan --cpu 23 --domtblout TrinotatePFAM.Hery.out Pfam-A.hmm Hery.braker.pasa.transcripts_no_utr.protein.fa 
hmmscan --cpu 23 --domtblout TrinotatePFAM.Spurp.out Pfam-A.hmm SPU_peptide.fasta
```


Please see Joseph Ryan's git https://github.com/josephryan/SpezHox for code pertaining to the E. sp. EZ's hox and parahox analyses
