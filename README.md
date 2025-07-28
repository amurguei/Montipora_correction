# Montipora_correction
Attempts to correct artifacts in Montipora capitata developmental timeseries (3 life stages)

The Montipora capitata developmental timeseries has an artifact that is likely inflating the separation between the spat from the other samples. This is likely influencing the downstream multi species analysis. 

Firstly, I re-ran the mapping in Hive, since the original analysis was done in Andromeda (now closed), and the MultiQC reports I had from such analysis were not very conclusive (only ran before and after trimming). In the new attempt I ran MultiQC also the Hisat2 logs, feature counts (for diagnostic purposes, as the counts were originally assigned with PrepDE), and I calculated average Transcript Identity Numbers (TINs) per sample, as I do not have access for RINs for this dataset. This revealed the spat samples had both lower alignment rates & lower TINs, suggesting higher degradation. 

I tested 3 groups of corrections and re-ran PCAs on them. Firstly I included, different variables as covariates in the VST-transformation model (I attempted with alignment rate, TINs, and significant subrogate variables as revealed by SVA analysis). Secondly, I tried to re-residualize the matrixes based on the same variables. Thirdly, I attempted a correction based on a hypothetical batch I termed "spat_status", assumming (I do not actually know this was the case) that the spat samples went on a different sequencing batch and that could be causing the artifact. 

From group 1, results show there is not significant change in the variance explained by PC1 and PC2, however, the spread or range of the X axis does shrink substantially with corrections, particularly with SVA.

From group 2, corrections seem to cause distortions in the data matrix, although PC1 variance is reduced. 

ComBat-seq results appear likewise distorted. 

I tested whether one of the models with the covariates that at least managed to reduce the spread produced a more normal network output with respect to the uncorrected-VST transformed matrix. For this purpose, I used the ddSEQ design with SVA covariates. 

In this repository you can find relevant files for the mapping process (MultiQC reports, bioinformatics code), the WGCNA Montipora code and gene count matrix, and the attempts at corrections code with files.  