# data

Here, all data is stored, which was used to generate the results.

## reference_sequences

Includes reference sequences as< well as anotation files.

## fastq

Contains all raw fastQ files



## libs

trimmed libraries, with fastqc htmls 



## link_lt_gn.tab

- created 4 Dez 2020

Tab file connecting locus tag names to gene names. Used in r-scripts for linking. It was created using the gff reference file 

how it was created (bash command):

```bash
grep -P "(\tgene\t)|(\tpseudogene\t)|(\rRNA\t)|(\tRNA\t)" ./reference_sequences/FQ312003.1.gff |\
cut -f9 | \
sed -r 's/^.*Name=([^;]+).*;locus_tag=([^; ]+).*$/\1\t\2/' | \
sed -r 's/^ID=.*Name=([^;]+).*$/\1\t\1/'  > link_lt_gn.tab
```



## PHOPQ.tsv

genes related to PHOPQ

