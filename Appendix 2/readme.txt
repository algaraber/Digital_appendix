Primer selection
----------------

The scripts in this directory were used to draw graphs depicting the distance of any pair of binding sites for each of the LAMP primer sets designed on non-target genomes. All genomes from Genbank were searched by BLAST. Those primer sets where primers did not bind to any two close binding sites on a non-target genome were considered unlikely to amplify the DNA of any non-target organism that was present in GenBank. This guided the selection of primer sets to be synthesised and tested.
The procedure could be replicated by following the instructions in this readme file.

Prerequisite software (must be installed before starting):
- NCBI's blast suite 
- ete3

First, unzip and place these files in the desired working directory.

Second, place all the final output files of GLAPD with the primer sequences (ended in .txt) here.

Third, run the scripts in this directory in the following order. It is recommended that they are run one by one. 


### Scripts in order: ###

bash splitter.sh *_primers.txt  
bash subshelling.sh [directory name]/*.fna # This one needs the user (you!) to introduce the name of the directory where the fna files were placed manually.
for i in *_set*.out ; do bash namer_old.sh $i ; done

bash repurge.sh *_primers_ready/*set{1..20}.csv # Takes a long time to run!
bash dividing_by_primer.sh *_repurged/*_set{1..20}_repurged.csv # Very fast.
bash counting_matches.sh *_repurged/*_set{1..20}_repurged.csv # Why does it take the same input as the previous step? Does it add a column or something?
bash cumsum.sh *_repurged/*.PA.tsv
bash matchnummer_repurged.sh
bash specificity_checks2.sh *_repurged/*_set{1..20}_repurged.csv  # Makes *_PAD directories with several files that contain distances between primer pairs that fall on the same contig.
bash aggregating_dists.sh

R Primer_pair_dist_graphs3.R

### End of scripts ###

