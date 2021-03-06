---
title: BioJava:Hackers Guide
permalink: wiki/BioJava%3AHackers_Guide
---

### A hacker's guide to BioJava

BioJava is an open-source framework developement by a worldwide group of
volunteer programmers. We're always happy to receive contributions of
new features, bug-fixes, or documentation. Before starting on any major
new features, we suggest you make contact with the [Developers' mailing
list](mailto:biojava-dev@biojava.org), which is always a good source of
advice on design, packaging, and how best to make your code interact
with the rest of BioJava.

If you're considering any development work on BioJava, we suggest you
start with an up-to-date version -- either a nightly snapshot or a copy
direct from our CVS repository. If you are contributing substantion
amounts of code, or submitting patches on a regular basis, we'll usually
give you direct write access to the CVS repository. Contact the mailing
list for more information.

### Style guide

> \* We generally aim to follow Sun's [Java Code
> Conventions](http://java.sun.com/docs/codeconv/html/CodeConvTOC.doc.html).

> \* All java files source files should contain the license header (see
> below).

> \* Place an @author tag in every file that you edit. The 'maintainer'
> (either the original author, or the person currently overseeing the
> code) should be first, and then all other authors follow. Don't be
> shy - anything from spelling corrections in the JavaDoc through to
> re-writing a whole method counts.

> \* Always indent with spaces, not tabs. Different editors expand tabs
> to different widths.

> \* Indent depths of 2 or 4 characters are acceptable -- use whichever
> you prefer when creating new files or working on a major rewrite. When
> modifying just a few lines, it's usually easier to preserve the
> existing indentation.

> \* Javadoc all interface methods fully. An interface is defined by the
> method signatures, clear documentation and a reference implementation.

> \* Javadoc class methods when they are not implementing an interface
> method. Javadoc methods that implement an interface method only if
> clarification is needed, otherwise trust the documentation
> inheritance.

> \* Methods should nearly always specify types by interface, not
> concrete implementations. This makes it easier to extend the code
> later.

> \* With every interface Foo that defines a useful object, provide an
> implementation named SimpleFoo in the same package that is a plain,
> pure-java reference version. This gives other people a clearer idea of
> what the interface is meant to encapsulate. It also often makes it
> obvious if something is missing.

### Standard source file header

`/*`  
` *                    BioJava development code`  
` *`  
` * This code may be freely distributed and modified under the`  
` * terms of the GNU Lesser General Public Licence.  This should`  
` * be distributed with the code.  If you do not have a copy,`  
` * see:`  
` *`  
` *      `[`http://www.gnu.org/copyleft/lesser.html`](http://www.gnu.org/copyleft/lesser.html)  
` *`  
` * Copyright for this code is held jointly by the individual`  
` * authors.  These should be listed in @author doc comments.`  
` *`  
` * For more information on the BioJava project and its aims,`  
` * or to join the biojava-l mailing list, visit the home page`  
` * at:`  
` *`  
` *      `[`http://www.biojava.org/`](http://www.biojava.org/)  
` *`  
` */`
