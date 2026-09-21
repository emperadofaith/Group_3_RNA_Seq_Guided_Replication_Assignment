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

**Comparison of the Original Study and Galaxy Re-analysis Pipeline**

To examine how closely the Galaxy re-analysis reproduced the published study, the main analysis steps and results were compared. The comparison focused on the dataset, quality control, reference files, alignment, gene counting, differential expression, significance criteria, and major biological findings.

Table 1. Comparison of the Original RNA-Seq Analysis and the Galaxy Re-analysis.
| **Analysis Step** | **Original Authors** | **Our Galaxy Re-analysis** |
|---|---|---|
| **RNA-seq dataset** | The original study analyzed four uninfected human intestinal biopsy samples and five *S. Typhi* infected biopsy samples, together with four bacterial control samples for a separate bacterial analysis. | Six human intestinal biopsy samples were analyzed, consisting of three uninfected controls and three *S. Typhi* infected samples. |
| **Quality control** | The original authors assessed sequence quality using FastQC version 0.10.0. | FastQC version 0.12.1 and MultiQC were used to assess and summarize the quality of all six samples. |
| **Trimming** | The original authors did not report performing a read-trimming step before alignment. | Read trimming was not performed because all samples showed good per-base sequence quality and passed the adapter-content check. |
| **Reference genome** | The original authors aligned the human RNA-seq reads to the *Homo sapiens* GRCh38 reference genome. | The *Homo sapiens* GRCh38 primary assembly was used as the reference genome. |
| **Annotation** | The original paper referred to GRCh38.78 but did not clearly provide the exact annotation file used for the human analysis. | The Ensembl Release 78 annotation file `Homo_sapiens.GRCh38.78.gtf.gz` was used. |
| **RNA-seq aligner** | The original authors aligned the human RNA-seq reads using TopHat version 2.1.1. | TopHat version 2.1.1 in Galaxy was used for read alignment. |
| **Gene counting** | The original authors used HTSeq version 0.4.7 to generate gene-level read counts. | featureCounts was used to generate gene-level read counts from the mapped RNA-seq reads. |
| **Differential expression** | The original authors used DESeq version 1.5.24 to identify genes with altered expression between infected and control samples. | DESeq2 in Galaxy was used to compare the three infected samples with the three control samples. |
| **Significance threshold** | The original study considered genes significant using a p-value of 0.05 or lower together with fold-change criteria for increased or decreased expression. | Genes with an adjusted p-value lower than 0.05 were considered significantly differentially expressed. |
| **Main genes or pathways identified** | The original study highlighted genes such as GSTM1, CRIP1, and CCL25 and reported changes in pathways associated with immune defense, B-cell receptor signaling, and host mucosal responses. | A total of 32 significantly differentially expressed genes were identified, including 10 upregulated and 22 downregulated genes. Selected genes included C1QC, AADAC, MUC3A, ULK1, and MUC20, which were associated with immune response, metabolism, autophagy, and mucosal barrier function. |

**Main Quality Control Results**

Quality control was performed on the six selected RNA-seq samples using FastQC in Galaxy to assess the overall quality of the sequencing data. The individual FastQC reports were then summarized using the MultiQC tool in Galaxy for easier comparison among the samples. The results were examined based on the number of reads, general sequence quality, adapter contamination, overrepresented sequences, and other possible quality problems. The summarized quality control results are presented in below.

Table 2. RNA-Seq read quality, adapter contamination, sequence composition, and duplication profiles of uninfected and infected tissue biopsies.
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

Table 3. Mapping Statistics of the Selected RNA-Seq Samples Using TopHat
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

Table 4. Summary of Differential Gene Expression Analysis.
| **DESeq2 Result** | **Result** | **Interpretation** |
|---|---:|---|
| Genes tested | 8,848 | Total genes included in the DESeq2 analysis |
| Significantly differentially expressed genes | 32 | Genes with adjusted *p*-value < 0.05 |
| Positive log2 fold change | 10 | Significantly higher expression in the infected group |
| Negative log2 fold change | 22 | Significantly lower expression in the infected group |
| Adjusted *p*-value (FDR) threshold | < 0.05 | Threshold used to determine statistical significance |

The result based on the DESeq2 results, 32 genes were found to be significantly different between the infected and normal groups. Ten genes were more active, while 22 were less active in the infected group. This shows that the infection had an effect on gene expression.

**Interpreted Genes** 

