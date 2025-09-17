# Download Kraken2 database

The kraken2 database is too large to be put in this repo. Instead, you will need to download
it yourself. For testing purposes, we can just make use of the latest Standard-8 build.

To get the database, run the following command:

```{bash}
# For latest URL visit: https://benlangmead.github.io/aws-indexes/k2
wget -O kraken2.tar.gz https://genome-idx.s3.amazonaws.com/kraken/k2_standard_08_GB_20250714.tar.gz
```

For testing purposes, we'll need both the original tarball and the extracted tarball. So, be
sure to keep the original tarball.

```{bash}
tar -xzvf kraken2.tar.gz
```
