# Crabs_160823
#steps everytime
```
module purge
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
5) Pga
```
crabs pga --input merged_total.fasta --database pcr_12s_fish.fasta --output pga_12s_fish.fasta --fwd GTCGGTAAAACTCGTGCCAGC --rev CATAGTGGGGTATCTAATCCCAGTTTG --speed medium --percid 0.90 --coverage 0.90 --filter_method relaxed # dropped percid and coverage to 0.90 instead of 0.95 because we were losing important species
```
6) Assign taxa
```
crabs assign_tax --input pga_12s_fish.fasta --output pga_12s_fish.tsv --acc2tax nucl_gb.accession2taxid --taxid nodes.dmp --name names.dmp --missing missing_pga_12s_fish.tsv
```
7) Dereplicate
```
crabs dereplicate --input pga_12s_fish.tsv --output pga_12s_fish_derep.tsv --method uniq_species
```
8) Seq cleanup
```
crabs seq_cleanup --input pga_12s_fish_derep.tsv --output pga_12s_fish_derep_clean.tsv --minlen 100 --maxlen 500 --maxns 0 --enviro yes --species yes --nans 0
```
9) Tax format export
```
crabs tax_format --input pga_12s_fish_derep_clean.tsv --output pga_12s_fish_derep_clean.fasta --format sintax
```
10)
