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
code here
```
