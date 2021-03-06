Metadata_Injection
==================

A Java program to embed BAM/PFA cataloging data into image files, written by Andrew Chang of BAM/PFA. This program originally extracted cataloging data from the museum's FileMaker database. It has been adapted to use data extracted from CollectionSpace, as part of the migration of the collection management system from FileMaker to CollectionSpace. It has also been converted to use maven for build management (instead of using unscripted Eclipse builds), and the onejar maven plugin for dependency bundling (instead of Eclipse's jarinjarloader).

The program requires two libraries that do not appear to be available from any public maven repository:

- jai_core: http://download.java.net/media/jai/builds/release/1_1_3/jai-1_1_3-lib.zip
- moss-image: http://moss.digitalcave.ca/nightlies/moss-image-2.1.0.0.zip

After downloading, the jar files for these libraries may be installed to the local maven repository, using these commands:

	mvn install:install-file -Dfile=jai_core.jar -DgroupId=javax.media -DartifactId=jai_core -Dversion=1.1.3 -Dpackaging=jar -DgeneratePom=true
	mvn install:install-file -Dfile=moss-image-2.1.0.0.jar -DgroupId=ca.digitalcave.moss -DartifactId=moss-image -Dversion=2.1.0.0 -Dpackaging=jar -DgeneratePom=true

To build:

	mvn clean install
	
This produces two jar files:

	InjectMetaDataBAMCollection-[version].jar
	InjectMetaDataCDArchive-[version].jar
	
The jar files are identical, except for having different main classes. All dependencies are bundled in the jars.

Usage:

	java -jar target/InjectMetaDataCDArchive-[version].jar [path to image archive directory]
	java -jar target/InjectMetaDataBAMCollection-[version].jar [path to image directory]