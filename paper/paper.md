---
title: 'BioHackJP 2023 Report R1: Structural variation data model'
title_short: 'BioHackJP 2023 SV'
tags:
  - Structural variation
  - Genome Variation Ontology
  - human genome
authors:
  - name: Yosuke Kawai
    orcid: 0000-0003-0666-1224
    affiliation: 1
  - name: Toshiaki Katayama
    orcid: 0000-0003-2391-0384
    affiliation: 2
  - name: Mayumi Kamada
    orcid: 0000-0002-2555-7345
    affiliation: 3
  - name: Nobutaka Mitsuhashi
    orcid: 0000-0003-3300-7308
    affiliation: 2
  - name: Takahiro Fujisawa
    orcid: 0000-0001-8978-3344
    affiliation: 4
  - name: Yuichi Shiraishi
    orcid: 0000-0001-6144-5845
    affiliation: 5
  - name: Hideji Kawaji
    orcid: 0000-0002-0575-0308
    affiliation: 6
  - name: VISC members
    orcid: 0000-0000-0000-0000
    affiliation: 7
affiliations:
  - name: National Center for Global Health and Medicine, Japan
    index: 1
  - name: Database Center for Life Science, Research Organization of Information and Systems, Japan
    index: 2
  - name: Kyoto University, Japan
    index: 3
  - name: Bioinformation and DDBJ Center, National Institute of Genetics, Japan
    index: 4
  - name: National Cancer Center, Japan
    index: 5
  - name: Research Center for Genome & Medical Sciences, Tokyo Metropolitan Institute of Medical Science, Japan
    index: 6
date: 30 June 2023
cito-bibliography: paper.bib
event: BH23JP
biohackathon_name: "BioHackathon Japan 2023"
biohackathon_url:   "https://2023.biohackathon.org/"
biohackathon_location: "Kagawa, Japan, 2023"
group: R1
git_url: https://github.com/biohackathon-japan/bh23-visc
authors_short: Yosuke Kawai \emph{et al.}
---

# Background

With the proliferation of next-generation sequencers, information on variants obtained in research has surged both qualitatively and quantitatively. Short variants (SNVs, indels), which are relatively easy to detect and manage by genomic coordinates, are being catalogued in databases such as dbSNP. On the other hand, structural variants, which are large in size and diverse in types, have not been cataloged in databases sufficiently due to the lack of standardization of data structures. This project aims to answer this question by standardizing the format and ontology of structural variations for registration in databases. So far, the members of this project have held Variant Information Standardization Collegium ([VISC](https://github.com/dbcls/visc)) meetings and have been working on standardization efforts on a regular basis.

# Outcomes

## How to compare/distinguish between SVs
The precise interpretation of detected Structural Variations (SVs) hinges on distinguishing between known and novel SVs, a task dependent on genomic positions and sequence similarity. The intrinsic complexity and variety of SVs can make comparative analyses a painstaking endeavor. A thorough manual process is necessary to ascertain their correlation with previous SV data.
In this BioHackathon, to investigate the disparities among various SV detection tools, we compared SV call results for [a popular sequence data by Genome in a Bottle project](https://github.com/genome-in-a-bottle/giab_data_indexes) and evaluated them. 

- Compared tools
    - [GRIDSS](https://github.com/PapenfussLab/gridss)
    - [Delly](https://github.com/dellytools/delly)
    - [Manta](https://github.com/Illumina/manta)
- Sequence data
    - HG002 (Son of AshkenazimTrio)
        - Illumina WGS 2x150bp 300X per individual 
        - PacBio CCS 15kb_20kb chemistry2

## MGeND
[MGeND](https://mgend.ncgm.go.jp/) is a database that deposits variant information obtained from genomic medicine research and clinical testing together with clinical information, and has the same orientation as clinVar[^1]. MGeND deposits data mainly from studies conducted in Japan, and VICS has been considering the acceptance of data such as structural variants that are expected to be registered in medical research in the future.
- Register MGeND variant records in UCSC Genome Browser tracks. 
- Development of a new variant registration system based on PubcaseFinder CaseSharing.

## JVar
[JVar](https://www.ddbj.nig.ac.jp/jvar/index-e.html) is a database of human variants operated by DDBJ. In principle, JVar data will be exchanged with [dbSNP](https://www.ncbi.nlm.nih.gov/snp/) and [dbVar](https://www.ncbi.nlm.nih.gov/dbvar/) for international data sharing. JVar data will be integrated with TogoVar to provide a fancy interface for searching and analysis in near future.
- Whole genome sequencing data (NA19079; Hapmap JPY) analyzed by International 1000 Genomes are analyzed by manta SV caller, and the obtained data of structural variants are registered to JVar. Problems identified in the process will be discussed.
- Got a BioProject ID (PRJDB16199), which describes the purpose of this research, from DDBJ.
- VCF was made from the output of manta. VCF togather with meta information were submitted to JVar team.
- the submitted VCF were applied to validator developed by Yuichi Kodama and discussed about criteria of each SVTYPE in JVar-SV  submission.


## Genomic Variation of Diverse human populations
Large scale human genome data have been collected from the public database for anthropological studies. At present, [the genome data](https://sc.ddbj.nig.ac.jp/en/advanced_guides/advanced_guide_2023/#reanalysis-dataset-of-public-data-of-human-whole-genome-analysis) (CRAM and VCF) of 5,098 individuals from worldwide populations are released on the DDBJ supercomputer.
In addition, we are compiling a database (JoGo) of the results of whole genome sequencing analysis using immortalized B cell-derived DNA from HapMap JPT.
- Will deposit variant information to JVar
- Make meta data containing sample attributes (population, project, gender, file path, etc)
- Begin discussions with Dr. Robert Hoehndorf on integration with the full-length genome of the Saudi Arabian population being analyzed at KAUST.
 

# Future work
- Provide the Variant data and metadata issued JVar-SV accession as public data from JVar/TogoVar.
- Update [Genome Variation Ontology (GVO)](https://ceur-ws.org/Vol-3415/paper-22.pdf) perspective from a database registration/publication.
- Discuss JSON Lines as data exchange format and Design of a data model in JSON format describing SNPs and SVs corresponding to the current RDF models.
- We are going to perform additional SV call and meticulously assess the definition, ambiguity of detection region boundaries, and representation of detection outcomes. Subsequent to our investigations, we will systematically categorize the discrepancies, taking into account SV types, and formulated criteria for subsequent normalization.

# Acknowledgements

Dr.Toyofumi Fujiwara kindly provide PubcaseFinder CaseSharing for MGeND submission tools.
Thanks to Dr. Yuichi Kodama for rapid response in checking the submitted data.
Thanks to the biohackathon organizers and biohackers.

# References
[^1]: [Kamada et al. "MGeND: an integrated database for Japanese clinical and genomic information." Human Genome Variation. 2019;6(1)]([Link1](https://www.nature.com/articles/s41439-019-0084-4))
