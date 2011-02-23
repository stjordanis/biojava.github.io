---
title: BioJava:CookBook3:NCBIQBlastService
---

How can I use NCBI's QBlast to do my alignments remotely?
---------------------------------------------------------

BioJava now has some ability to use remote bioinformatics services to
execute tasks on servers and fetch the results for further use. The
first example of this new ability is the capacity to perform Blast
analysis via the QBlast service at NCBI. Not strictly speaking a web
service in the true sense of the word, QBlast takes specially formatted
HTTP requests to execute Blast searches on NCBI servers.

The QBlast BioJava classes implement a serie of interfaces:
RemotePairwiseAlignmentService, RemotePairwiseAlignmentProperties and
RemotePairwiseAlignmentOutputProperties. These interfaces are designed
in such a fashion that setting the parameters for alignement, submitting
the results and fetching the results in a desired format are done
independently from each other. This allows a program to send a bunch of
requests, grab the requests ID and fetch the results at a later time.

To use QBlast, you use a NCBIQBlastService object (which implements
RemotePairwiseAlignmentService) to manage the connection to the QBlast
service, submission of requests and fetching of results. To do so, it
needs a sequence (represented by either a string or a Sequence object;
search by GID will be added in a future release) and a
NCBIQBlastAlignmentProperties object. Submitting a Sequence object is
the preferred method since it allows for some basic sanity checks
related to the sequence type-to-program selection. The
NCBIQBlastAlignmentProperties class implements
RemotePairwiseAlignmentProperties and it is use to set which program and
which database to use for the analysis. Right now, it can't much make
use of other parameters of the QBlast service but the methods are in
development to fix this situation. One would recover results using the
same NCBIQBlastService object, which hold submission information, and an
object of type NCBIQBlastOutputProperties to specify the informations to
recover and the format to present to the submitter.

Using the interfaces found in package org.biojava3.ws.alignment should
allow extensions to other remote alignment services like FASTA and Blast
at EBI, which use more classic web services.

**WARNING (as of early February 2011):**

- You need to use the latest biojava-live tree to have this example
working.

- Only blastall programs are implemented right now: blastn,
blastp,blastx,tblastn,tblastx. MegaBlast and phi-blast are high in the
TO DO list. However, as QBlast is implemented right now, it might not be
possible to create a way of doing psi-blast analysis.

- Basic sanity checks are in place so that you won't try to use blastn
on a ProteinSequence object...

- Get and Set methods now exists to manipulate expect values and word
sizes. (Note: this is done as of 21 feb 2011; available via
biojava-live)

- Do not use multiple threads to send loads of requests to NCBI. This
would only get you into trouble, up to getting you blacklisted by NCBI.

<java>

import java.io.BufferedReader; import java.io.File; import
java.io.IOException; import java.io.InputStream; import
java.io.InputStreamReader; import java.util.ArrayList; import
java.util.LinkedHashMap; import java.util.Map.Entry;

import org.biojava3.core.sequence.ProteinSequence; import
org.biojava3.core.sequence.io.FastaReaderHelper; import
org.biojava3.ws.alignment.qblast.NCBIQBlastService; import
org.biojava3.ws.alignment.qblast.NCBIQBlastAlignmentProperties; import
org.biojava3.ws.alignment.qblast.NCBIQBlastOutputProperties; import
org.biojava3.ws.alignment.qblast.NCBIQBlastOutputFormat;

public class NCBIQBlastServiceTest {

`   /**`  
`    * The program take only a string with a path toward a sequence file`  
`    * `  
`    * For this example, I keep it simple with a single FASTA formatted file`  
`    * `  
`    */`  
`   public static void main(String[] args) {`  
  
`       NCBIQBlastService rbw;`  
`             NCBIQBlastAlignmentProperties rqb;`  
`             NCBIQBlastOutputProperties rof;`  
`       InputStream is;`  
`       ArrayList`<String>` rid = new ArrayList`<String>`();`  
`       String request = "";`  
  
`       try {`

`           // Let's capture the sequences in a file...`  
`           LinkedHashMap`<String, ProteinSequence>` a = FastaReaderHelper.readFastaProteinSequence(new File(args[0]));`  
`                       `  
`           /*`  
`            * You would imagine that one would blast a bunch of sequences of`  
`            * identical nature with identical parameters...`  
`            */`  
`           rbw = new NCBIQBlastService();`  
`           rqb = new NCBIQBlastAlignmentProperties();`

`           rqb.setBlastProgram("blastp");`  
`           rqb.setBlastDatabase("nr");`  
`                       `  
`           /*`  
`            * First, let's send all the sequences to the QBlast service and`  
`            * keep the RID for fetching the results at some later moments`  
`            * (actually, in a few seconds :-))`  
`            *`  
`            * Using a data structure to keep track of all request IDs is a good`  
`            * practice.`  
`            *`  
`            */`  
`           for (Entry`<String, ProteinSequence>` entry : a.entrySet()) {`  
`               System.out.println( entry.getValue().getOriginalHeader() + "\n");`  
`                               String s = entry.getValue().toString();`  
`               request = rbw.sendAlignmentRequest(s,rqb);`  
`               rid.add(request);`  
`           }`

`           /*`  
`            * Let's check that our requests have been processed. If completed,`  
`            * let's look at the alignments with my own selection of output and`  
`            * alignment formats.`  
`            */`  
`           for (String aRid : rid) {`  
`               System.out.println("trying to get BLAST results for RID "`  
`                       + aRid);`  
`               boolean wasBlasted = false;`  
  
`               while (!wasBlasted) {`  
`                   wasBlasted = rbw.isReady(aRid, System.currentTimeMillis());`  
`               }`  
  
`               rof = new NCBIQBlastOutputProperties();`  
`               rof.setOutputFormat(NCBIQBlastOutputFormat.TEXT);`  
`               rof.setAlignmentOutputFormat(NCBIQBlastOutputFormat.PAIRWISE);`  
`               rof.setDescriptionNumber(10);`  
`               rof.setAlignmentNumber(10);`  
  
`               /*`  
`                * Simply to show you that your output options were followed`  
`                * `  
`                */ `  
`               is = rbw.getAlignmentResults(request, rof);`  
  
`               BufferedReader br = new BufferedReader(`  
`                       new InputStreamReader(is));`  
  
`               String line = null;`  
  
`               while ((line = br.readLine()) != null) {`  
`                   System.out.println(line);`  
`               }`  
`           }`  
`       }`  
`       /*`  
`        * What happens if the file can't be read`  
`        */`  
`       catch (IOException ioe) {`  
`           ioe.printStackTrace();`  
`       }`  
`       /*`  
`        * What happens if FastaReaderHelper hits a snag`  
`        */`  
`       catch (Exception bio) {`  
`           bio.printStackTrace();`  
`       }`  
`   }`

} </java>