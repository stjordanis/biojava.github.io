---
title: BioJava:PhyloSOC07
---

This page will include all info and docs about our efforts in the 2007
Google Summer of Code as part of the NESCent phyloinformatics group.

**<APIs for BioJava: Project Plan>**

**Part I : Development of basic I/O**

*Week 1 Development of basic Input*

- Input: Nucleic acid sequences (practice w/ FASTA format and create API
for NEXUS format)

- Initialization: create objects for each sequence

*Week 2 Development of basic Output*

- Tree constructing practice with JGraphT
(http://www.jgrapht.org/javadoc/ )

- Output file creation in NEXUS format(converting tree object into NEXUS
format)

**Part II: Distance method (multiple hit correction method)**

*Week 3 Jukes-Cantor*

*Week 4 Kimura's 2-parameter*

**Part III: Distance based phylogeny reconstruction**

*week5 UPGMA method & Neighbor-Joining method*

[UPGMA]

1. finding shortest distance within distance matrix

2. calculate branch lengths as distance/2

3. build a sub-tree for that pair

4. collapse a pair (changes distance into 0)

5. repeat process expanding/combining trees

[N-J]

1. S = total branch length of tree

2. separate pair of taxa from all others

3. choose pair of taxa that minimizes S

4. build a sub-tree for that pair

5. collapse pair as distance and recalculate distance matrix

6. next pair that gives smallest S is chosen

7. repeat until complete

*Week 6 Documentation for Part I & II & III* : (JavaDoc and BJ website)

**Part III : Maximum Parsimony**

*Week 7 & 8 Maxumum Parsimony Method*

1. aligning sequences

2. decide informative sites (2 or more differences)

3. create tree type and calculate \# of base changes for that tree

4. repeat step 3 for all informative sites

5. for each tree type, add \# of changes for all sites

6. find the tree with smallest number of changes

**Part IV : Maximum Likelihood**

*Week 9 & 10 Maxumum Likelihood Method*

1. aligning sequences

2. define possible tree types

3. for each tree, calculate

`  L = multiply Pr(D|T) for every sites`  
`  Pr(D|T) = (prob. for the tree from certain ancestral base)`

4. find a tree with maximum likelihood

**Part V : Phylogeny supporting method**

*Week 11 Bootstrap method*

1. replicate alignments

- taking the original sequence alignment

- entire column is randomly sampled(w/ replacement)

2. for each re-sampled replicate alignment, reconstruct phylogeny based
on the method

3. count the number of replicates that each internal branch of the
original tree is found

*Week 12 Documenting: part IV & V*