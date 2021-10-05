# read-it-and-keep
Read contamination removal.


## Install
Install either from source or build a singularity container.

### Compile from source
Make the executable `src/readItAndKeep` by running:
```
cd src && make
```

### Singularity container
Build a singularity container by cloning this repository
and running:
```
sudo singularity build readItAndKeep.sif Singularity.def
```


## Usage
Required options:
1. `--ref_fasta`: reference genome in FASTA format.
2. `--reads1`: at least one reads file in FASTA[.GZ] or FASTQ[.GZ] format.
3. `-o,--outprefix`: prefix of output files.


Run on one file of reads:
```
readItAndKeep --ref_fasta ref_genome.fasta --reads1 reads1.fq.gz -o out
```
It will output `out.reads.fastq.gz`.

Run on paired reads, in two files `reads1.fq.gz` and `reads2.fq.gz`:
```
readItAndKeep --ref_fasta ref_genome.fasta --reads1 reads1.fq.gz --reads2 reads2.fq.gz -o out
```
It will output `out.reads_1.fastq.gz` and
`out.reads_2.fastq.gz`.

If the input reads files are in FASTA format, then it will output reads in
FASTA format, calling the files `*.fasta.*` instead of `*.fastq.*`.

It always writes the counts of input and output reads to `STDOUT` in
tab-delimited format, for example:
```
Input reads file 1	1000
Input reads file 2	1000
Kept reads 1	950
Kept reads 2	950
```
All logging messages sent to `STDERR`.


## Tests

These are under development. To run them you will need:
1. Python 3
2. Python package [pytest](https://docs.pytest.org/en/stable/) (`pip install pytest`)
3. Python package [pyfastaq](https://github.com/sanger-pathogens/Fastaq)  (`pip install pyfastaq`)
4. [ART read simulator](https://www.niehs.nih.gov/research/resources/software/biostatistics/art/index.cfm)
   installed, so that `art_illumina` is in your `$PATH`
5. [badread](https://github.com/rrwick/Badread) for nanopore read simulation.

Run the tests after compiling the source code, ie:
```
cd src
make
make test
```
