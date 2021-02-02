# GOOGLER

Make a uniq gene list

```
cat XT7_WY_fmt6_out | cut -f 2 | uniq > WY_uniq_genes.tsv
```

Info on how to start building github programs can be found in

```bash

https://github.com/processing/processing/wiki/Build-Instructions
```
(start with this if you have not set this up already)

Then clone googler from github

```bash
git clone https://github.com/jarun/googler.git
```

Then go to the directory and build it if needed

```bash
cd googler/
make
```

Then you can use googler by

```bash
Path/to/googler/googler -options
```

Following will google all the genes in the tsv file, select top 5 hits and check whether they have something to do with the keywords gene, sex and save the output in a file named after the gene

```bash
for gene in $(cat test_genes.tsv); do echo "\n"| ../googler/googler -n 5 $gene | grep 'gene\|sex'>google_hits/$gene ; echo checked $gene; done
```
