---
title: BioJava:Cookbook:Sequence:Reverse
permalink: wiki/BioJava%3ACookbook%3ASequence%3AReverse
---

How do I Reverse Complement a Sequence or SymbolList?
-----------------------------------------------------

To reverse complement a DNA SymbolList or Sequence simply use the
DNATools.reverseComplement(SymbolList sl) method. An equivalent method
is found in RNATools for performing the same operation on RNA based
Sequences and SymbolLists.

```java import org.biojava.bio.symbol.\*; import org.biojava.bio.seq.\*;

public class ReverseComplement {

` public static void main(String[] args) {`  
`  `  
`   try {`  
`     //make a DNA SymbolList`  
`     SymbolList symL = DNATools.createDNA("atgcacgggaactaa");`

`     //reverse complement it`  
`     symL = DNATools.reverseComplement(symL);`  
`    `  
`     //prove that it worked`  
`     System.out.println(symL.seqString());`  
`   }`  
`   catch (IllegalSymbolException ex) {`  
`     //this will happen if you try and make the DNA  seq using non IUB symbols`  
`     ex.printStackTrace();`  
`   }catch (IllegalAlphabetException ex) {`  
`     //this will happen if you try and reverse complement a non DNA (RNA) sequence using DNATools (RNATools)`  
`     ex.printStackTrace();`  
`   }`  
` }`

} ```
