# Alzheimer’s Disease Gene Expression Analysis

## 1. Introduction

### Goal of the Analysis
This analysis aims to identify specific genes and pathways that may play protective or harmful roles in neurodegeneration. In the context of Alzheimer’s Disease (AD), understanding these gene expression changes is crucial, as they can offer insights into underlying mechanisms that contribute to disease progression. By investigating genes that are either upregulated or downregulated in response to cellular stress or neurodegenerative factors, we can pinpoint pathways that may foster resilience or, conversely, pathways that could accelerate neurodegeneration.

### Background on Alzheimer’s Disease
Alzheimer’s Disease (AD) is a progressive neurodegenerative disorder primarily affecting memory and cognitive function, significantly diminishing quality of life. As a leading cause of dementia, understanding AD is essential for tackling a major public health challenge. Identifying effective biomarkers and therapeutic targets is crucial for early diagnosis, developing improved treatments, and potentially slowing disease progression.

### Role of Gene Expression in Understanding AD
Investigating gene expression changes offers a window into the molecular mechanisms underlying neurodegeneration. In AD, certain pathways may become dysregulated, potentially exacerbating neuronal damage or, alternatively, activating protective responses. By identifying upregulated and downregulated genes, we gain a deeper understanding of biological processes that could either contribute to or mitigate AD pathology. This analysis provides hands-on practice in using bioinformatics tools to analyze gene expression data with a focus on AD-related pathways, offering foundational insights into disease mechanisms and the roles of specific genes in neurodegeneration.

---

## 2. Dataset and Features

### Data Overview
The dataset used in this analysis is sourced from the [National Center for Biotechnology Information (NCBI) Gene Expression Omnibus (GEO)](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE252132), specifically Series GSE252132. This dataset provides RNA sequencing data to examine the effects of gene expression changes related to cellular aging and neurodegeneration, particularly focusing on Alzheimer’s Disease (AD). The dataset’s structure includes untreated and doxycycline (Dox)-induced conditions, allowing us to observe the expression levels of genes under baseline and stress conditions in neuron-like cells.

### Feature Description
The key features in this dataset include:
- **Gene Identifiers**: Each gene is identified uniquely, enabling us to map and analyze expression changes across different samples.
- **Expression Levels**: RNA sequencing provides quantitative data on gene expression, indicating which genes are upregulated or downregulated across different conditions.
- **Treatment Conditions**: Samples are categorized by untreated and Dox-induced conditions, enabling comparisons to identify differentially expressed genes in response to cellular stress.
- **Time Points**: Gene expression data is collected at two treatment durations, 2 days and 4 days, to observe changes over time.

These features are integral for identifying differentially expressed genes under the influence of Dox treatment, which provides insight into pathways that could be associated with neurodegeneration or resilience in AD.

### Dox Induction
The samples include conditions with Dox induction, a method used here to control the expression of the p16 gene. In this context, Dox-induced expression allows us to examine changes in gene expression associated with cellular aging processes relevant to neurodegeneration. This approach enables a controlled analysis of how specific genes respond under induced stress, aiding in the identification of pathways potentially linked to neuroprotective or neurodegenerative effects.

---

## 3. Analytical Approach

### Step 1: Define Control and Treated Groups
The analysis began by defining control and Dox-treated groups based on the column labels in our dataset. The samples without Dox induction were assigned to the control group, while those with Dox treatment were classified as the treated group. This division allowed us to compare the baseline (control) expression levels with those induced by Dox.

### Step 2: Differential Expression Analysis Using T-Test
To identify genes with significant expression changes, we used a t-test to compare gene expression between control and Dox-treated samples. By looping through each gene, we applied a two-sample t-test, comparing the mean expression levels in the control and treated groups. The t-test provides a t-statistic and a p-value for each gene:
- **t-statistic**: Represents the ratio of the difference between group means to the variability within groups. A larger t-statistic suggests a more pronounced difference in means.
- **p-value**: Indicates the probability of observing such a difference in gene expression by chance. A smaller p-value suggests that the observed difference is unlikely to have occurred randomly.

### Step 3: Multiple Testing Adjustment (FDR Correction)
Given the thousands of genes analyzed, performing multiple t-tests increases the likelihood of false positives. To address this, we applied a False Discovery Rate (FDR) correction to adjust the p-values, specifically using the Benjamini-Hochberg method.

### Step 4: Filtering Differentially Expressed Genes (DEGs)
We identified significantly differentially expressed genes (DEGs) by filtering genes with an adjusted p-value < 0.05, marking them as statistically significant. These DEGs included both upregulated and downregulated genes in response to Dox treatment.

### Step 5: Visualization with Volcano Plot
To visualize DEGs, we created a **volcano plot**:
- **X-axis (Log2 Fold Change)**: Represents the log2-transformed fold change in gene expression between Dox-treated and control samples.
  - Positive values indicate upregulated genes in Dox-treated samples.
  - Negative values indicate downregulated genes.
- **Y-axis (-log10 Adjusted P-value)**: Shows the statistical significance of each gene’s differential expression.
  - Higher values represent more statistically significant genes.
  - The blue dashed line represents the 0.05 adjusted p-value threshold, with points above the line indicating significant DEGs.
- **Red Points:** Each red dot represents a significantly differentially expressed gene. Their spread across the X-axis indicates variability in expression changes, with some genes exhibiting higher fold changes.

---

## 4. Results and Findings

The results of this analysis reveal several insights relevant to Alzheimer's Disease (AD), highlighting potential compensatory mechanisms and pathways involved in both protective and detrimental roles in neurodegeneration.

