---
title: BioJava:Cookbook:Sequence:SubSequence
permalink: wiki/BioJava%3ACookbook%3ASequence%3ASubSequence
---

How do I get a subsection of a Sequence?
----------------------------------------

Given a Sequence object we might only be interested in examining the
first 10 bases or we might want to get a region between two points. You
might also want to print a subsequence to an OutputStream like STDOUT
how could you do this?

BioJava uses a biological coordinate system for identifying bases. The
first base is numbered 1 and the last base index is equal to the length
of the sequence. Note that this is different from String indexing which
starts at 0 and proceedes to length -1. If you attempt to access a
region outside of 1...length an IndexOutOfBoundsException will occur.

### Getting a Sub - Sequence

```java

`   SymbolList symL = null;`

`   //code here to generate a SymbolList`

`   //get the first Symbol`  
`   Symbol sym = symL.symbolAt(1);`

`   //get the first three bases`  
`   SymbolList symL2 = symL.subList(1,3);`

`   //get the last three bases`  
`   SymbolList symL3 = symL.subList(symL.length() - 3, symL.length());`

```

### Printing a Sub - Sequence

```java

`   //print the last three bases of a SymbolList or Sequence`  
`   String s = symL.subStr(symL.length() - 3, symL.length());`  
`   System.out.println(s);`

```

### Complete Listing

```java import org.biojava.bio.seq.\*; import org.biojava.bio.symbol.\*;

public class SubSequencing {

` public static void main(String[] args) {`  
`   SymbolList symL = null;`

`   //generate an RNA SymbolList`  
`   try {`  
`     symL = RNATools.createRNA("auggcaccguccagauu");`  
`   }`  
`   catch (IllegalSymbolException ex) {`  
`     ex.printStackTrace();`  
`   }`

`   //get the first Symbol`  
`   Symbol sym = symL.symbolAt(1);`

`   //get the first three bases`  
`   SymbolList symL2 = symL.subList(1,3);`

`   //get the last three bases`  
`   SymbolList symL3 = symL.subList(symL.length() - 3, symL.length());`

`   //print the last three bases`  
`   String s = symL.subStr(symL.length() - 3, symL.length());`  
`   System.out.println(s);`  
` }`

} ```
