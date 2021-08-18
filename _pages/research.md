---
title: "Research"
permalink: /research/
author_profile: true
---

The size and complexity of publicly available genomics data is immense, and represents the result of billions of dollars of public research expenditure. This valuable repository of data offers an unprecedented opportunity to make new discoveries relevant to basic science, as well as human health and disease. Unfortunately, the wealth of information in these datasets has gone undiscovered as most investigators can’t use it due to its scale, diverse protocols and aims, highly variable metadata, and systemic batch effects between studies. 

The goal of my research is to turn these challenges into strengths – that is, to develop statistical and computational methods that leverage the scale and heterogeneity of publicly available data in order to bring the power of this data to the biomedical research community and, in so doing, maximize the new knowledge that can be obtained from this invaluable resource. 

## Hierarchical cell type classification with the Cell Ontology

Cell type annotation is a fundamental task in the analysis of single-cell RNA-sequencing data. We present [CellO](https://github.com/deweylab/CellO), a machine learning-based tool for annotating human RNA-seq data with the [Cell Ontology](http://www.obofoundry.org/ontology/cl.html). CellO enables accurate and standardized cell type classification by considering the rich hierarchical structure of known cell types. Furthemore, CellO comes pre-trained on a novel, comprehensive dataset of human, healthy, untreated primary samples in the [Sequence Read Archive](https://www.ncbi.nlm.nih.gov/sra) (SRA) which, to the best of our knowledge, is the most diverse curated collection of primary cell data to date. 

* Bernstein, M.N., Ma, J., Gleicher, M., and Dewey, C.N. (2021). [CellO: Comprehensive and hierarchical cell type classification of human cells with the Cell Ontology](https://doi.org/10.1016/j.isci.2020.101913). _iScience_. 24(1), 101913.
* Bernstein, M.N., Dewey, C.N. (2021). [Annotating cell types in human single-cell RNA-seq data with CellO](https://doi.org/10.1016/j.xpro.2021.100705). _STAR Protocols_, 2(3), 100705.

[logo]: https://mbernste.github.io/images/MetaSRA_overview.png "Logo Title Text 2"
![My helpful screenshot]({{ "  https://mbernste.github.io/images/cell_type_classification.png" |   https://mbernste.github.io/images/cell_type_classification.png }})

## Standardizing metadata for large, public genomics databases

The NCBI’s [Sequence Read Archive](https://www.ncbi.nlm.nih.gov/sra) (SRA) promises great biological insight if one could analyze the data in the aggregate; 
however, the data remain largely underutilized, in part, due to the [poor structure](https://www.nature.com/articles/sdata201921) of the metadata associated with each sample. We developed the [MetaSRA](http://metasra.biostat.wisc.edu), a novel computational pipeline and associated database for standardizing the metadata associated with samples in the SRA by mapping each sample to biomedical [ontologies](https://en.wikipedia.org/wiki/Ontology_(information_science)).  See [my talk](https://www.youtube.com/watch?v=pVHMq9SdUtc) describing the MetaSRA from [ISMB 2018](https://www.iscb.org/ismb2018).

* Bernstein, M.N., Doan, A., and Dewey, C.N. (2017). [MetaSRA: Normalized human sample-specific metadata for the Sequence Read Archive](https://doi.org/10.1093/bioinformatics/btx334). _Bioinformatics_. 33(18), 2914–2923. 
* Bernstein, M.N., et al. (2020). [Jupyter notebook-based tools for building structured datasets from the Sequence Read Archive](https://f1000research.com/articles/9-376). _F1000 Research_. 9(376).

[logo]: https://mbernste.github.io/images/MetaSRA_overview.png "Logo Title Text 2"
![My helpful screenshot]({{ " https://mbernste.github.io/images/MetaSRA_web.png" |  https://mbernste.github.io/images/MetaSRA_web.png }})

## Webtools for exploring public single-cell cancer data

Single-cell RNA-seq (scRNA-seq) enables the profiling of genome-wide gene expression at the single-cell level and in so doing facilitates insight into and information about cellular heterogeneity within a tissue. This is especially important in cancer, where tumor and tumor microenvironment heterogeneity directly impact development, maintenance, and progression of disease. We present CHARacterizing Tumor Subpopulations (CHARTS), a computational pipeline and web application for analyzing, characterizing, and integrating publicly available scRNA-seq cancer datasets. CHARTS is freely available at [charts.morgridge.org](https://charts.morgridge.org).

* Bernstein, M.N., Ni, Z., Collins, M., Burkard, M.E., Kendziorski, C., and Stewart, R. (2021). [CHARTS: A web application for characterizing and comparing tumor subpopulations in publicly available single-cell RNA-seq datasets](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-021-04021-x). _BMC Bioinformatics_. 22(83).

![My helpful screenshot]({{ " https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/CHARTS_schematic.png" |  https://raw.githubusercontent.com/mbernste/mbernste.github.io/master/images/CHARTS_schematic.png }})
