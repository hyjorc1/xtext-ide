# Boa's XText-based IDE #

This is Boa's XText-based IDE, which is a plugin for Eclipse.


## Pre-requisites ##

**INSTALL XTEXT FIRST!** XText is required to compile the IDE.  You can
download it here:

[http://www.eclipse.org/Xtext/download.html](http://www.eclipse.org/Xtext/download.html)

Currently tested with this version:
Xtext Complete SDK	2.8.4.v201508050135	org.eclipse.xtext.sdk.feature.group

After checking out this project, make sure you run setup.sh to create some
necessary (empty) directories!  Otherwise Eclipse will refuse to build the
projects.


## Project Organization ##

This repository contains 4 Eclipse projects:

* edu.iastate.cs.boa
* edu.iastate.cs.boa.sdk
* edu.iastate.cs.boa.tests
* edu.iastate.cs.boa.ui

Each project contains a 'src' sub-dir, which contains files you **can** modify
and src-gen, xtend-gen sub-dirs that you **should not** modify (they are
generated)!

Important files:

* edu.iastate.cs.boa - /src/edu/iastate/cs/boa/Boa.xtext (the grammar file)
* edu.iastate.cs.boa - /src/edu/iastate/cs/boa/GenerateBoa.mwe2 (the modeling engine workflow file)
* edu.iastate.cs.boa.ui - /lib/boa-compiler.jar (the boa language compiler)

If you modify the input grammar (Boa.xtext) or modeling engine workflow file
(GenerateBoa.mwe2) you must rebuild! 

The corresponding compiler (boa-compiler.jar) must be updated for modifying the input grammar.


## Re-generating Files ##

Open the GenerateBoa.mwe2 file and Run As -> MWE2 Workflow.  This can require a
lot of memory/time!


## Running the IDE ##

Once you have all files built, you can run the custom IDE:

* Right-click on the 'edu.iastate.cs.boa' or 'edu.iastate.cs.boa.ui' project
	* Run-As
		* Eclipse Application

Note that anytime you make changes to source, you have to restart the custom
IDE.


## Debugging the IDE ##

Since the IDE is just Java code, you can also choose to debug it.

* Right-click on the 'edu.iastate.cs.boa' or 'edu.iastate.cs.boa.ui' project
	* Debug-As
		* Eclipse Application

This will launch the IDE in a separate Eclipse instance.  You can use the
original instance to debug it, by setting breakpoints, pausing it, etc just as
you would any other Java application.


## Exporting ##

Before exporting: 
1. Make sure to bump the version in *both* manifest files and the feature.xml file.
1. In the Category.xml, select the boa category => delete the previous feature 
=> add Feature (locate the .sdk and add it)

In order to properly export the IDE to an Eclipse update site, you need to have
Eclipse PDE installed:

Eclipse Plug-in Development Environment	3.11.0.v20150603-2000	org.eclipse.pde.feature.group

Then follow these steps:

1. select the edu.iastate.cs.boa.sdk project
1. choose File -> Export
1. choose 'Deployable features'
1. select the www directory
1. make sure 'Package as individual JAR archives' is checked
1. make sure 'Generate p2 repository' is checked
1. 'Categorize repository' with a path selecting .sdk/category.xml
1. hit Finish

After this, the www directory contains the exported project.  You need to
update a few files manually:

1. edit www/site.xml to bump the version
1. replace www/category.xml with .sdk/category.xml

Then git add/commit/push all changed files in the www directory, and git pull
the updates to the webserver.