### Upregulated Genes and Pathways (GO Biological Processes and KEGG Pathways)

#### GO Biological Processes (Upregulated Genes)
The top enriched terms for upregulated genes suggest that these genes may contribute to compensatory mechanisms in neurodegeneration, focusing on maintaining synaptic connections, cellular communication, and metabolic responses. Key terms include:
- **Calcium-dependent Cell-cell Adhesion**:
  - Genes like PCDHB11 and PCDHB9 play significant roles in cell-cell adhesion through calcium signaling, which is critical for neural connectivity. In AD, strengthening or preserving neural connections could counteract synaptic loss, a hallmark of the disease.
- **Synapse Assembly and Organization**:
  - Terms like "synapse assembly" and "synapse organization" show high enrichment, suggesting that upregulated genes are involved in forming and maintaining neural connections. This process might act as a compensatory response to counteract synapse loss in AD, supporting cognitive function.
- **Steroid and Progesterone Metabolic Processes**:
  - Genes such as CUBN and AKR1C2 are involved in steroid and hormone metabolism. Steroids like estrogen have neuroprotective effects that reduce tau protein accumulation and beta-amyloid plaques—key features of AD pathology.
    
#### KEGG Pathways (Upregulated Genes)
The KEGG pathways enriched for upregulated genes reinforce the metabolic and neuroprotective adaptations that may help combat AD progression.

- **Vitamin Digestion and Absorption**:
  - CUBN (Cubilin) appears in this pathway, playing a role in nutrient absorption, particularly vitamin B12, which is essential for neural health. Vitamin B12 deficiency is linked to cognitive decline, so maintaining sufficient levels may help preserve cognitive function in AD.
- **Steroid Hormone Biosynthesis**:
  - AKR1C2 plays a role in steroid hormone biosynthesis, contributing to neuroprotective effects. Hormones such as estrogen have been linked to reduced neurodegeneration, potentially slowing down AD progression.
- **Chemical Carcinogenesis**:
  - AKR1C2 is also linked to chemical carcinogenesis pathways, suggesting involvement in detoxifying harmful chemicals. This could indicate a response to protect neurons from oxidative stress and toxins, factors that exacerbate AD.
  
### Downregulated Genes and Pathways (GO Biological Processes and KEGG Pathways)

#### GO Biological Processes (Downregulated Genes)
The top enriched terms for downregulated genes indicate that critical cellular maintenance functions, including DNA replication, metabolic regulation, and nucleotide recycling, may be impaired in AD.
- **Regulation of DNA-dependent DNA Replication Initiation**:
  - CDT1 is significantly downregulated, impacting DNA replication and possibly leading to impaired cell cycle control. Aberrant cell cycle re-entry is harmful to neurons, as it can trigger cell death, a detrimental process in AD.
- **Nucleobase Catabolic Processes**:
  - DPYSL5 is implicated in nucleobase catabolism, essential for recycling cellular components. A decrease in this process could disturb cellular nucleotide pools, leading to an accumulation of damage and contributing to neurodegeneration in AD.
- **Negative Regulation of Macromolecule Metabolic Processes**:
  - ANKRD13B and FGF19 are involved in regulating complex molecule metabolism. Downregulation here may imply reduced energy production and cellular stress responses, potentially reducing resilience to the AD disease process.
    
#### KEGG Pathways (Downregulated Genes)
The KEGG pathways enriched for downregulated genes further illustrate an impairment in processes that maintain cellular health and resilience.
- **Cancer-related Pathways (e.g., Breast Cancer, Melanoma)**:
  - While these pathways are primarily related to cell proliferation in cancer, their downregulation in neurons may suggest a protective measure, preventing harmful, aberrant cell growth. However, this also limits the cell's capacity to replace or repair damaged cells, an issue in AD.
- **Signaling Pathways (e.g., MAPK, Calcium Signaling)**:
  - Reduced MAPK and calcium signaling could reflect an attempt to control inflammatory responses, as neuroinflammation is associated with AD progression. However, these pathways also play roles in neuron survival, so their downregulation might make cells more vulnerable to damage.
- **Metabolic Pathways**:
  - Decreased involvement in metabolic pathways may suggest reduced cellular energy and growth signaling, which can impair neuronal function and resilience, potentially accelerating the neurodegenerative process.

---

## Conclusions
1.	**Compensatory Mechanisms in Upregulated Genes**:
- The upregulated pathways in cell adhesion, synapse assembly, and steroid metabolism suggest an attempt by the cells to counteract AD-related damage, enhancing structural support, and potentially providing neuroprotective responses. By supporting neural connectivity and maintaining essential functions, these pathways may delay or reduce the progression of AD symptoms.
  
2.	**Potentially Detrimental Processes in Downregulated Genes**:
- The downregulated pathways, particularly those associated with DNA replication, nucleotide metabolism, and metabolic signaling, suggest a reduced capacity for cell cycle maintenance and resilience. These impairments could lead to cumulative cellular damage and contribute to the degeneration seen in AD.
  
3.	**Disease Relevance**:
- Understanding the balance between compensatory and degenerative processes provides insights into AD's progression. Enhancing upregulated pathways or counteracting the downregulated ones could provide avenues for therapeutic exploration, offering strategies to preserve neuronal function and prevent or slow neurodegeneration.

  
In summary, this analysis provides foundational insights into gene expression changes and pathway involvement in neurodegeneration, especially in the context of Alzheimer’s Disease (AD). However, further experimental research is necessary to validate and expand upon these findings.



