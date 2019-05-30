# dbuild launcher module

This project is the componetized sbt launcher.   It can be used to launch many Maven/Ivy deployed applications
and utilities, and forms the basis of [sbt](https://github.com/sbt/sbt),
[activator](https://github.com/typesafehub/activator) and [conscript](https://github.com/foundweekends/conscript)'s launching
abilities.

For the full set of documentation, read: http://www.scala-sbt.org/0.13/docs/Sbt-Launcher.html
.

This repository is a fork of the sbt launcher, with minimal customizations, for use by the
[dbuild tool](https://github.com/lightbend/dbuild) (also see
[the manual](http://lightbend.github.com/dbuild)).

This fork is active, but not supported. It is maintained by the Tooling Team at Lightbend.

## Rebundling

This project provides two modules for general use:

1. A library for interacting with Launcher features as a launched application, or for defining a launched Server.
2. A minimal JAR that can be used to lookup your application, using Ivy, and load/run it.

This minimal JAR file is designed to be:

* Less than 1MB in size
* Able to launch any application on the JVM
* Isolate classloaders and allow re-use of Scala library classloader for Scala applications.
* Rebundled as a "wrapper" or "launcher" for your specific project.

To rebundle the JAR for your project, first you'll need a launcher properties file (specified [here](http://www.scala-sbt.org/0.13/docs/Launcher-Configuration.html)).

You can test your launch configuration file by running:

```
java -jar <raw launch jar> @<my launcher properties file>
```

Once you've verified your properties file is complete you can inject your launcher properties file into the "launch jar"
as the file `sbt/sbt.boot.properties`.   The launcher will look for this file in lieu of any command-line arguments to
launch an application.


If you've not done this correctly, you will see the following:

```
$ java -jar target/sbt-launch-1.0.0-SNAPSHOT.jar
Error during sbt execution: Could not finder sbt launch configuration.  Searched classpath for:
	/sbt.boot.properties0.13.7
	/sbt/sbt.boot.properties0.13.7
	/sbt.boot.properties0.13
	/sbt/sbt.boot.properties0.13
	/sbt.boot.properties
	/sbt/sbt.boot.properties
```


Additionally, we recommend renaming your bundled launch jar for your application (e.g. activator calls theirs
"activator-launch-<version>.jar").


# License

This software is under a modified BSD license.
