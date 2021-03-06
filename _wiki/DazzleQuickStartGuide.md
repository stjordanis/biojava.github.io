---
title: DazzleQuickStartGuide
---

Steps required to set up dazzle in eclipse with already available plugins
=========================================================================

Setting up dazzle in eclipse makes it easier to debug the application if
configuration files are incorrect and makes it easy to test your das
server in an integrated environment. This step by step guide should be
usable by anyone with only a moderate knowledge of java and web
development. It describes how to set up a basic dazzle instance with the
default plugins available and test datasets included in the application.

Download container (apache tomcat 5.5.27)
-----------------------------------------

Go to <http://tomcat.apache.org/download-55.cgi> and download tomcat by
clicking on a link under the core catagory - windows installer if you
are using windows or a tar.gz if you are using linux or macOSX

Download EasyEclipse (EasyEclipse server java version which has Web tools already).
-----------------------------------------------------------------------------------

Go to <http://www.easyeclipse.org/site/distributions/server-java.html>
and select the download for your type of operating system e.g. windows
or mac

Set up a server configuration in eclipse
----------------------------------------

-   right click on the servers tab at the bottom of eclipse.
-   click new, server.
-   browse to the tomcat 5.5.27 dir and select. then select the jvm1.60
    from the dropdown menu below.

next, next, ok.

Get project from the latest source in subversion
------------------------------------------------

-   choose import, other, checkout projects from svn.
-   click next (create new repository location).
-   type in "<http://www.derkholm.net/svn/repos/dazzle/>"
-   next
-   select the trunk directory
-   next
-   leave the default "check out the project using the New Project
    Wizard"
-   click "finish"
-   open web dir then select dynamic web project
-   type in the name of your project as "das"
-   click finish
-   click ok if eclipse talks about standard resources

Your das project should now be in eclipse.

-   right click on the project in the eclipse explorer window and select
    "build path" then "configure build path","add jars" then open the
    project in the popup that appears and a jars dir should be visible,
    then select all the jar files, then ok.

(newer features require java 5.0 so we need to make sure the project is
configured to use java 5.0 as standard). rigt click on the project and
select properties then the J2EE tab, then select the jar files as before
to be added to the project.

-   go to project properties again and select the java build path,
    source tab- then click "add resources" tick the resources folder and
    ok.

Configure using dazzle.xml
--------------------------

-   drag the web.xml file from the dazzle-webapp dir to the
    webcontent/web-inf dir
-   then drag all the other files from that dir into the webcontent dir
    above the web-inf dir!!!(currently these files include files such as
    das.xsl, dazzlecfg.xml, example.up, fickett-tss.gff, sources.xml,
    test.embl, test.style, tss.style, wellcome.html).
-   now go to the dazzlecfg.xml file that you just moved into the
    webcontent folder and alter the "value" next to filename for all
    occurances and put a / in front e.g. change "test.embl" to
    "/test.embl"

Run using eclipse
-----------------

-   Right click on the project in the window on the left and select "run
    as" then "run on server", "finish". Another window should appear
    with the url <http://localhost:8080/das/> at the top and a list of
    das sources.

Alternatively:

-   Right click on the "tomcat 5.5..." server in the servers tab in the
    bottom window of eclipse and choose start.
-   If you navigate to <http://localhost:8080/TutorialDazzleTest/> in a
    internet browser you should now see a list of das sources!!!???

<!-- -->

-   now type into the browser the url
    <http://localhost:8080/TutorialDazzleTest/dsn>
-   right click on the web page and select "view page source" this will
    open a file containing the raw xml that is being returned from your
    dazzle server.

Deploy using eclipse
--------------------

-   Right click on the project in the left hand window and select
    "export","web","WAR file","next", browse to a folder where you want
    to put the war file, click "save" and then "finish". You can now
    move this .war file into the webapp directory of any java compliant
    webapp container such as tomcat or resin).

