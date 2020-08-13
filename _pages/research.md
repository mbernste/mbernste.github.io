---
title: "Research"
permalink: /research/
author_profile: true
---

## Hierarchical cell type classification against the Cell Ontology

Cell type annotation is a fundamental task in the analysis of single-cell RNA-sequencing data. We present [CellO](https://github.com/deweylab/CellO), a machine learning-based tool for annotating human RNA-seq data with the [Cell Ontology](http://www.obofoundry.org/ontology/cl.html). CellO enables accurate and standardized cell type classification by considering the rich hierarchical structure of known cell types. Furthemore, CellO comes pre-trained on a novel, comprehensive dataset of human, healthy, untreated primary samples in the [Sequence Read Archive](https://www.ncbi.nlm.nih.gov/sra) (SRA), which to the best of our knowledge, is the most diverse curated collection of primary cell data to date. 

* Bernstein, M.N., Ma, J., Gleicher, M., and Dewey, C.N. (2020). [CellO: Comprehensive and hierarchical cell type classification of human cells with the Cell Ontology](https://www.biorxiv.org/content/10.1101/634097). _bioRxiv_.

[logo]: https://mbernste.github.io/images/MetaSRA_overview.png "Logo Title Text 2"
![My helpful screenshot]({{ "  https://mbernste.github.io/images/cell_type_classification.png" |   https://mbernste.github.io/images/cell_type_classification.png }})

## Standardizing metadata for large, public genomics databases

The NCBI’s [Sequence Read Archive](https://www.ncbi.nlm.nih.gov/sra) (SRA) promises great biological insight if one could analyze the data in the aggregate; 
however, the data remain largely underutilized, in part, due to the [poor structure](https://www.nature.com/articles/sdata201921) of the metadata associated with each sample. We developed the [MetaSRA](http://metasra.biostat.wisc.edu), a novel computational pipeline and associated database for standardizing the metadata associated with samples in the SRA by mapping each sample to biomedical [ontologies](https://en.wikipedia.org/wiki/Ontology_(information_science)).  See [my talk](https://www.youtube.com/watch?v=pVHMq9SdUtc) describing the MetaSRA from [ISMB 2018](https://www.iscb.org/ismb2018).

* Bernstein, M.N., Doan, A., and Dewey, C.N. (2017). [MetaSRA: Normalized human sample-specific metadata for the Sequence Read Archive](https://doi.org/10.1093/bioinformatics/btx334). _Bioinformatics_, 33(18), 2914–2923. 

[logo]: https://mbernste.github.io/images/MetaSRA_overview.png "Logo Title Text 2"
![My helpful screenshot]({{ " https://mbernste.github.io/images/MetaSRA_web.png" |  https://mbernste.github.io/images/MetaSRA_web.png }})

## Developing tools for querying public datasets

We've built [Jupyter-notebook based tools](https://github.com/mbernste/hypothesis-driven-SRA-queries) atop the [MetaSRA](http://metasra.biostat.wisc.edu) for constructing structured datasets from the [SRA](https://www.ncbi.nlm.nih.gov/sra). The [Case-Control Finder](https://colab.research.google.com/drive/1HX8V5yFRCh-AdkC-XHnfo6thg6VHwplC?usp=sharing) finds matches samples of a given condition/disease from the SRA to control samples. The [Series Finder](https://colab.research.google.com/drive/1BNmBokHi41ODCWeS3G_WY8OfZ54RVXf3?usp=sharing) finds ordered sets of samples where samples are ordered by a continuous property such as age.

* Bernstein, M.N., et al. (2020). [Jupyter notebook-based tools for building structured datasets from the Sequence Read Archive](https://f1000research.com/articles/9-376). _F1000 Research_, 9:376.

![My helpful screenshot]({{ " https://mbernste.github.io/images/CaseControl.png" |  https://mbernste.github.io/images/CaseControl.png }})

