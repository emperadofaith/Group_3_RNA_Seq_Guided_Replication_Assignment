# Results

## 1. RNA-Seq Quality Control

Quality control was performed on six selected RNA-seq samples using FastQC and MultiQC in Galaxy. The samples produced approximately 20.1–24.4 million reads and passed the overall sequence-quality and adapter-contamination assessments. However, warnings were observed for overrepresented sequences, per-base sequence composition, GC-content distribution, and sequence duplication in some samples. Overall, the datasets were considered suitable for downstream RNA-seq analysis.

### Quality Control Summary

| Sample | Accession | Condition | Number of Reads | General Sequence Quality | Adapter Contamination |
|---|---|---|---:|---|---|
| Control_rep1 | SRR7029701 | Uninfected | 20.8 M | Pass | Pass |
| Control_rep2 | SRR7029702 | Uninfected | 23.5 M | Pass | Pass |
| Control_rep3 | SRR7029703 | Uninfected | 22.6 M | Pass | Pass |
| Infected_rep1 | SRR7029705 | Infected | 23.8 M | Pass | Pass |
| Infected_rep2 | SRR7029706 | Infected | 21.1 M | Pass | Pass |
| Infected_rep3 | SRR7029707 | Infected | 24.4 M | Pass | Pass |

---

## 2. Read Mapping

The six RNA-seq samples were mapped to the *Homo sapiens* GRCh38 reference genome using TopHat in Galaxy. The percentage of mapped reads ranged from 89.7% to 96.7%, while uniquely mapped reads ranged from 56.5% to 77.5%. SRR7029707 showed the lowest mapping percentage at 89.7% and was identified as the sample with unusually low mapping compared with the other samples.

### Mapping Statistics

| Sample | Total Reads | Mapped Reads (%) | Uniquely Mapped (%) | Unusually Low Mapping |
|---|---:|---:|---:|---|
| SRR7029701 | 20,768,901 | 96.1% | 77.5% | No |
| SRR7029702 | 23,483,399 | 96.7% | 77.5% | No |
| SRR7029703 | 22,642,554 | 95.4% | 73.1% | No |
| SRR7029705 | 23,750,360 | 93.1% | 67.6% | No |
| SRR7029706 | 20,081,963 | 93.9% | 56.5% | No |
| SRR7029707 | 24,357,703 | 89.7% | 61.3% | Yes |

---

## 3. Gene-Level Read Counting

Gene-level read counting was performed using featureCounts with the *Homo sapiens* GRCh38.78 GTF annotation. The resulting gene-count dataset contained approximately 64,254 gene entries from the six RNA-seq samples.

The complete gene-level count table was generated from the featureCounts outputs and was used as the input for differential gene expression analysis.

---

## 4. Differential Gene Expression Analysis

Differential gene expression analysis was performed using DESeq2 in Galaxy. The three infected samples were compared with the three uninfected control samples, with the control group used as the reference.

A total of **8,848 genes** with valid adjusted p-values were included in the analysis. Using an adjusted p-value threshold of **< 0.05**, **32 genes** were identified as significantly differentially expressed.

- **10 genes** were upregulated in the infected group.
- **22 genes** were downregulated in the infected group.

### Differential Expression Summary

| Result | Number |
|---|---:|
| Genes tested | 8,848 |
| Significantly differentially expressed genes | 32 |
| Upregulated genes | 10 |
| Downregulated genes | 22 |
| Adjusted p-value threshold | < 0.05 |

---

## 5. Selected Differentially Expressed Genes

Five significantly differentially expressed genes were selected for biological interpretation based on their log2 fold change and adjusted p-values.

| Gene | log2FC | Adjusted p-value | Regulation | Main Function |
|---|---:|---:|---|---|
| C1QC | 1.2847 | 0.01194 | Upregulated | Complement and immune defense |
| AADAC | 1.2308 | 0.01194 | Upregulated | Lipid and drug metabolism |
| MUC3A | -1.2790 | 0.02171 | Downregulated | Intestinal mucosal barrier |
| ULK1 | -1.0416 | 0.03695 | Downregulated | Autophagy |
| MUC20 | -1.3557 | 0.01032 | Downregulated | Epithelial barrier and signaling |

---

## 6. Overall Biological Result

Overall, the RNA-seq re-analysis showed that *Salmonella Typhi* infection was associated with changes in host gene expression. The identified differentially expressed genes were mainly associated with immune defense, lipid metabolism, mucosal barrier integrity, and autophagy. C1QC and AADAC were upregulated, while MUC3A, ULK1, and MUC20 were downregulated in the infected samples.

---

## 7. Comparison with the Original Study

The Galaxy re-analysis recovered the same general biological response described in the original study, particularly changes related to host immune defense and mucosal barrier function. However, the exact genes and number of significant genes differed from the original study because the re-analysis used a smaller subset of samples and different tools for gene counting and differential expression analysis.
