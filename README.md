# GWAS in maize with statgenGWAS

Reproducible genome-wide association study in R: marker QC, mixed-model GWAS with
a kinship matrix, QQ and Manhattan plots, for grain yield and flowering time.

**Question:** which genomic regions are associated with grain yield and anthesis in maize?

**Data:** public DROPS dataset shipped with the `statgenGWAS` package: 246 maize genotypes,
about 42,000 SNPs with chromosome positions, and field-trial phenotypes (trial `Mur13W`).
It is a well-known example dataset, so the project demonstrates the workflow, not a new finding.

## Pipeline
1. Build a genomic data object (markers, map, phenotypes)
2. Marker QC: remove duplicate and low-quality SNPs
3. Phenotype distributions
4. Single-trait GWAS with a kinship-based mixed model
5. QQ plots, Manhattan plots, and a cross-trait QTL plot

## Run it
```r
install.packages(c("statgenGWAS", "ggplot2", "rmarkdown"))
rmarkdown::render("analysis.Rmd")
```
The data comes with the package, so nothing needs to be downloaded.

## Results
- **Data after QC:** 36,624 SNPs on 10 chromosomes for 246 maize genotypes (duplicate SNPs removed; no SNP filtered for low minor allele frequency).
- **Model:** linear mixed model with an Astle kinship matrix, trial Mur13W. Genomic inflation factors were 0.99 (grain yield) and 0.97 (anthesis), so population structure was well controlled.
- **Grain yield:** 5 significant SNPs at a LOD threshold of 5.86 (smallest p-value 2.3e-7). All five fall in a single peak on chromosome 6, so they represent one candidate locus, not five independent signals.
- **Anthesis (flowering time):** no SNP reached significance in this trial.

The full code, plots (QQ, Manhattan, cross-trait QTL plot) and session information are in `analysis.Rmd` and the rendered `analysis.html`. Full results table: `results/gwas_Mur13W_all_snps.csv`.

## Limitations
- 246 genotypes and one trial limit power; small-effect loci are likely missed.
- Significant SNPs are candidate regions, not proven causal variants. Validating them would need independent data or functional work.
- Results come from one trial; effects can change across environments.
