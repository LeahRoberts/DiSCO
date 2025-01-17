Instruction for replicating analyses in DISCus paper
=======================================================

Tests to validate DISCus:
--------------------------

**ANALYSIS USING KNOWN INVERSION FREQUENCIES:**

The EC958 fasta files contained either a fimS in the OFF orientation (EC958.fasta) or in the ON orientation (EC958_fimS_ON.fasta). The ON orientation file was generated by reverse complementing the 314-bp fimS region from the original EC958 genome sequence (genomes given in "percent_ana" folder).

Following the manual instructions and the given error models in GemSIM (http://sourceforge.net/projects/gemsim/), the following commands were run in order to generate simulated reads:

 	$ python ./GemReads.py -r EC958.fasta -n 10000000 -l 100 -u 300 -s 20 -m models/ill100v4_p.gzip -c -q 64 -o EC958-OFF -p $ python ./GemReads.py -r EC958_fimS_ON.fasta -n 10000000 -l 100 -u 300 -s 20 -m models/ill100v4_p.gzip -c -q 64 -o EC958-ON -p

To parse the reads to give differing proportions of OFF to ON, the files were merged:

	$ head -32000000 EC958-OFF_fir.fastq > EC958-OFF80_1.fastq $ tail -8000000 EC958-ON_fir.fastq >> EC958-OFF80_1.fastq $ head -32000000 EC958-OFF_sec.fastq > EC958-OFF80_2.fastq $ tail -8000000 EC958-ON_sec.fastq >> EC958-OFF80_2.fastq

DISCus was then run using the fastq files and references generated using the the DISCus_create_references.py script (on the genomes in "percent_ana").


**ANALYSIS USING VARYING INVERSION SIZES:**

References with varying pseudo-inversions were created using the coordinates below (from the EC958 genome):

Inversion sizes:

* 150 bp (1827933..1828082)
* 250 bp (1827933..1828182)
* 350 bp (1827933..1828282)
* 500 bp (1827933..1828432)
* 600 bp (1827933..1828532)
* 700 bp (1827933..1828632)
* 800 bp (1827933..1828732)
* 1000 bp (1827933..1828932)
* 1250 bp (1827933..1829182)
* 1500 bp (1827933..1829432)
* 1750 bp (1827933..1829682)
* 2000 bp (1827933..1829932)
* 2500 bp (1827933..1830432)
* 3000 bp (1827933..1830933)

Extra genomes where these regions are inverted (reverse complemented) were manually created. To create reads for both orientations, reads were generated using GemSIM from the fasta references (with the pseudo-inversion).

The command to do this was::

	$ ~/bin/GemSIM_v1.6/GemReads.py -r EC958_complete.fasta -n 2000000 -l 100 -u 300 -s 20 -m ~/bin/GemSIM_v1.6/models/ill100v4_p.gzip -c -q 64 -o EC958_original_paired_sim -p

Once created, the reads were shuffled using a script (available upon request) and were then put through DISCus using the references in "size_ana".


**ANALYSIS OF KNOWN INVERTIBLE REGIONS IN EC958:**

Several region in EC958 are known to invert, namely:

1. the fimS region upstream of type 1 fimbriae
2. the promoter region for hyxR in the PAI-X pathogenicity island
3. Prophage tail fibres, namely Phi1, Phi2 and Phi4

Using Illumina paired-end sequencing reads for EC958 grown with shaking overnight (D0) or after 5 days grown statically (D5), DISCus was run to analyse the inversion of these region between the two samples. All reference files are given in the appropriate folders. The fastq files are available upon request. 


Analysis of fimS invertible region in ST131 lineage:
------------------------------------------------------

The fimS region was then analysed using Illumina paired-end sequencing reads for 95 ST131 strains, using the fimS region from EC958 as the pseudo-reference.

Reads used for this analysis are available on EMBL-EBI (Study accession ERR161327).



Metagenomic Analysis:
----------------------

**Reads:***

Reads were obtained from the paper "Single Clinical Isolates from Acute Urinary Tract infections are representative of dominant in situ populations" - doi: 10.1128/mBio.01064-13.

Using the fasta files in "metagenomic_pseudo_refs" (which are whole genome assemblies of the dominant isolate strain from each sample), the necessary references for use with DISCus were manually created to analyse the fimS region (this process can now be automated with the DISCus_create_references.py script). Using these pseudo-references, the metagenomic reads were mapped using DISCus, and inversion frequencies calculated.