Table 5. Biological Interpretation of Selected Differentially Expressed Genes.
| **Gene ID** | **Gene Name** | **log2FC** | **Adjusted *p*-value** | **Regulation** | **Known / Predicted Function** | **Possible Connection to Infection** |
|---|---|---:|---:|---|---|---|
| ENSG00000159189 | **C1QC** | 1.2847 | 0.01194 | Upregulated | Component of C1q involved in activation of the classical complement pathway and immune defense against pathogens (Kishore & Reid, 2000). | Increased C1QC expression may be associated with the host immune response to *S. Typhi* infection, as the complement system participates in host defense against *Salmonella* and interacts directly with *S. Typhi* during infection (Guerra et al., 2025). |
| ENSG00000114771 | **AADAC** | 1.2308 | 0.01194 | Upregulated | Microsomal serine esterase involved in drug and lipid metabolism, including the hydrolysis of triglycerides and cholesterol esters (Yang et al., 2025). | AADAC may be involved in infection-associated changes in host lipid metabolism. In HCV-infected cells, reduced AADAC was associated with impaired triglyceride lipolysis, while AADAC knockdown also affected viral production, demonstrating that AADAC can function as a host factor during infection (Nourbakhsh et al., 2013). |
| ENSG00000169894 | **MUC3A** | -1.2790 | 0.02171 | Downregulated | Encodes a cell-surface-associated mucin that contributes to the protective and lubricating barrier of mucosal surfaces (NCBI, 2026). | Downregulation of MUC3A may reflect alterations in the intestinal mucosal barrier during infection, as intestinal mucins contribute to epithelial defense and protection against *Salmonella* infection (Han et al., 2024). |
| ENSG00000177169 | **ULK1** | -1.0416 | 0.03695 | Downregulated | Encodes a serine/threonine kinase that plays a key role in initiating and regulating autophagy, including autophagosome formation (NCBI, 2026). | Downregulation of ULK1 may indicate altered autophagy-related host defense during infection, as *Salmonella* can suppress autophagy through mTORC1-mediated inhibition of ULK1, which may promote bacterial survival (Torsilieri et al., 2024). |
| ENSG00000176945 | **MUC20** | -1.3557 | 0.01032 | Downregulated | Transmembrane mucin involved in maintaining epithelial barrier integrity and participating in cellular signaling and immune responses at epithelial surfaces (Montero et al., 2025). | Downregulation of MUC20 may indicate changes in the intestinal mucosal barrier during infection, as an enhanced mucosal barrier has been shown to reduce the invasion of *Salmonella enterica* in human small intestinal epithelial cells (Yamazaki et al., 2024). |

The DESeq2 results identified five significant genes associated with S. Typhi infection, including C1QC and AADAC, which were upregulated, and MUC3A, ULK1, and MUC20, which were downregulated. These genes are mainly involved in immune defense, lipid metabolism, mucosal barrier integrity, and autophagy. Overall, the changes suggest that S. Typhi infection may alter host immune responses, intestinal barrier function, and cellular defense mechanisms. 

**Comparison with the Published Results**

The results of the Galaxy re-analysis were compared with the findings of the original study. The comparison focused on the biological response, identified genes, analysis tools, samples used, and possible reasons for differences between the two results.

**1. Did your group recover the same general biological response described by the authors?**

Yes. The original paper reported that S. Typhi colonization triggers extensive transcriptional changes related to immune defense and mucosal barrier function during infection. The re-analysis similarly identified differential expression in genes tied to immune activation — the C1QC, and mucosal barrier integrity —MUC3A and MUC20, which these aspects support the original paper discussed by the authors. 

**2. Were any of the genes highlighted in the paper also identified in your analysis?**

The original paper specifically highlighted genes such as GSTM1, CRIP1, CCL25, MUC5B, and EPPK1. These are not among the five genes selected for interpretation in our re-analysis. However, our results contained genes with related biological functions, particularly immune-response and mucosal-barrier genes such as C1QC, MUC3A, and MUC20. A complete gene-by-gene comparison would require matching all 32 significant genes from our analysis with the full gene lists reported by the authors.

**3. Which results were similar?**

Both directions of the biological narrative of the study were similar in terms of the theme, infection alters immune and mucosal-barrier gene expression. Both analyses used the same reference genome assembly GRCh28 and comparable pipeline steps — the QC, alignment, to differential expression. 

**4. Which results were different?**

The study only uses 6 of the original samples— 3 control and 3 infected, instead of the full data set which differs from the original study with a full data set with 4 control, 5 infected, plus bacterial controls. The number of significantly differentially expressed genes is very likely much smaller compared to the original study since they had a larger sample size and possible different statistical thresholds.

