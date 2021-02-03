# GOOGLER – sex determining genes

Make a unique gene list

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
Run the following changing the path to googler,
this will google all the genes in the tsv file as gene $gene_name, select top 15 hits and check whether they have something to do with the keyword ‘sex’ and save the output in a file named after the gene


```bash
echo please enter your file name WITH file format :  ;read filename; echo your search results are in $filename; mkdir ${filename%%.tsv}; for gene in $(cat $filename); do echo "\n"| ../googler/googler -n 15 $gene gene | grep 'sex'>${filename%%.tsv}/$gene ; echo checked $gene; done
```

Then run following to separate genes with no hits
```
cd ${filename%%.tsv}
mkdir files_with_no_hits
find . -type f -maxdepth 1 -size -5c -exec mv {} files_with_no_hits/ \;

cd ..
```

# * when you use large lists, google may banne your ip due to unusual activity. In that case use a vpn and use the following command to split your csv into smaller files and then google them

```bash
split -b1k WZ_uniq_genes.tsv
```
