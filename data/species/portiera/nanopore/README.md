## Nanopore Test Data Creation
I've been using _Candidatus Portiera aleyrodidarum_ for my test data because it has a 350kb genome size. There was already
Illumina seqeuncing for it, but not Nanopore. However there was Nanopore (ERX3774356) microbiome sequencing of 
_Bemisia tabaci_ (white fly) which contains _C. aleyrodidarum_ (its an endosymbiont, see 
https://dx.doi.org/10.1128%2FAEM.02976-12 for more info).

So I thought, why not just extract _C. aleyrodidarum_ reads from the microbiome sequencing of _B. tabaci_. Below outlines
how I went about that.

```
# Download B. tabaci nanopore sequencing (ERX3774356)
fastq-dl ERX3774356 SRA --cpus 8 --group_by_experiment
```

```
# Map reads to a completed C. aleyrodidarum genome (GCF_000292685)
minimap2 -x map-ont -a GCF_000292685.fna ERX3774356.fastq.gz  > aln.sam
```

```
# Extract the mapped reads
samtools fastq -F 4 aln.sam > output.fastq
```

```
# Get enough about mapped reads
cat output.fastq | fastq-scan -g 358242
{
    "qc_stats": {
        "total_bp": 583922467,
        "coverage": 1629.97,
        "read_total": 293643,
        "read_min": 131,
        "read_mean": 1988.55,
        "read_std": 2277.21,
        "read_median": 1238,
        "read_max": 61116,
        "read_25th": 707,
        "read_75th": 2360,
        "qual_min": 8,
        "qual_mean": 13.3032,
        "qual_std": 1.4851,
        "qual_max": 18,
        "qual_median": 14,
        "qual_25th": 12,
        "qual_75th": 14
    },
... TRUNCATED ...
}
```

```
# Randomly subsample 40x coverage
rasusa -i /home/robert_petit/repos/bactopia-tests/temp/output.fastq -c 40 -g 354000 -s 42 > ERR3772599.fastq
gzip --best ERR3772599.fastq
```

