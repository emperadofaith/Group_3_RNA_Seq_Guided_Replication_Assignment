# Group 3 - Infection
Behante, Fretz Ivan - Literature lead

Cadungong, Ella Pearl - Data lead

Emperado, Faith Denielle - Documentation lead

Gregorio, Richelle - Interpretation lead

Iljan, Shane Mae - Galaxy lead

Vertudazo, Maria Ryzah May - Interpretation lead

**Paper citation:** Nickerson, K. P., Senger, S., Zhang, Y., Lima, R., Patel, S., Ingano, L., Flavahan, W. A., Kumar, D. K. V., Fraser, C. M., Faherty, C. S., Sztein, M. B., Fiorentino, M., & Fasano, A. (2018). Salmonella Typhi Colonization Provokes Extensive Transcriptional Changes Aimed at Evading Host Mucosal Immune Defense During Early Infection of Human Intestinal Tissue. EBioMedicine, 31, 92–109. https://doi.org/10.1016/j.ebiom.2018.04.005 

**Research Question:** How does Salmonella Typhi interact with the human small intestinal mucosa during the initial stages of infection to reprogram host gene expression, rearrange cellular machinery, and evade mucosal immune defenses to establish infection?

**Organism and tissue used:** Intestinal tissue of Human

**Control and Treatment conditions:** Non-infected; mock-treated human intestinal biopsies for control and human infected intestinal biopsies for treatment condition.

| Run Accession Numbers |
| -------------------- |
| SRR702901            |
| SRR702902            |
| SRR702903            |
| SRR702904            |
| SRR702905            |
| SRR702906            |
| SRR702907            |

| Reference Genome | Annotation Version |
| ---------------- |  ----------------
| GRCh38           | GRCh38.78 |

**Author's Analysis Pipeline:** RNA was extracted and sequenced using Illumina HiSeq 2500. Reads underwent quality control using FastQC, followed by alignment to the human genome using TopHat and to the S. Typhi Ty2 genome using Bowtie. Reads were counted using HTSeq, and differential gene expression was analyzed using DESeq. 

**Galaxy Pipeline Used:**

**Main Quality Control Results**

Quality control was performed on the six selected RNA-seq samples using FastQC in Galaxy to assess the overall quality of the sequencing data. The individual FastQC reports were then summarized using the MultiQC tool in Galaxy for easier comparison among the samples. The results were examined based on the number of reads, general sequence quality, adapter contamination, overrepresented sequences, and other possible quality problems. The summarized quality control results are presented in below.

Table 1. RNA-Seq read quality, adapter contamination, sequence composition, and duplication profiles of uninfected and infected tissue biopsies.
| **Sample** | **Run Accession** | **Condition** | **Reads** | **Sequence Quality** | **Adapter Contamination** | **Overrepresented Sequences** | **Quality Issues** |
|---|---|---|---:|---|---|---|---|
| Control_rep1 | SRR7029701 | Uninfected tissue biopsy | 20.80 M | Pass (🗸) | Pass (🗸) | Warning (!) | Warning in per-base sequence content, per-sequence GC content, duplication levels, and overrepresented sequences |
| Control_rep2 | SRR7029702 | Uninfected tissue biopsy | 23.5 M | Pass (🗸) | Pass (🗸) | Warning (!) | Warning in per-base sequence content, per-sequence GC content, duplication levels, and overrepresented sequences |
| Control_rep3 | SRR7029703 | Uninfected tissue biopsy | 22.6 M | Pass (🗸) | Pass (🗸) | Warning (!) | Per-sequence GC content and sequence duplication levels failed; warnings in per-base sequence content and overrepresented sequences |
| Infected_rep1 | SRR7029705 | Infected tissue biopsy | 23.8 M | Pass (🗸) | Pass (🗸) | Warning (!) | Per-sequence GC content and sequence duplication levels failed; warnings in per-base sequence content and overrepresented sequences |
| Infected_rep2 | SRR7029706 | Infected tissue biopsy | 21.1 M | Pass (🗸) | Pass (🗸) | Warning (!) | Per-sequence GC content and sequence duplication levels failed; warnings in per-base sequence content and overrepresented sequences |
| Infected_rep3 | SRR7029707 | Infected tissue biopsy | 24.4 M | Pass (🗸) | Pass (🗸) | Warning (!) | Per-sequence GC content and sequence duplication levels failed; warnings in per-base sequence content and overrepresented sequences |

All six RNA-seq libraries produced adequate sequencing depth (20.1–24.4 million reads) and passed overall sequence-quality and adapter-contamination assessments, indicating generally reliable read quality. All samples showed overrepresented sequences and warnings for per-base sequence composition, GC-content distribution, and sequence duplication, suggesting potential transcript abundance bias or technical variation. Control_rep3 and Infected_rep1 failed the per-sequence GC-content assessment, while Infected_rep2 and Infected_rep3 additionally failed the sequence-duplication assessment, indicating reduced library complexity or possible PCR amplification bias. The datasets are suitable for downstream RNA-seq analysis, but these quality-control features should be considered during preprocessing and interpretation of differential gene expression.

**Mapping Results**

The selected RNA-seq samples were mapped to the Homo sapiens GRCh38 reference genome using TopHat in Galaxy, following the alignment approach used in the original study. The same mapping settings were applied consistently to all three control and three infected samples. After alignment, the total reads, percentage mapped, percentage uniquely mapped, and any unusually low mapping results were recorded to evaluate the success of the alignment. The mapping results for all six samples are presented in below.

