This directory contains part of the files needed to replicate the LAMP primer design.
These are:
- The commands, which are the .sge files in the GLAPD directory, used to run GLAPD and generate the bowtie indexes.
- Some essential information files within the downloads directory. These include a list of the target species, the "common" datasets (ie., the group of genomes for which the primers designed by GLAPD should be valid) and a table (all_accessions.xlsx) that lists the accessions of each of the genomes used in the primer design process. 

The remaining data (the genome sequences) can be downloaded from GenBank; as previously stated, all accessions are listed in all_accessions.xlsx. This data should be placed in the downloads directory.


To replicate the primer design process, first consider what resources are available to you. The .sge scripts are intended to be run on a computer cluster managed by a Sun Grid Engine. They can, however, be adapted to other scheduling systems, but this is beyond the scope of this appendix. 
Second, consider the intermediate files will occupy **very** large amounts of memory, beyond 250GB for the seven design jobs. This is important when using shared resources, or when there is a memory quota. However, once the primer designs are obtained, the intermediate files can be erased, and the final results will be files under 130KB in size.
Third, consider that you must have GLAPD to replicate the design process. The .sge files in the GLAPD directory must be placed within the "GLAPD" directory created when the software is downloaded. The "downloads" directory needs to be placed adjacent to the "GLAPD" directory (not within it).
Finally, some data processing is necessary before running GLAPD. Instructions on how to do this are provided below.


Preliminary data processing instructions:

- Plasmid sequences are removed from the reference target genomes.
 
- As this program cannot use genomes composed of several contigs as reference, these must be joined into one fasta entry per genome. This was done during the design procedure; a spacer was included between the contigs (a sequence of 30N) in order to avoid potential primers being aligned to the gap between contigs. The order in which they were joined was the order in which they were in the original fasta file for the genome. The output of this should be a file named [species name]_noplasmids.fna, placed in the "downloads/representative_targets" directory.

- The previous step should be carried out for all the genome sequences of the target group of genomes of each species, but they should be saved elsewhere (this will be a temporary location). This step is not necessary for the outgroup (the representative genomes of the other, non-target species in the genus). The reasoning for this is that GLAPD considers each fasta entry a separate genome; this is important when considering the "common" targets (every genome must contain the binding sites for the primers), but not when considering the outgroup/non-target genomes (all these genomes will be searched for binding sites and primers designs predicted to bind to any of these will be excluded).

- For each target species, the target genome files plus the non-target genome files should be combined into one large fasta file; these were named [genus]_entire.fna, and placed in the downloads directory. This file must exclude the reference genome of each species.