**5. Did you use exactly the same software as the authors?**

Partially. The study used TopHat for alignment, HTSeqq for read counting and DESeq2 instead of DESeq from the original study. DESeq was used since it is a newer, updated version of the same statistical framework but uses different shrinkage estimation that alters the results, 

**6. Did you use the same reference genome and annotation versions?**

Yes. The analyses used the same general human reference, GRCh38. The original paper reports alignment to the Homo sapiens reference genome GRCh38.78, while our re-analysis used the GRCh38 primary assembly together with the Ensembl Release 78 GTF annotation. However, the original paper does not explicitly provide the exact GTF annotation filename used, so we cannot confirm that the annotation files were completely identical.

**7. Did you analyze all samples or only a subset?**

Only a subset was analyzed in the study which differs from the original study that has 4 controls, 5 infected and a bacterial control sample. 

**8. Could differences in software versions, parameters, sample number, or reference files explain differences in the results?**

Yes. Using DESeq instead of DESeq, a smaller sample size reduces statistical power to detect true differential expressed genes, and potentially different parameters can all lead to differences in the number and identity of significant raw reads and reference genome. 

**9. What did this exercise teach you about reproducibility in molecular biology?**

This exercise showed that reproducibility in molecular biology is rarely a simple matter of running the same data through the same pipeline and expecting identical results. Even when researchers use the same reference genome, the same general workflow, and start from the same publicly available raw data, small differences— such as software versions, sample size, or default parameter settings, can lead to different specific outcomes. This suggests that true reproducibility depends heavily on detailed and transparent documentation of every methodological choice, since even minor insignia can influence the final results. At the same time, the fact that the broader biological patterns can still be recovered despite these differences suggests that reproducibility should often be evaluated at the level of overall conclusions rather than requiring an exact match of every individual result, and that some degree of variability between independent analysis is normal and expected part of the scientific research rather than necessary a sign of error.

**Limitations**

Although the major steps of the RNA-seq analysis were successfully reproduced in Galaxy, some parts of the original published workflow could not be followed exactly. Differences in software, sample selection, and Galaxy functionality required the use of reasonable alternatives. These changes and their possible effects on the results are summarized below. 

Table 6. Modifications and Limitations in Reproducing the Original RNA-Seq Workflow.
| **Step** | **Difference or Limitation** | **Alternative Used** | **Possible Effect on Results** |
|---|---|---|---|
| **Sample selection** | The complete set of human biopsy samples was not analyzed. | Three control and three infected samples were selected for the re-analysis. | Using fewer biological replicates may reduce statistical power and may change the number of significant genes detected. |
| **Gene counting** | The original study used HTSeq for gene-level counting. | featureCounts was used as required in the Galaxy re-analysis. | Differences in how reads are assigned to genes may result in slightly different gene counts. |
| **Differential expression** | The original study used DESeq. | DESeq2 was used in Galaxy. | Differences in normalization and statistical methods may affect log2 fold changes, adjusted p-values, and the genes identified as significant. |
| **Workflow extraction** | Galaxy was unable to automatically extract the workflow from the completed history because the server repeatedly returned a history-access error. | The workflow was manually reconstructed in the Galaxy Workflow Editor and exported as a `.ga` file. | This did not change the completed analysis results, but the workflow had to be recreated from the recorded analysis steps and parameters. |
| **Published pipeline reproduction** | Some software versions and exact parameters from the original study were different from those available or required in the current Galaxy workflow. | The closest available Galaxy tools and documented settings were used. | Software and parameter differences may contribute to differences between the published and re-analysis results. |

Despite these differences, the major RNA-seq analysis steps were successfully completed, including quality control, read mapping, gene-level counting, and differential expression analysis. The differences were documented to provide a transparent explanation of why the re-analysis may not produce exactly the same numerical results as the original study.

**Group Conclusion**

This activity allowed the students how to understand how RNA-seq can be used to study changes in gene expression during salmonella typhi infection. Through Galaxy, the students were able to perform quality control, read mapping, gene counting, and differential expression analysis. It was found that there's 32 significantly differentially expressed genes, with 10 upregulated and 22 downregulated in the infected samples. Although the results were not exactly the same as the original study because the students used fewer samples and some different tools, we still observed similar changes related to immune response and intestinal mucosal defense. This activity also enlightened the members of the group that small differences in the analysis process can affect the results, which is why proper documentation and reproducibility are important in  this subject.
