## Overview ##

**SiFit** is a tool for reconstructing phylogenetic tree from noisy mutation profile of single cells. Given an imperfect noisy genotype matrix from single cells, **SiFit** employs a heuristic search algorithm to infer the Maximum Likelihood (ML) phylogenetic tree under a finite-site model of evolution. Along with tree inference, error rates of the single-cell dataset can also be estimated.

## Dependencies ##

* PhyloNet ([https://bioinfo.cs.rice.edu/phylonet]())
* The Apache Commons Mathematics Library ([http://commons.apache.org/proper/commons-math]())
* Parallel Colt ([https://mvnrepository.com/artifact/net.sourceforge.parallelcolt/parallelcolt]())

## Installation ##

The binary **SiFit.jar** is directly downloadable.

## Usage ##

To run SiFit for tumor phylogeny inference, the genotype matrix should be obtained from single-cell DNA sequencing data. An example genotype matrix **dataset_20cells.txt** is provided in the ***exampleFiles*** directory. The corresponding true phylogenetic tree is provided in the file **Tree_20cells.newick** in newick format. To infer the maximum likelihood (ML) tree from this given dataset, SiFit can be executed as follows.

```
java -jar SiFit.jar -m 20 -n 446 -fp 0.002 -fn 0.2 -iter 10000 -df 1 -ipMat exampleFiles/dataset_20cells.txt
```
SiFit outputs the ML tree in newick format and also outputs the ML false negative rate.

## Input Files ##
1. ### Genotype Matrix ###
The mutational profile of single cells are represented as a genotype matrix and it has to be provided as input. The first column of the matrix contains the position of the mutation. Each of the rest of the columns represents the mutation profile of a single cell. Each row represents one mutation. The first entry of each row contains the position of the mutation. The other entries represent the genotype of the corresponding cell for the given mutation. Columns are separated by a white space character. The genotype matrix can be binary/ternary.
### a) Binary: ### The genotype information represents the presence/absence of a mutation