# 🧬 Cancer Evolution Analysis: Breast Cancer Subclones

## 📊 Project Overview
Comprehensive phylogenetic and evolutionary analysis of breast cancer single-cell RNA-seq data to identify cancer subclones and map their evolutionary relationships.

---

## 📁 Project Structure
```
cancer-evolution/
│
├── LICENSE
├── README.md
├── requirements.txt
├── environment.yml
│
├── data/
│   └── raw/
│       └── breast_cancer.h5              # Input: 10X scRNA-seq data (4,992 cells)
│
├── notebooks/
│   └── Cancer_evolution_analysis.ipynb   # Complete analysis pipeline
│
└── results/
    ├── figures_tables/                    # Combined figures and data tables
    │   ├── cancer_cells_identification.png
    │   ├── cluster_markers.csv
    │   ├── comprehensive_evolutionary_map.png
    │   ├── driver_genes_subclone_0.csv
    │   ├── driver_genes_subclone_1.csv
    │   ├── driver_genes_subclone_2.csv
    │   ├── driver_genes_subclone_3.csv
    │   ├── driver_genes_subclone_4.csv
    │   ├── driver_genes_subclone_5.csv
    │   ├── driver_genes_subclone_6.csv
    │   ├── evolutionary_map_with_connections.png
    │   ├── evolutionary_rate_analysis.png
    │   ├── final_subclones_selected.png
    │   ├── genetic_distance_matrix.png
    │   ├── pathway_heatmap_comprehensive.png
    │   ├── phylogenetic_tree.png
    │   ├── spatial_distribution_subclones.png
    │   ├── subclone_density_maps.png
    │   ├── subclone_driver_genes_heatmap.png
    │   ├── subclone_markers_dotplot.png
    │   └── ... (all other figures and CSVs)
    │
    └── COMPREHENSIVE_PROJECT_SUMMARY.txt  # Full analysis report
```

---

## 🚀 Quick Start

### Installation

1. **Clone or download the repository**

2. **Install dependencies:**
```bash
   # Option 1: Using conda (recommended)
   conda env create -f environment.yml
   conda activate cancer-sc

   # Option 2: Using pip
   pip install -r requirements.txt
```

3. **Launch Jupyter:**
```bash
   cd notebooks
   jupyter notebook Cancer_evolution_analysis.ipynb
```

4. **Run the analysis:**
   - Execute all cells sequentially (Cell → Run All)
   - Or run sections individually

---

## 📊 Analysis Workflow

The notebook is organized into 6 main analysis sections:

### 1️⃣ **Data Loading & Quality Control**
- Load 10X Genomics h5 file
- Calculate QC metrics (genes per cell, UMI counts, mitochondrial %)
- Filter low-quality cells and genes
- Normalize and log-transform data

**Input:** `data/raw/breast_cancer.h5` (4,992 cells)  
**Output:** 3,821 high-quality cells

---

### 2️⃣ **Clustering & Cell Type Annotation**
- Identify highly variable genes
- Dimensionality reduction (PCA, UMAP)
- Leiden clustering
- Differential expression analysis
- Annotate cell types based on marker genes

**Output:** 9 cell clusters identified  
**Cancer cells:** Clusters 1, 2, 4 (epithelial populations)

---

### 3️⃣ **Cancer Subclone Identification**
- Isolate 1,508 cancer cells
- Re-cluster at high resolution (resolution = 0.8)
- Identify 7 distinct cancer subclones

**Output:** 7 subclones (SC0-SC6)  
**Key finding:** Both luminal and basal lineages show heterogeneity

---

### 4️⃣ **Phylogenetic Tree Construction**
- Calculate mean expression profiles per subclone
- Compute pairwise Euclidean distances
- Build UPGMA phylogenetic tree
- Visualize evolutionary relationships

**Output:** Phylogenetic tree showing branching patterns  
**Key finding:** SC5 & SC6 are sister clones (closest relatives)

---

