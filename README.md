# Crabs_160823
#steps everytime
```
module load eDNA  
export PATH="/nesi/nobackup/uoo03904/bin/reference_database_creator:$PATH"
```
1) Download fasta files
```
crabs db_download --source mitofish --output mitofish.fasta --keep_original yes

crabs db_download --source ncbi --database nucleotide --query '12S[All Fields] AND txid7898[Organism:exp] AND mitochondrion[filter]' --output 12S_NCBI_fish.fasta --keep_original yes --email ryan.r.easton@gmail.com --batchsize 5000

crabs db_download --source embl --database 'VRT*' --output embl_vrt.fasta --keep_original yes

crabs db_download --source bold --database 'Actinopterygii|Petromyzontiformes' --output bold_fish_lamprey.fasta --keep_original yes
```
2) Download taxonomy
```
crabs db_download --source taxonomy #use gunzip to unzip file if not automatically unzipped
```
3) Merge
```
crabs db_merge --output merged_total.fasta --uniq no --input mitofish.fasta 12S_NCBI_fish.fasta bold_fish_lamprey.fasta embl_vrt.fasta
```
4) Insilico_pcr
```
crabs insilico_pcr --input merged_total.fasta --output pcr_12s_fish.fasta --fwd GTCGGTAAAACTCGTGCCAGC --rev CATAGTGGGGTATCTAATCCCAGTTTG --error 4.5
```
5)
