---
title: BioLit
---

BioJava module: BioLit
----------------------

The BioJava - BioLit module allows to perform web service request to the
webservices provided by [BioLit](http://biolit.ucsd.edu). BioLit allows
to access information from open access articles that are published in
PubMedCentral.

This library is used by the RCSB-PDB web site to dynamically request the
data from the [BioLit RESTful web
services](http://biolit.ucsd.edu/doc/rest.jsp). For an example see here:
[<http://www.rcsb.org/pdb/explore/literature.do?structureId=1aoi>](http://www.rcsb.org/pdb/explore/literature.do?structureId=1aoi)

### Source Code Examples

```java

import org.rcsb.biolit.io.TermParser;

/\*\* Get PDB codes that are cited in the same articles as the query PDB
id.

`*`  
`*`  
`*/`

public class GetRelated {

`  public static void main(String[] args){`  
`     String pdb = "1hiv";`

`     TermParser parser = new TermParser();`  
`     try{`  
`        List`<String>` ids = parser.fetch(pdb);`

`        for (String id : ids)`  
`        {`  
`           System.out.println(id);`  
`        }`  
`     } catch (Exception e){`  
`        e.printStackTrace();`  
`     }`  
`  }`

} ```

Running this code will provide you with a list of PDB that have been
cited in the same article as
<i>[1HIV](http://www.rcsb.org/pdb/explore/literature.do?structureId=1HIV)</i>:

    1A3C
    1A6Q
    1A7J
    1AAC
    1AC5
    1AH7
    1AK1
    1AKO
    1AMJ
    1BTL
    1HIV
    2LZM
    1A2P
    1GVP
    1BAZ
    1CLL
    1EER
    3PVI
    5PTI

For more examples see the "demos" subdirectory in SVN.

### Source Code

Developer access to the module is available via here:

`svn co svn+ssh://dev.open-bio.org/home/svn-repositories/biojava/biojava-live/branches/modules/biojava-biolit/trunk biojava-biolit`

Anonymous access is via here:

`svn co `[`svn://code.open-bio.org/biojava/biojava-live/branches/modules/biojava-biolit/trunk`](svn://code.open-bio.org/biojava/biojava-live/branches/modules/biojava-biolit/trunk)` biojava-biolit`
