################################################################################
## A self contained, executable, Jython Excel dohicky.
## 
## Based on the work of 
##
## By Ryan McGuire
## www.EnigmaCurry.com
## 
## and the jython wiki
##
## By JS Bruneau 
################################################################################

The only thing that this application does is spit out a silly Excel
file using the Apache POI java library. It means to be an example of
how to package your own Jython application in a manner that requires
no external dependancies other than a JVM on the host computer.

To base your own project off this example you should understand how
this package is organized:

 * /etc 
    Placeholder for config files. All files here will be copied over the /dist
	folder.
	
 * /java-lib 
    Put all of your external java libraries (.jar) here

 * /java-src
	All java source code you might need in your app. For now we have a launcher (Main.java)
	and a trust provider that disable certificate validation for SSL connections to force
	Jython's behaviour to resemble more CPython
	
 * /python-lib
	Placeholder for any pure python external libraries. They will be added to the sys.path

 * /python-src
	Your python code. When the jar gets executed, a file called entrypoint.py will be executed.
	

    This sample project has two dependancies:

      * Jython itself (jython-full.jar)
      * Apache POI for the excel capabilities (poi-3.5-beta5-20090219.jar). 
        Obviously if your project doesn't work with excel files, you'd delete this file from 
		your project.
    
    Since this is a Jython project, the jython jar is required in this
    directory. For most applications, you will want a "full" or self
    contained Jython .jar which contains the entire Jython /Lib
    directory inside. This jar should be called jython-full.jar to
    differentiate it from the one that the regular Jython installer builds.

    See the Jython build instructions below for more details.


Building the app:

    You need Apache Ant installed. It should be sufficient to just 
    run 'ant' in the same directory as build.xml
    
    Ant should create a new jar file called dist/JythonExcelExample.jar
    which you can then run:

        java -jar dist/JythonExcelExample.jar


Building Jython:
  
    Jython is already included in this distribution, but when new
    versions of Jython come out, you may wish to upgrade. These are
    the instructions you'll need for modifying the Jython jar that the
    Jython installer builds so that it will work in a One-Jar
    environment:

    * Download the latest Jython installer (right now it's 2.5rc2) :

        wget http://downloads.sourceforge.net/jython/jython_installer-2.5rc2.jar

    * Extract the installer, there's no need to run it:
        
	mkdir jython-exploded
	cd jython-exploded
	unzip ../jython_installer-2.5rc2.jar

    * Add the Lib/ folder to a new jython jar:
        
	cp jython.jar jython-full.jar
	zip -r jython-full.jar Lib/

    * jython-full.jar is now a complete Jython install in a single jar
      file.
      
      Should be about 11MB. Simply place it at the root of your project or edit 
	  the build.xml accordingly.

    
