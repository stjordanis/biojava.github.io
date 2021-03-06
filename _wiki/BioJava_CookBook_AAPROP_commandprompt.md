---
title: BioJava:CookBook:AAPROP:commandprompt
permalink: wiki/BioJava%3ACookBook%3AAAPROP%3Acommandprompt
---

### How can I compute physico-chemical properties using Command Prompt?

1) Download
[biojava3-aa-prop-3.0.2-SNAPSHOT-jar-with-dependencies.jar](http://www.biojava.org/download/maven/org/biojava/biojava3-aa-prop/3.0.2-SNAPSHOT/biojava3-aa-prop-3.0.2-SNAPSHOT-jar-with-dependencies.jar)
and rename it to AAProperties.jar  
2) Study the Manual section below  
Note: [Test.fasta](Test.fasta "wikilink") is available if you would need
sample fasta sequences.

### Manual

<b>NAME</b>

    An executable to generate physico-chemical properties of protein sequences.

<b>EXAMPLES</b>

    java -jar AAProperties.jar -i test.fasta -a
        Generates all possible properties.

    java -jar AAProperties.jar -i test.fasta -1 -3 -7
        Generates only molecular weight, extinction coefficient and isoelectric point.

    java -jar AAProperties.jar -i test.fasta -0 A -0 N -1
        Generates composition of two specific amino acid symbol and molecular weight.

<b>OPTIONS</b>

    Required
        -i location of input FASTA file

    Optional
        -o location of output file [standard output (default)]
        -f output format [csv (default) or tsv]
        -x location of Amino Acid Composition XML file for defining amino acid composition
        -y location of Element Mass XML file for defining mass of elements
        -d number of decimals (int) [4 (default)]

    Provide at least one of them
        -a compute properties of option 1-9
        -1 compute molecular weight
        -2 compute absorbance
        -3 compute extinction coefficient
        -4 compute instability index
        -5 compute apliphatic index
        -6 compute average hydropathy value
        -7 compute isoelectric point
        -8 compute net charge at pH 7
        -9 compute composition of 20 standard amino acid (A, R, N, D, C, E, Q, G, H, I, L, K, M, F, P, S, T, W, Y, V)
        -0 compute composition of specific amino acid symbol
