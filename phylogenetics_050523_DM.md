### Bioinformatics Practical 3. Phylogentic inferences

**Aim of the practical**

**1)** To learn the principle of phylogenetic tree construction

**2)** Steps in building a basic phylogenetic tree

**3)** Constructing a phylogenetic tree in R

# Principle of tree construction

We will do a fun exercise before we do a real phylogenetic tree construction. Can you place these new organisms in order? And give your rationale for your placement of that organism in this tree.

![](https://raw.githubusercontent.com/shri1984/study-images/main/Picture1.jpg?token=GHSAT0AAAAAACCFFFMC5RONLSSBPRYSKJBGZCUWWBQ)

## Building a phylogenetic tree using some anatomical characters

Table below contains charatcters to make our tree. + indicates presence and 0 represents absence. This data taken from Principles of biology by Robert Bear (table from khan academy) with some modifications.

![](https://raw.githubusercontent.com/shri1984/study-images/main/Screen%20Shot%202023-05-03%20at%2012.23.01.png?token=GHSAT0AAAAAACCFFFMDFNA5P5PWHFBIYVHCZCUWUQQ)

One important thing we should know from above table is what forms the ancestral trait, and which are derived traits. This is important to make a tree based on characters. An ancestral trait is what we think was
present in the recent common ancestor of the species of interest. Also, if the trait is present only in the outgroup you can call it ancestral trait. A derived trait is a trait or character that appears somewhere on a
lineage descended from recent common ancestor.

We will start building a tree now. Lampery lacks all the traits listed
in the table. Hence we can assume that ancestors for these group of
organisms lacked these listed traits. Presence of any or all features
indicates they are derived traits.

1.  Which of these characters are mostly shared by ? Jaws. Present in
    all except lampreys. So start off with drawing lamprey branching off
    from the rest.

2.  What’s the next character shared by most of the species? Next, we
    can look for the derived trait shared by the next-largest group of
    organisms. This would be lungs, shared by the antelope, bald eagle,
    and alligator, but not by the sea bass. Based on this pattern, we
    can draw the lineage of the sea bass branching off, and we can place
    the appearance of lungs on the lineage leading to the antelope, bald
    eagle, and alligator.

3.  Following the same pattern, we can now look for the derived trait
    shared by the next-largest number of organisms. That would be the
    gizzard, which is shared by the alligator and the bald eagle (and
    absent in antelope). Based on this data, we can draw the
    antelope lineage branching off from the alligator and bald eagle
    lineage, and place the appearance of the gizzard on the latter.

4.  What about our remaining traits of fur and feathers? These traits
    are derived, but they are not shared, since each is found only in a
    single species. Derived traits that aren’t shared by many don’t help
    us build a tree, but we can still place them on the tree in their
    most likely location. For feathers, this is on the lineage leading
    to the bald eagle (after divergence from the alligator). For fur,
    this is on the antelope lineage, after its divergence from the
    alligator and bald eagle.

# Constructing a phylogenetic tree in R

Phylogentics in R needs various packages such as `msa` (Bonatesta et
al), `bios2mds`,(Pele et al) and `phangorn` (Schliep et al). One benefit
of using R functions to calculate the phylogentic tree is that you dont
need some other software(s) which are many times OS dependent and hence,
unpredictable.

## 1. Install or load R packages

Some of the packages (phangorn, tinytex, and bios2mds) can be directly
downloadable from R studio “packages” tab. However, **msa package** and **ggmsa**
needs to be downloaded using **Bioconductor**. Type ***“msa r package”*** in
google and find relevant bioconductor package. Read relevant information
about how to download msa. First you may need to download package downloader called **bioconductor**

```
if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

BiocManager::install("msa")

BiocManager::install("ggmsa")

```
#load packages
library(msa) 
library(bios2mds) 
library(phangorn) 
library(ape)
library(stats)
library(ggplot2)
library(ggmsa)

# Alignment of nucleotide sequences

## Read sequences in fasta format into msa (Multiple Sequence Alignment) algorithm

mysequencefile <- readDNAStringSet("phylogenetics_tree.fasta", format = "fasta") 

### Run multiple alignemnt analysis using `muscle` program in msa

This following step can lot of time, depending on number of sequences
and length. Here it will go fast.

alignmuscle  <- msa(mysequencefile, method = "Muscle")

align_format <- msaConvert(alignmuscle, type= "bios2mds::align")

you can write alignment data to a file instead of keeping it in an R object, use

```
export.fasta(align_format, outfile = "myAlignment.fasta", ncol = 60, open = "w")

```

Now open the file myAlignment.fasta in bbedit and see the content. You see there is string of NAs at the end of each fasta sequence. It is a bug or artefact. We will remove them manually. 

If ypu want to see the part of alignment , use function ggmsa from ggmsa package. 

```
ggmsafile<- "/Users/sbh001/Library/CloudStorage/OneDrive-UiTOffice365/course-FSK2053/lecture3_phylogenetics/myAlignment.fasta"

ggmsa(ggmsafile, 300, 350, color = "Clustal", font = "DroidSansMono", char_width = 0.5, seq_name = TRUE ) # see alignment in coliurful format.

```

Once you are done with alignment, next step is making the phylogenetic
tree. This follwing function converts a multiple sequence alignment
object to formats used in other sequence analysis packages. Benefit of
this is that you can directly proceed to other packages without reading
the input again. Here we will convert msa object into DNAbin object reqired by paclakge ***ape**.

```
alignmentfish <- msaConvert(alignmuscle, type= "ape::DNAbin")

```

Now we will try to do some phylogenetic trees based on different
methods.

## Phylogenetic tree construction

Distance-based trees are produced by calculating the genetic distances between pairs of taxa/species/measurements, followed by hierarchical clustering that creates the actual “tree” look. Two popular clustering methods that are used most frequenctly for distance based clustering method are UPGMA and NJ algorithms.

UPGMA- this is the simplest method for constructing trees, assumes the same evolutionary speed for all lineages (which can be a disadvantage); all leaves have the same distance from the root (creates ultrametric tree)

Neighbor-joining- taking the two closest nodes of the tree and defines them as neighbors; you keep doing this until all of the nodes have been paired together


### Distance based phylogenetic tree construction

First calculate a distance matrix from ***ape** package

```
D <- dist.dna(alignmentfish, model = "TN93")  #just the type of evolutionary model we’re using, this particular one allows for different transition rates, heterogenous base frequencies, and variation of substitution rate at the same site

length(D) #number of pairwise distances, computed as n(n-1)/2

```
Now use object dm to costruct two distance based phylogenetic trees. There are lot of functions in R to build distance based phylogenetic tree. But we will use few of them here mainly from ***ape** package

```
treeNJ <- nj(D)

class(treNJ) #all trees created using ape package will be of class phylo

treeNJ <- ladderize(treeNJ) #This function reorganizes the internal structure of the tree to get the ladderized effect when plotted

treNJ # tells us what the tree will look like but doesn't show the actual construction

treeUPGMA <- hclust(D, method = "average", members = NULL) # method = average is used for UPGMA, members can be equal to NULL or a vector with a length of size D. This tree is called an ultrametric tree, 

```
Plot trees using generic function. Remember here we are just making tree strucure. But you can play around and make colourful trees using different functions. 

```
plot(treUPGMA, main="A Simple UPGMA Tree")

plot(treeNJ, type = "phylogram", main="A Simple NJ Tree", show.tip=FALSE)

add.scale.bar()

```
if you want make rooted NJ treee,

```
treeNJroot <- root(treNJ, outgroup = "KM224857_Esox_lucius", resolve.root = TRUE, edgelabel = TRUE)


treeNJroot <- ladderize(treeNJout)

plot(treeNJroot, show.tip=FALSE, edge.width=2, main="Rooted NJ tree")

add.scale.bar()

```
As we have lot of options to make a phylogenetics trees, we have to make sure that the alogrithm we chose to make tree is the right one to explain the sequence data. We need to test what type of algorithm explains the data well (NJ or UPGMA?)

## choosing 'right' algorithm 

We will use correlation analysis between the caluclated distnce between the taxa and cophenetic distance to choose the the right tree. The cophenetic distance between two observations that have been clustered is defined to be the intergroup dissimilarity at which the two observations are first combined into a single cluster. Note that this distance has many ties and restrictions.

```
x <- as.vector(D) # convert D as vector
y <- as.vector(as.dist(cophenetic(tre2))) # caluclate cophentic distance from tre2 and convert it to vector. Cophenetic function computes distances between the tips of the trees
plot(x, y, xlab="original pairwise distances", ylab="pairwise distances on the tree", main="Is UPGMA appropriate?", pch=20, col="red", cex=3)
abline(lm(y~x), col="red")
cor(x,y)^2

#### UPGMA tree
y <- as.vector(as.dist(cophenetic(treeUPGMA)))
plot(x, y, xlab="original pairwise distances", ylab="pairwise distances on the tree", main="Is UPGMA appropriate?", pch=20, col="red", cex=3)
abline(lm(y~x), col="red")
cor(x,y)^2

```
choose right tree and proceed to bootstrapping.

### Run bootstrapping

Bootstrapping is a test or metric that uses random sampling withreplacement and falls under the broader class of resampling methods. It
uses sampling with replacement to estimate the sampling distribution for
the estimator (Ojha et al 2022). Basic idea is building same tree
leaving out some portion of evidence (some bases from a sequence) and check if same clades appear
even after leaving out some data

First we need to write a function

    fun <- function(x) root(nj(dist.dna(x, model = "TN93")),1) ## function calculates distance first and then tree is calculated from alignment. function fun performs tree building on the input x using the upgma algorithm after calculating the pairwise distance between elements using dist.ml.

Then need to calculate boot strap values through bootstrap.phyDat function from phangron.

bs_nj <- boot.phylo(treeNJroot, alignmentfish, fun) # performs the bootstrap automatically for us

bs_nj

plot the bootstrap values on tree branches like below 

```
plot(treeNJroot, show.tip=FALSE, edge.width=2, main = "NJ tree + bootstrap values") #plot bootstrap values

add.scale.bar()

nodelabels(bs_nj, cex=.6) # adds labels to or near the nodes

```
How does node support looks? the numbers shown by nodelabels() show how many times each node appreared in the bootstrapped trees. If the numbers by each node are pretty low, meaning there’s not a huge overlap between the nodes in our original tree and the nodes in the bootstrapped tree. Tt means that some of the nodes aren’t supported.

How do we overcome this and fix our tree? We can collapse some of the smaller branches, which will make the tree less informative but more concrete.

```
temp <- treeNJroot
N <- length(treeNJroot$tip.label)
toCollapse <- match(which(bs_nj<70)+N, temp$edge[,2])
temp$edge.length[toCollapse] <- 0
treeNJroot_trimmed <- di2multi(temp, tol=0.00001)
plot(treeNJroot_trimmed, show.tip=FALSE, edge.width=2, main = "NJ tree after collapsing weak nodes")

```

### Parsimony based trees

Now we will caluclate parsimony score, which is the minimum number of changes ncecessary to describe the data for a given tree type.

```
align_phydata <- msaConvert(alignmuscle, type= "phangorn::phyDat")

parsimony(treeNJroot, align_phydata) #parsimony returns the parsimony score of a tree

tre.pars.nj <- optim.parsimony(treNJ, align_phydata)
tre.pars.nj 

plot(tre.pars.nj, type="unr", show.tip=FALSE, edge.width=2, main = "Maximum-parsimony tree") #it has lower parsimonious score compare to the original tree.

```

### Maximum Likelihood-based 

#### compare different nucleotide substitution models we needed to make MxL-based tree

As a first step, we will try to find the best fitting substition model. For this we use the function `modelTest` to compare different nucleotide or protein models with the AIC, AICc or BIC

```
mt <- modelTest(align_phydata, control=pml.control(trace=0))

fit <- as.pml(mt, "BIC") #choose best model based on BIC criteria

```

##  make a ml tree

```
dm <- dist.dna(align_phydata)

tree <- nj(D)

fit.ini <- pml(tree, align_phydata )

fitTrN <- optim.pml(fit.ini, model="TrN", optInv=TRUE, optGamma=TRUE, rearrangement = "stochastic", control = pml.control(trace = 0))

anova(fit.ini, fitTrN)


```

It is important to verify which tree was better and has good evidence? 

```
anova(fit.ini, fit)

AIC(fit.ini)

AIC(fit)

```
Both the ANOVA test (highly significant) and the AIC (lower=better) indicate that the new tree is a better model of the data than the initial one.

```
tre4 <- root(fit$tree,1)
tre4 <- ladderize(tre4)
plot(tre4, show.tip=FALSE, edge.width=2, main = "Maximum-likelihood tree")

```






Extra information: ’Beauti’fication of phylogenetic trees can be done
using `ggplot`and its associated package called `ggtree` can be used to
make trees more beautiful.

######## Reference: some scripts are taken from tutorial: estimating phylogenetic trees with phangorn
