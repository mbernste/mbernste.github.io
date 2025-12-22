---
title: "Projects"
permalink: /projects/
author_profile: true
---

Here are some of the software products to come out of my research:

## Monkeybread

Monkeybread is a Python toolkit that provides broad functionality for
analyzing and visualizing cellular organization, cellular niches, and intercellular communication
via ligand-receptor interactions. Monkeybread provides functions for visualization methods and lightweight statistical methods for exploring
spatial transcriptomics data.

* GitHub: [https://github.com/immunitastx/monkeybread](https://github.com/immunitastx/monkeybread)  
* Documentation: [https://monkeybread.readthedocs.io/en/latest/](https://monkeybread.readthedocs.io/en/latest/)  
* Paper: [https://doi.org/10.1101/2023.09.14.557736](https://doi.org/10.1101/2023.09.14.557736)

## SpatialCorr

Recent advances in spatially resolved transcriptomics technologies enable both the measurement of genome-wide gene expression profiles and their mapping to spatial locations within a tissue. SpatialCorr is a method for identifying sets of genes with spatially varying correlation structure. Given a collection of gene sets pre-defined by a user, SpatialCorr tests for spatially induced differences in the correlation of each gene set within tissue regions, as well as between and among regions.

* GitHub: [https://github.com/mbernste/SpatialCorr](https://github.com/mbernste/SpatialCorr)
* Documentation: [https://spatialcorr.readthedocs.io/en/latest/index.html](https://spatialcorr.readthedocs.io/en/latest/index.html)
* Paper: [https://doi.org/10.1016/j.crmeth.2022.100369](https://doi.org/10.1016/j.crmeth.2022.100369)

[logo]: https://github.com/mbernste/SpatialCorr/raw/main/imgs/Overview_MainFigure_V3-01.png "Logo Title Text 2"
![My helpful screenshot]({{ "  https://github.com/mbernste/SpatialCorr/raw/main/imgs/Overview_MainFigure_V3-01.png" |   https://github.com/mbernste/SpatialCorr/raw/main/imgs/Overview_MainFigure_V3-01.png }})

## CellO

Cell type annotation is a fundamental task in the analysis of single-cell RNA-sequencing data. We present [CellO](https://github.com/deweylab/CellO), a machine learning-based tool for annotating human RNA-seq data with the [Cell Ontology](http://www.obofoundry.org/ontology/cl.html). CellO enables accurate and standardized cell type classification by considering the rich hierarchical structure of known cell types. Furthemore, CellO comes pre-trained on a novel, comprehensive dataset of human, healthy, untreated primary samples in the [Sequence Read Archive](https://www.ncbi.nlm.nih.gov/sra) (SRA) which, to the best of our knowledge, is the most diverse curated collection of primary cell data to date. 

* GitHub: [https://github.com/deweylab/CellO](https://github.com/deweylab/CellO)
* Paper: [https://doi.org/10.1016/j.isci.2020.101913](https://doi.org/10.1016/j.isci.2020.101913)
* Website: [https://uwgraphics.github.io/CellOViewer/](https://uwgraphics.github.io/CellOViewer/)
 
[logo]: https://mbernste.github.io/images/MetaSRA_overview.png "Logo Title Text 2"
![My helpful screenshot]({{ "  https://mbernste.github.io/images/cell_type_classification.png" |   https://mbernste.github.io/images/cell_type_classification.png }})

## MetaSRA

The NCBI’s [Sequence Read Archive](https://www.ncbi.nlm.nih.gov/sra) (SRA) promises great biological insight if one could analyze the data in the aggregate; 
however, the data remain largely underutilized, in part, due to the [poor structure](https://www.nature.com/articles/sdata201921) of the metadata associated with each sample. We developed the [MetaSRA](http://metasra.biostat.wisc.edu), a novel computational pipeline and associated database for standardizing the metadata associated with samples in the SRA by mapping each sample to biomedical [ontologies](https://en.wikipedia.org/wiki/Ontology_(information_science)).  See describing the MetaSRA from [ISMB 2018](https://www.iscb.org/ismb2018).

* Website: [http://metasra.biostat.wisc.edu](http://metasra.biostat.wisc.edu)
* GitHub:
  * [https://github.com/deweylab/MetaSRA-pipeline](https://github.com/deweylab/MetaSRA-pipeline)  
  * [https://github.com/deweylab/MetaSRA-website-frontend](https://github.com/deweylab/MetaSRA-website-frontend)
  * [https://github.com/deweylab/MetaSRA-API-backend](https://github.com/deweylab/MetaSRA-API-backend)
* Paper: [https://doi.org/10.1093/bioinformatics/btx334](https://doi.org/10.1093/bioinformatics/btx334)
* Talk: [At ISMB 2018](https://www.youtube.com/watch?v=pVHMq9SdUtc) 

## CHARTS

Characterize and compare tumor subpopulations across public single-cell RNA-seq data.

* Website: [https://charts.morgridge.org](https://charts.morgridge.org)
* GitHub: [https://github.com/stewart-lab/CHARTS](https://github.com/stewart-lab/CHARTS)
* Paper: [https://doi.org/10.1186/s12859-021-04021-x](https://doi.org/10.1186/s12859-021-04021-x)

## Series Finder & Case-Control Finder

Build structured datasets of RNA-seq data from the Sequence Read Archive.

* GitHub: [https://github.com/mbernste/hypothesis-driven-SRA-queries](https://github.com/mbernste/hypothesis-driven-SRA-queries)
* Paper: [https://doi.org/10.12688/f1000research.23180.2](https://doi.org/10.12688/f1000research.23180.2)

