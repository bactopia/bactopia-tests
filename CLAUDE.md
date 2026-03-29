# bactopia-tests

This is a **data-only** test fixtures repository for the [Bactopia](https://github.com/bactopia/bactopia) Nextflow pipeline. There is no source code, no build system, and no tests to run here. Changes to this repo are typically adding, updating, or reorganizing test data files.

## Directory Structure

- `species/` - Test data organized by bacterial species (20 species). Each species directory may contain `reads/`, `assembly/`, `compressed/`, and `uncompressed/` subdirectories.
- `datasets/` - Tool-specific reference databases and pre-computed results, organized by tool name.
- `empty/` - Empty placeholder files used to test error handling in the Bactopia pipeline.

## Important Notes

- Several entries in `datasets/` are **symlinks** to `/data/cache/databases/` (bakta, checkm2, eggnog, gtdbtk, kraken2, midas, nohuman, sketcher, srahumanscrubber, sylph). These will not resolve on most machines and are not tracked in git.
- Binary and compressed files (`.fastq.gz`, `.msh`, `.tar`) are common -- do not attempt to read or parse them as text.
- This repo is referenced by the main [bactopia](https://github.com/bactopia/bactopia) repository for CI/CD testing.
