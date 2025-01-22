# Opa1-scRNAseq
scRNAseq analysis included in Willett et al. 2024


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
