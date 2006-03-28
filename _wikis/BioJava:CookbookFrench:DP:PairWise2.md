---
title: BioJava:CookbookFrench:DP:PairWise2
---

Comment faire pour créer un alignement global (algorithme de Needleman-Wunsh) ou local (algorithme de Smith-Waterman)
---------------------------------------------------------------------------------------------------------------------

Les alignements de deux séquences ont traditionnellement été obtenues
par des approches de programmation dynamique déterministique. Deux
algorithmes de cette nature sont utilisés: l'algorithme de Needleman and
Wunsch est utilisé pour des alignements globaux alors que l'algorithme
de Smith-Waterman a été développé pour les alignements locaux. L'exemple
ci-dessous vous montre comment faire l'un ou l'autre grâce aux
implémentations de chacun de ces algorithmes retrouvées dans le package
alignment. Ces classe ne sont pas disponibles dans la version 1.4; vous
les retrouverez dans la version biojava-live disponible sur le [serveur
CVS](http://cvs.biojava.org). Évidemment, ils se retrouveront dans la
version 1.5 ;-)

L'idée derrière ces approches est de maintenir un représentation
matricielle d'un graphe d'éedition, avec des fonctions d'insertion, de
délétion, de substitution et d'extension de gap; en pratique,
l'insertion et la délétion sont des opérations d'ouverture de gaps au
sein de la séquence connue de l'un, de la séquence inconnue de l'autre).
Par programmation dynamique, les éléments contenus dans la matrice, qui
sont des valeurs représentant la valeur de l'opération à effectuer, sont
calculés. Le parcours permettant d'obtenir le meilleur score produit le
meilleur alignement. Les alignements utilisant des valeurs différentes
pour la valeur et la pénalité d'une ouverture et son élongation
consument une plus grande quantité de mémoire et de temps par rapport à
des valeurs identiques pour les deux.

Il est possible d'utiliser des matrices de substitution pour faire la
calcul des alignements; elles permettent de calculer la valeur de
transition d'un acide aminé à un autre. Plusieurs de ces matrices
existent et sont disponibles publiquement. Elles peuvent être
téléchargées à partir du
[NCBI](ftp://ftp.ncbi.nlm.nih.gov/blast/matrices/) et sont nécessaires
pour cet exemple.

Une démo des classes d'alignement global et local
-------------------------------------------------

<java> import java.io.File;

import org.biojava.bio.alignment.NeedlemanWunsch; import
org.biojava.bio.alignment.SequenceAlignment; import
org.biojava.bio.alignment.SmithWaterman; import
org.biojava.bio.alignment.SubstitutionMatrix; import
org.biojava.bio.seq.DNATools; import org.biojava.bio.seq.Sequence;
import org.biojava.bio.symbol.AlphabetManager; import
org.biojava.bio.symbol.FiniteAlphabet;

/\*

`* Created on Mar 28, 2006`  
`*/`

/\*\* Demo effectuant l'alignement global et local, successivement,

` * de deux sequences avec affichage des resultats a l'ecran. `  
` * L'usage d'une matrice de substitution est necessaire, facilement obtenues via`  
` * at @link `[`ftp://ftp.ncbi.nlm.nih.gov/blast/matrices/`](ftp://ftp.ncbi.nlm.nih.gov/blast/matrices/)  
` * Cette demo ne fonctionne qu'avec des sequences d'ADN. Cependant, les algorithmes fonctionnent `  
` * avec n'importe quel Alphabet pourvu qu'une matrice valable existe `  
` * Dans cet exemple, la matrice NUC.4.4 est correcte.`  
` *`  
` * @author Andreas Dräger`  
` */`

public class DeterministicAlignmentDemo {

` /** Cette classe permet l'alignement de deux sequences `  
`   * pour affichage a l'ecran.`  
`   * @param args: une sequnece inconnue et une sequence connue, `  
`   *   un fichier avec lea valeurs de la matrice de subsitution a utiliser.`  
`   * @link `[`ftp://ftp.ncbi.nlm.nih.gov/blast/matrices/`](ftp://ftp.ncbi.nlm.nih.gov/blast/matrices/)  
`   */`  
` public static void main (String args[]) {`  
`   if (args.length < 3)`  
`     throw new Error("Usage: DeterministicAlignmentDemo " +`  
`                     "querySeq targetSeq substitutionMatrixFile");`  
`   try {`  
`     // Specification de l'Alphabet des sequences, DNA dans cet exemple.`  
`     // Pour des sequences proteiques, simplement utiliser`  
`     // AlphabetManager.alphabetForName("Protein");`  
`     FiniteAlphabet alphabet = (FiniteAlphabet) AlphabetManager.alphabetForName("DNA");`  
`     `  
`     // Lecture du fichier de la matrice de substitution. `  
`     // Pour cet exemple, la matrice NUC.4.4 est correcte.`  
`     SubstitutionMatrix matrix = new SubstitutionMatrix(alphabet, new File(args[2]));`  
`     `  
`     // Definition des valeurs par defaut pour l'alignement global.`  
`     SequenceAlignment aligner = new NeedlemanWunsch( `  
`       alphabet, `  
`       2,      // insertion`  
`       2,  // deletion`  
`       1,      // gapExtend`  
`       0,  // match`  
`       3,  // remplacement`  
`       matrix  // Matrice de substitution`  
`     );`

`     Sequence query  = DNATools.createDNASequence(args[0], "query");`  
`     Sequence target = DNATools.createDNASequence(args[1], "target");`

`     // Faire l'alignement et perserver les resultats.`  
`     aligner.pairwiseAlignment(`  
`       // sources`  
`       query, `  
`       // sequenceDB`  
`       target`  
`     );`

`     // Imprimer l'alignement obtenu a l'ecran`  
`     System.out.println("global alignment with NeedlemanWunsch:\n"+`  
`       aligner.getAlignmentString());    `  
`     `  
`     // Effectuer l'alignement local. `  
`     // Primo, definir la valeur pour chaque operation.`  
`     aligner = new SmithWaterman(`  
`       0, // match`  
`       2, // insertion`  
`       3, // replacement `  
`       2, // deletion`  
`       1, // gapExtend`  
`       matrix); // Matrice de substitution`  
`     aligner.pairwiseAlignment(query, target);`  
`     System.out.println("\nlocal alignment with SmithWaterman:\n"+`  
`       aligner.getAlignmentString());`  
`   } catch (Exception exc) {`  
`     exc.printStackTrace();`  
`   }`  
` }`

} </java>