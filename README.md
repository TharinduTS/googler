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
# search_genes.sh
Save this as a script named search_genes.sh CHANGING the path to googler,
this will google all the genes in the tsv file as gene $gene gene_name function, select top 15 hits and check whether they have something to do with the keyword ‘sex’ and save the output in a file named after the gene

then it will seperate files with a hit from the rest


```bash
echo please enter your file name WITH file format :  ;read filename; echo your search results are in $filename; mkdir ${filename%%.tsv}; for gene in $(cat $filename); do echo "\n"| ../googler/googler -n 15 $gene gene function | grep 'sex'>${filename%%.tsv}/$gene ; echo checked $gene; done

cd ${filename%%.tsv}
mkdir files_with_no_hits
find . -type f -maxdepth 1 -size -5c -exec mv {} files_with_no_hits/ \;

cd ..
```

# * when you use large lists, google may bann your ip due to unusual activity. In that case use a vpn , save the following as a bash script and then run it. ***you should have saved above script as search_genes.sh before running this **


```bash
echo Please enter the file name to split and search:  ; read filename_with_format ; echo splitting and searching $filename_with_format; echo all files with hits will be collected in XXX_all_hits;echo -en "\n";echo output files will be stored in directories begining with ${filename_with_format%%_uniq_genes.tsv} ;echo -en "\n" ; split -l100 $filename_with_format ${filename_with_format%%_uniq_genes.tsv}_splitted_ ; for i in ${filename_with_format%%_uniq_genes.tsv}_splitted*; do mv $i $i.tsv;done ; for i in ${filename_with_format%%_uniq_genes.tsv}_splitted_*.tsv; do echo $i|bash search_genes.sh;sleep 5; done 

echo -en "\n" ; echo Final list of hits:   ; for i in ${filename_with_format%%_uniq_genes.tsv}_splitted*/; do cd $i; ls -p | grep -v / ;cd ..; done;echo -en "\n"; echo These are all the files with hits ; echo files without hits are in directories labelled no_hits ; echo if no files are listed there were no hits; echo -en "\n"
```

Then you can check for results in all of the the splitted directories all together by

**change WY into whatever the genotype before running**

```bash
echo -en "\n" ; echo Final list of hits:   ; for i in WY_splitted*/; do cd $i; ls -p | grep -v / ;cd ..; done;echo -en "\n"; echo These are all the files with hits ; echo files without hits are in directories labelled no_hits; echo -en "\n"
```
