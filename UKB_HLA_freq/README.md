# HLA allelotype frequencies in the UK Biobank

We provide the HLA allelotype frequencies in UK Biobank.
The allelotype frequencies are computed using unrelated set of individuals in the following 5 populations.

- White British (`white_british`, N = 337,138)
- Non-British White (`non_british_white`, N = 24,905)
- South Asian (`s_asian`, N = 7,885)
- African (`african`, N = 6,497)
- East Asian (`e_asian`, N = 1,154)

Our population definitions are based on a combination of self-reported ethnicity data and genotype PCs provided by UK Biobank. Our sample QC procedure is described in our manuscript[1] (we have updated the definition since the initial draft of this manuscript and we are still preparing the updated manuscript at this moment).

We computed the allelotype frequency using `--freq` and `--geno-counts` subcommands in PLINK v2.00a3LM[2,3].

Also, our initial HLA allelotype analysis is briefly described in our paper[4].

## Data files

We have the following 4 files for the 5 populations.

- `ukb_hla_v3.${population}.afreq.zst`: the output from the `--freq` command. The file format is described [here](https://www.cog-genomics.org/plink/2.0/formats#afreq).
- `ukb_hla_v3.${population}.afreq.log`: the log files from the `--freq` command.
- `ukb_hla_v3.${population}.gcount.zst`: the output from the `--geno-counts` command. The file format is described [here](https://www.cog-genomics.org/plink/2.0/formats#gcount).
- `ukb_hla_v3.${population}.gcount.log`: the log files from the `--geno-counts` command.

### Zstandard compression of the output files

The output files are compressed with Zstandard[5].
You can read the file with the following commands:

```{bash}
# example in bash
zstdcat <file>.zst | head
```

From `R`, you may read the tables like this:

```{R}
# example in R
df <- data.table::fread(cmd=paste('zstdcat', zst_file))
```

## Reference

1. [Sinnott-Armstrong, N. et al. Genetics of 38 blood and urine biomarkers in the UK Biobank. bioRxiv 660506 (2019)](https://doi.org/10.1101/660506).
2. [Chang, C. C. et al. Second-generation PLINK: rising to the challenge of larger and richer datasets. Gigascience 4, (2015)](https://doi.org/10.1186/s13742-015-0047-8).
3. [PLINK 2.0](https://www.cog-genomics.org/plink/2.0/).
4. [McInnes, G. et al. Global Biobank Engine: enabling genotype-phenotype browsing for biobank summary statistics. Bioinformatics (2019)](https://doi.org/10.1093/bioinformatics/bty999).
5. [Zstandard - Real-time data compression algorithm](https://facebook.github.io/zstd/).