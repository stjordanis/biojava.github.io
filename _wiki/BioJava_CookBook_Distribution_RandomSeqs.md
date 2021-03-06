---
title: BioJava:CookBook:Distribution:RandomSeqs
permalink: wiki/BioJava%3ACookBook%3ADistribution%3ARandomSeqs
---

How can I generate a random Sequence from a Distribution?
---------------------------------------------------------

BioJava Distribution objects have a method for sampling Symbols. By
successively sampling enough Symbols you can build up a random sequence.
Because this is a common task a static method is provided in
DistributionTools called generateSequence().

The following program generates a random Sequence using a uniform
Distribution over the DNA Alphabet. The emitted sequence will differ
each time although its composition should be close to 25% of each
residue. Non uniform distributions can be used to generate biased
sequences.

```java import org.biojava.bio.dist.\*; import org.biojava.bio.seq.\*;
import org.biojava.bio.seq.io.\*; import java.io.\*;

public class RandomSequence {

` public static void main(String[] args) {`

`   //make a uniform distribution over the DNA Alphabet`  
`   Distribution dist = new UniformDistribution(DNATools.getDNA());`

`   //generate a 700bp random sequence`  
`   Sequence seq = DistributionTools.generateSequence("random seq", dist, 700);`

`   try {`  
`     //print it to STDOUT`  
`     SeqIOTools.writeFasta(System.out, seq);`  
`   }`  
`   catch (IOException ex) {`  
`     //io error`  
`     ex.printStackTrace();`  
`   }`  
` }`

} ```
