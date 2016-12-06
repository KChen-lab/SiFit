## Overview ##

**SiFit** is a tool for reconstructing phylogenetic tree from noisy mutation profile of single cells. Given an imperfect noisy genotype matrix from single cells, **SiFit** employs a heuristic search algorithm to infer the Maximum Likelihood (ML) phylogenetic tree under a finite-site model of evolution. Along with tree inference, error rates of the single-cell dataset can also be estimated.

## Dependencies ##

* PhyloNet ([https://bioinfo.cs.rice.edu/phylonet]())
* The Apache Commons Mathematics Library ([http://commons.apache.org/proper/commons-math]())
* Parallel Colt ([https://mvnrepository.com/artifact/net.sourceforge.parallelcolt/parallelcolt]())

## Installation ##

The binary **SiFit.jar** is directly downloadable.

## Usage ##

To run SiFit for tumor phylogeny inference, the genotype matrix should be obtained from single-cell DNA sequencing data. An example genotype matrix **dataset_20cells.txt** is provided in the exampleFiles directory. The corresponding true phylogenetic tree is provided in the file **Tree_20cells.newick** in newick format. To infer the maximum likelihood (ML) tree from this dataset, SiFit can be executed as follows.

```
java -jar SiFit.jar -m 20 -n 446 -fp 0.002 -fn 0.2 -iter 10000 -df 1 -ipMat exampleFiles/dataset_20cells.txt -trueTree exampleFiles/Tree_20cells.newick
```