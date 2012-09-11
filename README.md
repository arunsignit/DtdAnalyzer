﻿#DtdAnalyzer

##Moved!

<b><em>Note:  the development of this tool has moved to
[NCBITools/DtdAnalyzer](https://github.com/NCBITools/DtdAnalyzer).  Please update your
bookmarks.</em></b>

##Overview

This tool will create an XML representation (using elements and attributes)
of an XML DTD.

##Usage

    dtdanalyzer [options] [<output file>]

All options have a short and a long form.   At least one option must be given that specifies
the DTD that is to be processed:
* -s, --system *system-id* - Use the given system identifier to find the DTD.  This could
  be a relative pathname, if the DTD exists in a file on your system, or an HTTP URL.
* -d, --doc *xml-file* - Specify an XML file used to find the DTD.  This could be just a "stub"
  file, that contains nothing other than the doctype declaration and a root element.  This
  file doesn't need to be valid according to the DTD.
* -p, --public *public-id* - Use the given public identifier to find the DTD.  This would
  be used in conjunction with an OASIS catalog file.

Other possible options and arguments are:
* -h,--help - Print usage information and exit.
* -c, --catalog *catalog-file* - Specify a file to use as the OASIS catalog, to resolve public
  identifiers
* -x, --xslt *xslt-file* - An XSLT script to run to post-process the output.  This is optional.
* -t, --title *dtd-title* - Specify the title of this DTD.  This will be output within a &lt;title>
  element under the root &lt;declarations> element of the output XML.
* &lt;output file> - Name of the file to write the output to.  If this argument is not given,
  the output is written to standard out.

##Examples

Process the NISO JATS Journal Archiving and Interchange DTD, and write the output to a
file:

    dtdanalyzer --system http://jats.nlm.nih.gov/archiving/1.0/JATS-archivearticle1.dtd \
        JATS-archivearticle1.daz.xml


##Development environment / getting started

The development environment for this project is very rudimentary at present,
and uses make.  To use the scripts that come with the package, first set the
environment variable $DTDANALYZER_HOME to the root of the git repository.
For example (Unix):

    git clone git://github.com/Klortho/DtdAnalyzer.git
    cd DtdAnalyzer
    export DTDANALZER_HOME=`pwd`

Next, set up your environment using either the
setenv.sh or setenv.bat scripts in the scripts directory.  On Unix,

    . script/setenv.sh

On Windows,

    script\setenv

Next, you'll want to download all the dependencies into the lib directory.  This
script is only available for Unix.  On Windows, you'll have to do it manually.

    getlibs.sh

See below for a list of the dependencies.

To build the project, use make.  The Makefile targets are:

* all - default target, everything below.
* clean - deletes intermediate files
* bin - compiles all .java → .class; results go into 'class' directory
* doc - builds javadocs; puts results into 'doc'
* t - runs the script over the test file in the 'test' directory

To run, from the test directory, for example,

    dtdanalyzer --doc archiving-3.0.xml out.xml


##Dependencies

The following jar files are required.  You can use the script getlibs.sh to download and
unpack these, if you like (Unix only).

* [Apache Commons CLI](http://commons.apache.org/cli/), version 1.2
  * commons-cli-1.2.jar
* [Apache xml-commons](http://xerces.apache.org/xml-commons/) resolver, version 1.2
  * resolver.jar
* [Apache Xerces2 Java parser](http://xerces.apache.org/#xerces2-j), version 2.11.0
  * xml-apis.jar
  * xercesImpl.jar
* [Saxon Home Edition](http://saxon.sourceforge.net), version 6.5.5
  * saxon.jar

##Discussion forum / mailing list

Please join the <a href='https://groups.google.com/d/forum/dtdanalyzer'>DtdAnalyzer Google group</a>
for discussions.

##Public domain

This work is in the public domain and may be used and reproduced without special permission.
