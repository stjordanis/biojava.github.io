---
title: BioJava:CookBook:Distribution:XML
permalink: wiki/BioJava%3ACookBook%3ADistribution%3AXML
---

How can I write a Distribution to XML?
--------------------------------------

If you frequently construct Distributions from large training sets for
later analysis it is desirable to be able to store these Distributions
for latter use. One possibility is to serialize the Distribution to
binary. Serialization, while ideal for short term storage or
communication between Java VMs, is fragile and likely to break between
different versions of BioJava. It is also impossible to inspect by eye.

A better solution is write the Distribution to XML, providing a long
term, human readable and language independent solution. The following
example shows how a Distribution can be written to XML and read back
again. The example requires a fairly recent version of BioJava as the
readFromXML() and writeToXML() methods in DistributionTools are fairly
new features. The cvs version or version 1.3 (when released) will be
adequate.

```java import java.io.\*;

import org.biojava.bio.dist.\*; import org.biojava.bio.seq.\*;

public class Dist2XMLAndBack{

` public static void main(String[] args){`

`     try{`  
`       File temp = File.createTempFile("xmltemp", ".xml");`

`       //create a Distribution to write`  
`       Distribution d = DistributionFactory.DEFAULT.createDistribution(DNATools.getDNA());`

`       //give the Distribution some random values`  
`       DistributionTools.randomizeDistribution(d);`

`       //write it to 'temp'`  
`       DistributionTools.writeToXML(d, new FileOutputStream(temp));`

`       //read it back in`  
`       Distribution d2 = DistributionTools.readFromXML(new FileInputStream(temp));`

`       //check that the weights are reproduced`  
`       boolean b = DistributionTools.areEmissionSpectraEqual(d, d2);`

`       System.out.println("Are values reproduced? " + b);`  
`     } catch(Exception ex){`  
`       ex.printStackTrace();`  
`     }`

` }`

} ```
