## Overview ##

**SiFit** is a tool for reconstructing phylogenetic tree from noisy mutation profile of single cells. Given an imperfect noisy genotype matrix from single cells, **SiFit** employs a heuristic search algorithm to infer the Maximum Likelihood (ML) phylogenetic tree under a finite-site model of evolution. Along with tree inference, error rates of the single-cell dataset can also be estimated.

## Dependencies ##

* PhyloNet ([https://bioinfo.cs.rice.edu/phylonet]())
* The Apache Commons Mathematics Library ([http://commons.apache.org/proper/commons-math]())
* Parallel Colt ([https://mvnrepository.com/artifact/net.sourceforge.parallelcolt/parallelcolt]())