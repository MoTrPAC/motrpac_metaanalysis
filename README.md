# motrpac_metaanalysis

This repository can be used to reproduce the preprocessing and (meta-)analysis of publicly available genomic exercise studies. Currently, only human gene expression data were analyzed. Manually curated metadata of all samples can be found [here](https://storage.googleapis.com/motrpac-portal-user-davidama/GEO_sample_metadata.xlsx).

These are the preprocessing scripts that generate data matrices and summary statistics:
1. human_ge_data_download.R - this script downloads data and some metadata and keeps all files locally. 
2. human_ge_data_preprocessing.R - this script uses the downloaded files to create a data matrices for each cohort, of which one is a matrix of summary statistics (e.g., mean and variance of fold change per gene)

The output of the preprocessing flow is an RData file per subsection of the database. These are the current available files:
1. [human_ge_cohort_preprocessed_db_acute.RData](https://storage.googleapis.com/motrpac-portal-user-davidama/human_ge_cohort_preprocessed_db_acute.RData) - acute bout cohorts
2. [human_ge_cohort_preprocessed_db_longterm.RData](https://storage.googleapis.com/motrpac-portal-user-davidama/human_ge_cohort_preprocessed_db_longterm.RData) - long-term training program cohorts

Loading each of these files will add the following objects to the R session:
1. cohort_data: a list of cohort datasets. Each entry in the list has a name and a group of data matrices:
  1. probe_data - probe level of microarray experiments. Can be transcript data for RNA-Seq datasets.
  2. gene_data - a gene level data that results from averaging rows in the probe_data matrix
  3. (Optional if preprocessing was successful) gene_fold_changes - for each gene and subject this matrix contains the fold change of a time-point vs. the base line.
  4. (Optional if preprocessing was successful) probe_fchanges - same as above, but computed using a slower algorithm. Was currently kept for QA reasons.
  5. (Optional if preprocessing was successful) time2ttest_stats - this matrix gives the **summary statistics** for each gene and each time point that is not the baseline: mean and variance of fold change, and the p-value of a paired t-test. 

For questions and suggestions please contact us at davidama@stanford.edu