### 5️⃣ **Functional Characterization**
- **Driver genes:** Identify subclone-specific markers
- **Pathway analysis:** 8 cancer pathways (Cell Cycle, EMT, Metastasis, etc.)
- **Trajectory analysis:** Infer evolutionary ordering (pseudotime)
- **Spatial distribution:** Map subclone locations in UMAP space

**Output:** Comprehensive functional profiles  
**Key finding:** SC6 shows most aggressive phenotype

---

### 6️⃣ **Evolutionary Rate Analysis**
- Calculate differentially expressed genes between all subclone pairs
- Quantify transcriptional divergence
- Correlate genetic distance with evolutionary divergence

**Output:** Evolutionary rate matrix  
**Key finding:** Strong correlation (r=0.931) between distance and divergence

---

## 📈 Key Results

### 🔬 Subclone Characteristics

| Subclone | Cells | % | Origin | Key Features |
|----------|-------|---|--------|--------------|
| **SC0** | 336 | 22.3% | Luminal | High proliferation (CCND1, CXCL14) |
| **SC1** | 283 | 18.8% | Luminal | Metabolic (COX6C, CSTA) |
| **SC2** | 269 | 17.8% | Basal | Growth factors (IGFBP5, CRISP3) |
| **SC3** | 251 | 16.6% | Luminal | **Immune signature** (HLA genes, LYZ) |
| **SC4** | 152 | 10.1% | Basal | ECM remodeling (COL1A1, CEACAM6) |
| **SC5** | 113 | 7.5% | Luminal | Proteases (CTSD, TGM2) |
| **SC6** | 104 | 6.9% | Basal | **Most aggressive** (FN1, SPARC, high EMT) |

---

### 🌳 Phylogenetic Insights

**Closest Pairs (Recent Divergence):**
- SC5 ↔ SC6: 99 DE genes (sister clones)
- SC1 ↔ SC3: 314 DE genes
- SC0 ↔ SC5: 416 DE genes

**Most Divergent Pairs:**
- SC1 ↔ SC6: 3,983 DE genes
- SC1 ↔ SC2: 3,577 DE genes
- SC1 ↔ SC5: 3,133 DE genes

**Correlation:**
- Genetic distance vs transcriptional divergence: **r = 0.931** (p < 0.001)

---

### 🎯 Functional Highlights

**Most Proliferative:**
- SC6: Cell cycle score = 0.537
- SC0: Cell cycle score = 0.409

**Most Aggressive (EMT/Metastasis):**
- SC6: EMT = 0.255, Metastasis = 0.474, ECM = 1.196
- SC4: EMT = 0.137, Metastasis = 0.158, ECM = 0.656

**Unique Immune Response:**
- SC3: Only subclone with positive immune signature (0.512)

---

## 📂 Output Files

All results are saved in `results/figures_tables/`:

### 🖼️ Key Figures

1. **cancer_cells_identification.png** - Separation of cancer vs non-cancer cells
2. **final_subclones_selected.png** - 7 identified subclones on UMAP
3. **phylogenetic_tree.png** - UPGMA evolutionary tree
4. **genetic_distance_matrix.png** - Pairwise distance heatmap
5. **subclone_driver_genes_heatmap.png** - Top 10 markers per subclone
6. **pathway_heatmap_comprehensive.png** - 8 cancer pathways across subclones
7. **spatial_distribution_subclones.png** - Individual subclone locations
8. **evolutionary_rate_analysis.png** - 6-panel divergence analysis
9. **comprehensive_evolutionary_map.png** - Multi-panel summary
10. **FINAL_COMPREHENSIVE_SUMMARY.png** - Complete analysis overview

### 📋 Data Tables

- **cluster_markers.csv** - Top 10 markers for initial 9 clusters
- **driver_genes_subclone_0.csv** through **driver_genes_subclone_6.csv** - Complete marker gene lists for each subclone (columns: gene name, scores, log fold changes, adjusted p-values)
- **genes_for_enrichment_SC*.txt** - Gene lists for external pathway tools (Enrichr, g:Profiler)
- **pairwise_de_gene_counts.csv** - Number of DE genes between all subclone pairs

### 📄 Reports

