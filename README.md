Project u12
===========

## Install ##

+ You will need KorfLab/grimoire

## Programs ##

+ `u12` - base program for doing stuff

## Files ##

+ `1pct.fa.gz` - 1% of the A. thaliana genome
+ `1pct.genes.gff3.gz` - 1% of the A. thaliana genes
+ `1pct.splice.gff3.gz` - 1% of the A. thaliana splices (RNA-seq introns)
+ `at.genome.fa.gz` - complete genome TAIR10
+ `at.genes.gff3.gz` - complete set of genes TAIR10
+ `at.splices.gff3.gz` - complete set of RNA-seq introns TAIR10
+ `at.introns.tsv.gz` - the result of the Build procedure below

## Build ##

Used the `1pct...` files for testing.

```
./u12 introns --fasta 1pct.fa.gz --splices 1pct.splices.gff3.gz
```

This will output a tab-delimited file that looks something like below, which
shows the chromosome, begin, end, strand, count, and sequence for every intron
in the splices file. 

```
Chr1    3877    3995    +       2       GTCAACATCTGTAG...
Chr1    3912    3993    -       2       GTTCAAAACAAAAA...
Chr1    3914    3995    +       1363    GTAAGTTCCGAATT...
Chr1    4277    4485    +       1021    GTTTTCTTCTATTC...
```

The introns for the entire genome result in an 87M file (16M compressed).

```
./u12 introns --fasta at.genome.fa.gz --splices at.splices.gff3.gz > at.introns.tsv
gzip introns.tsv
```

To find overlapping introns

```
./u12 overlap --introns at.introns.tsv.gz
```

Some stats about the splice sites

```
./u12 stats --introns at.introns.tsv.gz
```
