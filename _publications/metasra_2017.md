---
title: "MetaSRA: normalized human sample-specific metadata for the Sequence Read Archive"
collection: publications
permalink: /publication/metasra_2017
excerpt: 'The NCBI’s Sequence Read Archive (SRA) promises great biological insight if one could analyze the data in the aggregate; 
however, the data remain largely underutilized, in part, due to the poor structure of the metadata associated with each sample. We present MetaSRA, a database of normalized SRA human sample-specific metadata following a schema inspired by the 
metadata organization of the ENCODE project. The MetaSRA is available at metasra.biostat.wisc.edu <metasra.biostat.wisc.edu> via both a searchable web interface and bulk downloads.'
date: 2017-09-15
venue: 'Bioinformatics'
paperurl: 'https://academic.oup.com/bioinformatics/article/3848915/MetaSRA-normalized-human-sample-specific-metadata'
citation: #'Your Name, You. (2009). &quot;Paper Title Number 1.&quot; <i>Journal 1</i>. 1(1).'
---

**Motivation**

The NCBI’s Sequence Read Archive (SRA) promises great biological insight if one could analyze the data in the aggregate; however, the data remain largely underutilized, in part, due to the poor structure of the metadata associated with each sample. The rules governing submissions to the SRA do not dictate a standardized set of terms that should be used to describe the biological samples from which the sequencing data are derived. As a result, the metadata include many synonyms, spelling variants and references to outside sources of information. Furthermore, manual annotation of the data remains intractable due to the large number of samples in the archive. For these reasons, it has been difficult to perform large-scale analyses that study the relationships between biomolecular processes and phenotype across diverse diseases, tissues and cell types present in the SRA.

**Results**

We present MetaSRA, a database of normalized SRA human sample-specific metadata following a schema inspired by the metadata organization of the ENCODE project. This schema involves mapping samples to terms in biomedical ontologies, labeling each sample with a sample-type category, and extracting real-valued properties. We automated these tasks via a novel computational pipeline.

**Availability and implementation**

The MetaSRA is available at [http://metasra.biostat.wisc.edu](metasra.biostat.wisc.edu) via both a searchable web interface and bulk downloads. Software implementing our computational pipeline is available at [http://github.com/deweylab/metasra-pipeline](http://github.com/deweylab/metasra-pipeline).

The paper can be found at [here](https://academic.oup.com/bioinformatics/article/3848915/MetaSRA-normalized-human-sample-specific-metadata)
