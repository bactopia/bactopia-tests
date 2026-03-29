# bactopia-tests

Test datasets for [Bactopia](https://github.com/bactopia/bactopia), a Nextflow pipeline for
the complete analysis of bacterial genomes. This repository provides sequencing reads,
assemblies, reference databases, and pre-computed results used by Bactopia's CI/CD tests.

## Testing Quick Start

Here's a quick setup for using bactopia-tests with the latest tests from bactopia. This
might be out of sync with latest bactopia builds, so please refer to them for the 
latest instructions.

```{bash}
mkdir ~/bactopia-repos
cd ~/bactopia-repos
git clone https://github.com/bactopia/bactopia.git
git clone https://github.com/bactopia/bactopia-py.git
git clone https://github.com/bactopia/bactopia-tests.git
git clone https://github.com/bactopia/nf-bactopia.git

# Create and activate a conda environment for bactopia-dev
cd bactopia
conda create -y -n bactopia-pev -f environment.yml
conda activate bactopia-pev

# Install latest bactopia-py from source
cd ../bactopia-py
just install

# Install nf-bactopia plugin
cd ../nf-bactopia
make assemble
make install

# Run tests using the test datasets
cd ../bactopia
# test modules
bactopia-test \
    --bactopia-path ~/bactopia-repos/bactopia \
    --test-data ~/bactopia-repos/bactopia-tests \
    --tier modules \
    --jobs 4

# test subworkflows
bactopia-test \
    --bactopia-path ~/bactopia-repos/bactopia \
    --test-data ~/bactopia-repos/bactopia-tests \
    --tier subworkflows \
    --jobs 4

# test workflows
bactopia-test \
    --bactopia-path ~/bactopia-repos/bactopia \
    --test-data ~/bactopia-repos/bactopia-tests \
    --tier workflows \
    --jobs 4

# test everything
bactopia-test \
    --bactopia-path ~/bactopia-repos/bactopia \
    --test-data ~/bactopia-repos/bactopia-tests \
    --tier all \
    --jobs 4
```

## Directory Structure

```
bactopia-tests/
├── species/      # Test data organized by bacterial species
├── datasets/     # Tool-specific reference databases and results
└── empty/        # Empty placeholder files for error handling tests
```

## Species

| Species | Accession(s) | Genome Size | Data Types |
|---------|--------------|-------------|------------|
| *Bacillus anthracis* | GCF_000008445 | - | Assembly |
| *Escherichia coli* | GCF_001695515 | 5.87 Mb | Assembly |
| *Escherichia coli* (mcr-1) | GCF_001682305 | 4.62 Mb | Assembly |
| *Glaesserella parasuis* | GCF_002777395 | 2.48 Mb | Assembly |
| *Haemophilus influenzae* | GCA_000027305, GCF_900478275 | 1.89 Mb | Assembly, Annotation |
| *Klebsiella pneumoniae* | GCF_000009885 | 5.47 Mb | Assembly |
| *Legionella pneumophila* | GCF_000048645 | 3.64 Mb | Assembly |
| *Listeria monocytogenes* | GCF_002285835 | 3.15 Mb | Assembly |
| Mixed | Multiple | - | Illumina reads, Annotations |
| *Neisseria gonorrhoeae* | GCF_001047255 | 2.17 Mb | Assembly |
| *Neisseria meningitidis* | GCF_003355215 | 2.31 Mb | Assembly |
| *Portiera* | SRR2838702, ERR3772599 | 358 kb | Illumina, Nanopore, Assembly, Annotation, Sketches |
| *Pseudomonas aeruginosa* | GCF_000006765 | 6.26 Mb | Assembly |
| *Salmonella enterica* | GCF_016028495 | 4.97 Mb | Assembly |
| *Shigella boydii* | GCF_016726285 | 4.55 Mb | Assembly |
| *Shigella dysenteriae* | GCF_002949675, ERR6005894, SRR13039589 | 4.58 Mb | Assembly, Illumina, Nanopore |
| *Staphylococcus aureus* | GCF_000017085 | 2.90 Mb | Assembly |
| *Streptococcus pneumoniae* | GCF_001457635, ERR1438863 | 2.11 Mb | Assembly, Illumina |
| *Streptococcus pyogenes* | GCF_006364235 | 1.91 Mb | Assembly |
| *Streptococcus suis* | GCF_002285535 | 2.07 Mb | Assembly |

## Datasets

**Databases**

| Dataset | Description |
|---------|-------------|
| amrfinderplus | AMRFinderPlus antimicrobial resistance gene database |
| ariba | ARIBA pre-processed CARD and VFDB databases |
| defensefinder | DefenseFinder bacterial defense system models |
| emmtyper | EMM type reference sequences for *S. pyogenes* |
| ismapper | IS element reference sequences |
| mlst | Multi-locus sequence typing allele and profile database |
| variants | RefSeq genome Mash sketches |

**Test Sequences**

| Dataset | Description |
|---------|-------------|
| blast | Gene, primer, and protein sequences for BLAST searches |
| generic | Reference genomes, GFFs, metadata, and pan-genome data |
| mapping-sequences | Short reference sequences for read mapping |

**Pre-computed Results**

| Dataset | Description |
|---------|-------------|
| bracken | Bracken taxonomic classification output |
| genotyphi | GenoTyphi *Salmonella* Typhi genotyping output |
| rgi | RGI/CARD resistance gene identifier output |
| snippy | Snippy variant calling output (VCF and aligned FASTA) |
| tbprofiler | TBProfiler results for Illumina and Nanopore |

**Symlinked Databases**

The following datasets are symlinks to large external database caches and are not tracked in this repository: bakta, checkm2, eggnog, gtdbtk, kraken2, midas, nohuman, sketcher, srahumanscrubber, sylph.

## Empty Files

The `empty/` directory contains 21 empty files (e.g., `EMPTY_R1.fastq.gz`, `EMPTY_ASSEMBLY`) used to verify that Bactopia handles missing or empty input gracefully.

## Machine-Readable Files

- `llms.txt` -- LLM-friendly project overview ([llmstxt.org](https://llmstxt.org/) format)
- `catalog.json` -- Structured metadata for all species, datasets, and files

## License

[MIT](LICENSE)
