---
title: "How to setup an IDE"
---

[Deutsche Übersetzung](/de/project_info/howto_regain_in_an_ide/)

How to setup an IDE
===================

In any case, you need to install the JDK first: [Download](http://java.sun.com/javase/downloads/index.jsp).

You also should set the environment variable JAVA_HOME to the directory you installed the JDK into, e.g. `C:/Programme/Java/jdk1.6.0_12`. The variable PATH should contain the `bin`-Folder, e.g. `%PATH%;%JAVA_HOME%\bin`.

Hint: Under Windows, you can set environment variable by:
  * Hitting Windows+Pause
  * Tab "Advanced"
  * Button "Environment Variables"

netbeans
--------
  - Check out the [source code with subversion](/en/project_info/project_info/sourcecode/#check_out_sourcecode_from_the_svn_repository) into a folder of your choice. There exists several tools (RapidSVN, tortoise) or use the command line on a *nix/Cygwin.
  - Create a new project with the type 'Java Free-Form Project'

      - Choose the root of the checkout as Location
      - All other fields should be automatically filled 
      - You can map ant targets to netbeans actions
      - Set the source level to JDK 1.6
      - add the libs from 'lib/' to the 'src/src' Source Package Folder. 
      - add only the needed libs from lib/ to 'test/src'

Eclipse
-------

  - Install [Subversive](http://www.eclipse.org/subversive/downloads.php) (or another SVN client).
  - Add `https://regain.svn.sourceforge.net/svnroot/regain` as repository.
  - Check out `trunk` as Java Project.
  - Add to the Build Path the Libraries:

      - All .jar in lib/ and sub-directories.
  - Add as Source folder: `test/src`

ANT
---
  - Create an adapted version of `build.properties` in the project root folder. Use  `build.properties.sample` as a blueprint.

Build Process
-------------
  - run the target **clean-all** first
  - run the target **runtime** which will create all necessary jars
  - run the target **run-desktop-fast** to start the desktop version
  - run the target **public** on a Windows system to create the exe-installer