Table 2. Mapping Statistics of the Selected RNA-Seq Samples Using TopHat
| **Sample** | **Total Reads** | **Percentage Mapped** | **Percentage Uniquely Mapped** | **Unusually Low Mapping?** |
|---|---:|---:|---:|:---:|
| SRR7029701 | 20,768,901 | 96.1% | 77.5% | No |
| SRR7029702 | 23,483,399 | 96.7% | 77.5% | No |
| SRR7029703 | 22,642,554 | 95.4% | 73.1% | No |
| SRR7029705 | 23,750,360 | 93.1% | 67.6% | No |
| SRR7029706 | 20,081,963 | 93.9% | 56.5% | No |
| SRR7029707 | 24,357,703 | 89.7% | 61.3% | Yes |

This table shows the result after mapping statistics of the selected RNA-sequence samples using TopHat which reveals that most of the RNA-seq reads successfully matched to the human genome, while the SRR7029707 is the only one that showed unusually low mapping compared to others which could indicate that it may still need a further checking.

**Differential Expression Results**

Differential gene expression analysis was performed using DESeq2 in Galaxy to compare the three S. Typhi-infected samples with the three control samples. The control condition was used as the reference. DESeq2 generated the log2 fold change and adjusted p-value for each gene, which were used to identify significantly upregulated and downregulated genes. Galaxy's DESeq2 output reports the gene ID, base mean, log2FC, standard error, Wald statistic, p-value, and adjusted p-value.

Table 3. Summary of Differential Gene Expression Analysis.
| **DESeq2 Result** | **Result** | **Interpretation** |
|---|---:|---|
| Genes tested | 8,848 | Total genes included in the DESeq2 analysis |
| Significantly differentially expressed genes | 32 | Genes with adjusted *p*-value < 0.05 |
| Positive log2 fold change | 10 | Significantly higher expression in the infected group |
| Negative log2 fold change | 22 | Significantly lower expression in the infected group |
| Adjusted *p*-value (FDR) threshold | < 0.05 | Threshold used to determine statistical significance |

The result based on the DESeq2 results, 32 genes were found to be significantly different between the infected and normal groups. Ten genes were more active, while 22 were less active in the infected group. This shows that the infection had an effect on gene expression.

**Interpreted Genes** 

Table 4. Biological Interpretation of Selected Differentially Expressed Genes.
| **Gene ID** | **Gene Name** | **log2FC** | **Adjusted *p*-value** | **Regulation** | **Known / Predicted Function** | **Possible Connection to Infection** |
|---|---|---:|---:|---|---|---|
| ENSG00000159189 | **C1QC** | 1.2847 | 0.01194 | Upregulated | Component of C1q involved in activation of the classical complement pathway and immune defense against pathogens (Kishore & Reid, 2000). | Increased C1QC expression may be associated with the host immune response to *S. Typhi* infection, as the complement system participates in host defense against *Salmonella* and interacts directly with *S. Typhi* during infection (Guerra et al., 2025). |
| ENSG00000114771 | **AADAC** | 1.2308 | 0.01194 | Upregulated | Microsomal serine esterase involved in drug and lipid metabolism, including the hydrolysis of triglycerides and cholesterol esters (Yang et al., 2025). | AADAC may be involved in infection-associated changes in host lipid metabolism. In HCV-infected cells, reduced AADAC was associated with impaired triglyceride lipolysis, while AADAC knockdown also affected viral production, demonstrating that AADAC can function as a host factor during infection (Nourbakhsh et al., 2013). |
| ENSG00000169894 | **MUC3A** | -1.2790 | 0.02171 | Downregulated | Encodes a cell-surface-associated mucin that contributes to the protective and lubricating barrier of mucosal surfaces (NCBI, 2026). | Downregulation of MUC3A may reflect alterations in the intestinal mucosal barrier during infection, as intestinal mucins contribute to epithelial defense and protection against *Salmonella* infection (Han et al., 2024). |
| ENSG00000177169 | **ULK1** | -1.0416 | 0.03695 | Downregulated | Encodes a serine/threonine kinase that plays a key role in initiating and regulating autophagy, including autophagosome formation (NCBI, 2026). | Downregulation of ULK1 may indicate altered autophagy-related host defense during infection, as *Salmonella* can suppress autophagy through mTORC1-mediated inhibition of ULK1, which may promote bacterial survival (Torsilieri et al., 2024). |
| ENSG00000176945 | **MUC20** | -1.3557 | 0.01032 | Downregulated | Transmembrane mucin involved in maintaining epithelial barrier integrity and participating in cellular signaling and immune responses at epithelial surfaces (Montero et al., 2025). | Downregulation of MUC20 may indicate changes in the intestinal mucosal barrier during infection, as an enhanced mucosal barrier has been shown to reduce the invasion of *Salmonella enterica* in human small intestinal epithelial cells (Yamazaki et al., 2024). |

The DESeq2 results identified five significant genes associated with S. Typhi infection, including C1QC and AADAC, which were upregulated, and MUC3A, ULK1, and MUC20, which were downregulated. These genes are mainly involved in immune defense, lipid metabolism, mucosal barrier integrity, and autophagy. Overall, the changes suggest that S. Typhi infection may alter host immune responses, intestinal barrier function, and cellular defense mechanisms. 
