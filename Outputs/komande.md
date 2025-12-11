# komande.md

*Ve�ba 6*

## >>> README.md

### 1.5 - 1.9 - uneti komande

```bash
conda activate kleborate
gunzip za_vezbe_Klebsiella_sekvence.tar.gz
tar -xzf za_vezbe_Klebsiella_sekvence.tar.gz 
cd za_vezbe_Klebsiella_sekvence.tar.gz
mkdir -p ../data/{genomes,annotations}
mv *.fna ../data/genomes ; mv *.gff ../data/annotations
cd ..
mkdir results
```

---

## >>> klebsiella_demonstracija_prosirena.md

### 4.1 - uneti *output* komandi, a ne komande

```bash
# Upi�ite brojeve kolona koje izdvajate:
1,52-55,71,67-69,60-63,73
# Prika�ite izdvojene kolone za Strain, Virulence score, iucA, iroB, rmpA i rmpA2:
strain         iucA  iucB  iucC  iucD  iroB  iroC   iroD  iroN   rmpA     rmpD    rmpC    virulence_score  rmpA2
GCF_017743115  1     1     1     1     1     13     1     1      2        15-0%   2       4                rmpA2_5-54%
GCF_017743135  9     7     12    8*    6     19-4%  11    5      11       14      8       4                -
GCF_017815715  1     1     1*    1     1     1      1     1      2        27*     2       3                rmpA2_5-54%
GCF_021057265  1     15    1     1     -     -      -     -      27       2       2       4                rmpA2_6*-47%
GCF_021442005  1     1     1     1     -     -      -     1*-0%  40*-47%  -       -       4                rmpA2_3-47%
GCF_902723695  1     1     1     1     1     1      1     1      2        2       2       4                rmpA2_2*-54%
GCF_902723705  1     1     1     1     1     1      1     1      2        2       2       4                rmpA2_4*-34%
GCF_902827215  2     6     5     15    4     9      5     4      82-19%   70-56%  44-11%  5                -
```

### 4.4 - uneti *output* komandi, a ne komande

```bash
# Upi�ite brojeve kolona koje izdvajate:
98
# Prika�ite izdvojene kolone za Strain, Virulence score i Resistance score
strain         virulence_score  resistance_score
GCF_017743115  4                0
GCF_017743135  4                0
GCF_017815715  3                0
GCF_021057265  4                1
GCF_021442005  4                2
GCF_902723695  4                2
GCF_902723705  4                1
GCF_902827215  5                0
# Odaberite 1 soj koji je samo hipervirulentan (+ ima rmpA2):
GCF_902827215
# Upi�ite informaciju o njegovoj virulentnosti/rezistentnosti sa NCBI/Genome:
hypervirulent Klebsiella pneumoniae
# Odaberite 1 soj koji je hipervirulentan i multirezistentan (+ ima iroB):
GCF_902723695
# Upi�ite informaciju o njegovoj virulentnosti/rezistentnosti sa NCBI/Genome:
Carbapenem resistant and hypervirulent Klebsiella pneumoniae kpn154
```

### 5.3 - uneti komande

```bash
grep -Ei "peg-344|iroB|iucA|rmpA|rmpA2" GCF_902723705.gff
for file in *.gff; do
 echo "=== $file ==="
 grep -Ei "peg-344|iroB|iucA|rmpA|rmpA2" "$file" | grep 'product=' || echo " (ниједан маркер није пронађен)"
done
```

### 2 - uneti komande

```bash
BASE_URL="https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/021/057/265/GCF_021057265.1_ASM2105726v1/"
wget ${BASE_URL}/GCF_021057265.1_ASM2105726v1_genomic.fna.gz
wget ${BASE_URL}/GCF_021057265.1_ASM2105726v1_genomic.gff.gz
wget ${BASE_URL}/md5checksums.txt
wget ${BASE_URL}/uncompressed_checksums.txt
gunzip -k GCF_021057265.1_ASM2105726v1_genomic.fna.gz ; gunzip -k GCF_021057265.1_ASM2105726v1_genomic.gff.gz
grep 'GCF_021057265.1_ASM2105726v1_genomic.fna.gz' md5checksums.txt > genome_compressed.txt
grep 'GCF_021057265.1_ASM2105726v1_genomic.gff.gz' md5checksums.txt >> genome_compressed.txt
#sledi provera
md5sum GCF_021057265.1_ASM2105726v1_genomic.gff.gz 
md5sum GCF_021057265.1_ASM2105726v1_genomic.fna.gz
#ili 
md5sum -c genome_compressed.txt 
```

### 3 - uneti komande

```bash
mkdir {genomes,annotations}
mv GCF_021057265.1_ASM2105726v1_genomic.fna genomes
mv GCF_021057265.1_ASM2105726v1_genomic.gff annotations/
cd ..
tar -czf klebsiella_genome.tar.gz klebsiella_genome/
```

### 4 - uneti komande i sadrzaj klebsiella_download_archive.sh fajla

```bash
mkdir scripts
touch klebsiella_download_archie.sh
#kopiramo sve komande u .sh fajl
chmod +x klebsiella_download_archive.sh
./klebsiella_download_archive.sh

    #sadrzaj fajla klebsiella_download_archive.sh
    #!/bin/bash

    BASE_URL="https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/021/057/265/GCF_021057265.1_ASM2105726v1/"

    wget ${BASE_URL}/GCF_021057265.1_ASM2105726v1_genomic.fna.gz
    wget ${BASE_URL}/GCF_021057265.1_ASM2105726v1_genomic.gff.gz
    wget ${BASE_URL}/md5checksums.txt
    wget ${BASE_URL}/uncompressed_checksums.txt

    gunzip -k GCF_021057265.1_ASM2105726v1_genomic.fna.gz
    gunzip -k GCF_021057265.1_ASM2105726v1_genomic.gff.gz

    mkdir -p {genomes,annotations}

    mv GCF_021057265.1_ASM2105726v1_genomic.fna genomes/
    mv GCF_021057265.1_ASM2105726v1_genomic.gff annotations/

    cd ..
    tar -czf klebsiella_genome.tar.gz klebsiella_genome/
```
