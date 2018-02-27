## Overview ##

**SiFit** is a tool for reconstructing phylogenetic tree from noisy mutation profile of single cells. Given an imperfect noisy genotype matrix from single cells, **SiFit** employs a heuristic search algorithm to infer the Maximum Likelihood (ML) phylogenetic tree under a finite-site model of evolution. Along with tree inference, error rates of the single-cell dataset can also be estimated.

## Publication ##
**SiFit: inferring tumor trees from single-cell sequencing data under finite-sites models** 

Hamim Zafar, Anthony Tzen, Nicholas Navin, Ken Chen and Luay Nakhleh

Genome Biology 2017, 18:178 

[https://genomebiology.biomedcentral.com/articles/10.1186/s13059-017-1311-2]()

## Dependencies ##

* PhyloNet ([https://bioinfo.cs.rice.edu/phylonet]())
* The Apache Commons Mathematics Library ([http://commons.apache.org/proper/commons-math]())
* Parallel Colt ([https://mvnrepository.com/artifact/net.sourceforge.parallelcolt/parallelcolt]())
* Habanero-Java Library ([https://wiki.rice.edu/confluence/display/PARPROG/HJ+Library]())

## Installation ##

The binary [SiFit.jar](https://bitbucket.org/hamimzafar/sifit/src/a601ab4a677457c536614a6a34f0a9a12e2fdf50/SiFit.jar?at=master&fileviewer=file-view-default) is directly downloadable.

## Usage ##

To run SiFit for tumor phylogeny inference, the genotype matrix should be obtained from single-cell DNA sequencing data. An example genotype matrix **dataset_20cells.txt** is provided in the ***exampleFiles*** directory. The corresponding true phylogenetic tree is provided in the file **Tree_20cells.newick** in newick format. To infer the maximum likelihood (ML) tree from this given dataset, SiFit can be executed as follows.

```
java -jar SiFit.jar -m 20 -n 446 -fp 0.002 -fn 0.2 -iter 10000 -df 1 -ipMat exampleFiles/dataset_20cells.txt
```
SiFit outputs the ML tree in newick format and also outputs the ML false negative rate.

## Input Files ##
### Genotype Matrix ###
The mutational profile of single cells are represented as a genotype matrix and it has to be provided as input. The first column of the matrix contains the position of the mutation. Each of the rest of the columns represents the mutation profile of a single cell. Each row represents one mutation. The first entry of each row contains the position of the mutation. The other entries represent the genotype of the corresponding cell for the given mutation. Columns are separated by a white space character. The genotype matrix can be binary/ternary.

a)*** Binary:*** 
The genotype information represents the presence/absence of a mutation. The entry at position [i, j+1] should be

* 0 if mutation i is not observed in cell j,
* 1 if mutation i is observed in cell j, or
* 3 if the genotype information is missing.

a)*** Ternary:*** 
The genotype information represents homozygous reference, heterozygous variant and homozygous variant respectively. The entry at position [i, j+1] should be

* 0 if mutation i is not observed in cell j,
* 1 if mutation i is heterozygous variant in cell j, 
* 2 if mutation i is homozygous variant in cell j, or
* 3 if the genotype information is missing.

### Cell Names (Optional) ###
A file specifying the names of the single cells. The names should appear in a row in the same order as in the genotype matrix separated by white space character.

### The True Tree (Optional) ###
For simulated datasets, for which the true tree is known, the true tree can be provided to SiFit for comparing the inferred tree. The true tree should be provided as an input file in Newick format. If the true tree is provided, SiFit will also report the tree reconstruction error.

## Output File ##
### Inferred Tree ###
The ML tree inferred by SiFit is written to file in Newick format. The output file obtains the base name from the input file and adds an extension ```_mlTree.newick```.

## Arguments ##
* ```-m <Integer>``` Replace <Integer> with the number of cells in the dataset.

* ```-n <Integer>``` Replace <Integer> with the number of mutations (rows) in the dataset.

* ```-ipMat <filename>``` Replace <filename> with the path to the file containing the genotype matrix.

* ```-fp <Double>``` Set <Double> to the estimated false positive rate of the single-cell sequencing experiment. 

* ```-fn <Double>``` Set <Double> to the estimated allelic dropout rate of the single-cell sequencing experiment. This will be used for setting the prior distribution for estimating false negative rate.

* ```-r <Integer>``` Set <Integer> to the desired number of restarts to use.

* ```-iter <Integer>``` Set <Integer> to the number of iterations to run for each restart.

* ```-df <Integer>``` Set <Integer> to 1 if the input matrix is ternary. Set <Integer> to 0 if the input matrix is binary.

## Optional Arguments ##
* ```-cellNames <filename>``` Replace <filename> with the path to the file containing the names of the cells. The cell names should be written in a single row separated by blank spaces. The order of the names of the cells should be same as the order in any row of the file containing the genotype matrix. If no such file is provided, the cells are numbered 1 to m.

* ```-trueTree <filename>``` Replace <filename> with the path to the file containing the ground truth tree. The true phylogenetic tree should be written in Newick format. The names of the leaves in the true tree should match the names of the cells. If this file is provided, then the program outputs tree reconstruction error.

* ``` -e <Double>``` Set <Double> to a value between 0 and 1. This specifies the probability of choosing the error rate changing move during the heuristic search process.  

* ``` -mp <Double>``` Set <Double> to a value between 0 and 1. This specifies the probability of choosing a move that proposes a new value for the parameters of the model of evolution during the heuristic search process. The model of evolution has two parameters, either of these two parameters is modified by each such move.

* ``` -mh <Double>``` Set <Double> to a value between 0 and 1. This specifies the probability of choosing a Metropolis-Hastings step. Metropolis-Hastings steps are used with a small probability while proposing a new error rate or a new phylogenetic tree. The default value is 0.1, only small values (< 0.25) are recommended.

* ``` -printIter <Integer>``` Set <Integer> to the number of iterations after which the best value of likelihood is to be printed to the standard output. This should be smaller than the total number of iterations for each restart.

## License ##
SiFit is released under the [MIT License](http://www.opensource.org/licenses/MIT).

## Inferring The Order of Mutations ##
**InferAncestralStates** program of **SiFit** can be used for inferring the order of mutations on the branches of the tumor phylogeny. The program should be executed as follows
```
java -cp SiFit.jar SiFit.algorithm.InferAncestralStates 
```
Following are the arguments for this program
# Arguments #
* ```-fp <Double>``` Set <Double> to the false positive rate of the single-cell sequencing experiment.

* ```-fn <Double>``` Set <Double> to the ML estimate of false negative rate reported by SiFit during learning the tree.

* ```-w <Double>``` Set <Double> to the ML estimate of LOH rate reported by SiFit during learning.

* ```-d <Double>``` Set <Double> to the ML estimate of deletion rate reported by SiFit during learning.

* ```-df <Integer>``` Set <Integer> to 0 if the input matrix is binary. Currently, we support only binary input matrix for this program.

* ```-ipMat <filename>``` Replace <filename> with the path to the file containing the input genotype matrix.

* ```-tree <filename>``` Replace <filename> with the path to the file containing the newick string format for the tree inferred by SiFit.

* ```-cellNames <filename>``` Replace <filename> with the path to the file containing the names of the cells in the dataset. It should be a text file that has the names of the cells in a single line separated by whitespace, the cell names should match the leaf names of the tree, also should be in the same order as they appear in the input genotype matrix.

* ```-geneNames <filename>``` Replace <filename> with the path to the file containing the names of the genes that are mutated. Each row of this test file should contain one gene name. The names of the genes should be in the same order as they appear in the input genotype matrix.

* ```-expectedMatrix <filename>``` Replace <filename> output file where the expected genotype matrix will be written.