- **COMPREHENSIVE_PROJECT_SUMMARY.txt** - Full analysis report including:
  - Dataset statistics
  - Subclone characteristics
  - Phylogenetic relationships
  - Pathway analysis
  - Spatial distribution
  - Evolutionary rates
  - Biological interpretation

---

## 🔧 Requirements

### Python Version
- Python 3.8 or higher

### Required Packages
```
scanpy >= 1.9.0
pandas >= 2.0.0
numpy >= 1.23.0
matplotlib >= 3.5.0
seaborn >= 0.12.0
scipy >= 1.9.0
scikit-learn >= 1.0.0
jupyterlab >= 3.0.0
```

### Installation Commands

**Using conda:**
```bash
conda env create -f environment.yml
conda activate cancer-sc
```

**Using pip:**
```bash
pip install -r requirements.txt
```

---

## ⏱️ Runtime

Complete analysis takes approximately **30-40 minutes** on a standard laptop:
- Data loading & QC: ~2 min
- Clustering: ~3 min
- Subclone identification: ~5 min
- Phylogenetic analysis: ~2 min
- Functional analysis: ~10 min
- Evolutionary rates: ~15 min

---

## 🧪 Methodology

### Clustering Parameters
- **Algorithm**: Leiden clustering
- **Resolution**: 0.5 (initial), 0.8 (subclone detection)
- **Neighbors**: 15
- **Principal Components**: 30

### Phylogenetic Analysis
- **Method**: UPGMA (Unweighted Pair Group Method with Arithmetic Mean)
- **Distance**: Euclidean distance on mean gene expression profiles
- **Linkage**: Average linkage hierarchical clustering

### Differential Expression
- **Test**: Wilcoxon rank-sum test (non-parametric)
- **Significance**: Adjusted p-value < 0.05
- **Fold Change**: |log2FC| > 0.5 (for evolutionary rate analysis)
- **Correction**: Benjamini-Hochberg FDR

### Pathway Analysis
- **Gene Sets**: 8 curated cancer-related pathways
  - Cell Cycle, Apoptosis, EMT, Metastasis
  - Stemness, Proliferation, ECM Remodeling, Immune Response
- **Scoring**: Mean expression of pathway genes per subclone

---

## 🔍 Biological Interpretation

### Evolutionary Model

The analysis reveals a **complex branching evolutionary history**:

1. **Two Major Lineages:**
   - Luminal-derived (SC0, 1, 3, 5, 6)
   - Basal-derived (SC2, 4)

2. **Ongoing Evolution:**
   - Intra-lineage heterogeneity demonstrates continued diversification
   - Strong correlation (r=0.931) indicates consistent evolutionary processes

3. **Functional Diversification:**
   - **Aggressive phenotype**: SC6 (high EMT, metastasis, ECM remodeling)
   - **Immunogenic phenotype**: SC3 (unique immune signature)
   - **Proliferative phenotype**: SC0, SC5 (high cell cycle activity)

4. **Sister Clones:**
   - SC5 and SC6 share recent common ancestor (only 99 DE genes)
   - SC1 shows highest divergence (early-branching lineage)

### Clinical Implications

1. **Therapeutic Targeting**: SC6's aggressive profile makes it priority target
2. **Immunotherapy Potential**: SC3's immune signature may respond to immunotherapy
3. **Multi-drug Necessity**: Subclone diversity requires combination therapies
4. **Biomarker Development**: Subclone-specific markers for prognosis

---

## 📝 Citation

If you use this code or methodology:
```bibtex
@software{cancer_evolution_2026,
  author = {Manju Selvakumaran},
  title = {Cancer Evolution Analysis: Breast Cancer Subclones},
  year = {2026},
  url = {https://github.com/Manju-Selvakumaran/cancer-evolution}
}
```

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👥 Authors & Acknowledgments

**Author**: Manju Selvakumaran   
**Contact**: manjuselvakumaran@gmail.com

**Acknowledgments**:
- Scanpy development team
- 10X Genomics for data generation
- Anthropic Claude for analysis assistance

---

**Last Updated**: January 2026
