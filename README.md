# Opa1-scRNAseq
scRNAseq analysis included in Willett et al. 2025 (in review at Cell Reports)


First project I'm putting into Github so things aren't as efficient or streamlined as I would like them to be. Will keep working on that.

Experimental details:
WT and Opa1-/- OT1 CD8 T cells
Two groups: naive and activated cells isolated from mice five days after LM.Ova.ActA challenge. All groups are splenocytes.

General process:
1) Read in data, add relevant metadata, merge into single seurat object
2) Initial data exploration
   - total reads per cell
   - unique genes per cell
   - mito pct
   - library complexity
3) Cell-level filtering
   - >200 unique genes
   - >1000 reads per cell
   - mito pct < 20%
   - complexity > 80%
4) Gene-level filtering
   - remove genes with 0 reads across all cells
   - remove genes not expressed in >10 cells
5) Post-filtering data check (see #2)
6) Log normalize gene expression
7) Calculate cell cycle score and cell cycle phase
   - distribution of cells amongst phases
8) PCA,tSNE, UMAP
9) clustering with FindNeighbors() -> 9 clusters
10) ID clusters based on commonly expressed genes
    - IDed contaminating RBCs, fetal-derived CD8 T cells, Macrophages, Bcells
11) Identify, remove doublets
12) New seurat object with contaminents removed
13) Rerun PCA, tSNE, UMAP, recluster -> 4 clusters
    - Naive (WT + KO)
    - d5_dividing (WT + KO)
    - d5_g1 (WT + KO)
    - d5_opaq_unique (KO only, dividing cells)
14) Cleanup seurat object metadata
15) Analysis:
    6A) activated vs naive
    6B) WT vs OPA1-/-
    6C) Clustering, split by genotype
    6D) makeup of each cluster (WT vs KO)
    6E) Cell cycle phase, split by genotype
    6F) Cell counts per cluster, colored by cell cycle phase
    6G) GEPs identified by cNMF, split by genotype
    6H) makeup of each GEP (WT vs KO)
    6I-J) Cell counts per GEP, split by genotype

    S5A) expression patterns of Tcell-relevant genes by clusters
    S5C) module score for hallmark Myc1 and Myc2 genesets (combined)
    
    
    
