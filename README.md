# TAROT2020: Installation Instructions

This tutorial is based on the QRS19 tutorial on [T6: Coverage-Based Automated Testing and Debugging](https://qrs19.techconf.org/tutorials/t6). There are two options: you either run the Eclipse IDE or the maven.

## Setup 

GZoltar requires `Java 8`, other versions will not work. Make sure that your project is using `Java 8` in the command line as well as in the Eclipse plugin. If version 8 is not your default one, you can run the following command (macOS):

```
export JAVA_HOME=`/usr/libexec/java_home -v 1.8`
```

The following tutorial has been tested using the Eclipse IDE for developers, *Version: 2019-06 (4.12.0)*.

## GZoltar for Eclipse (aka Crowbar)

GZoltar's internals depend on:

* Boost 1.70.0
* MPFR 4.0.2
* GMP 6.1.2_2

On OSX, you can install the dependencies by running the following command:

```
brew install boost mpfr gmp
```

To install the plugin itself, go to `Install New Software...` in the `Help` menu and use the link `http://www.gzoltar.com/plugin/eclipse/`. 

Once installed, you can enable the Crowbar Diagnostic Reports on `Window --> Show View --> Ohter --> Crowbar Views`. 

More information can be found at this [link](http://www.gzoltar.com/eclipse-plugin.html). 

## GZoltar for Maven

GZoltar is offered as a plugin for maven too. To set things up see the following [link](https://github.com/GZoltar/gzoltar/tree/master/com.gzoltar.maven). Once ready, run the following command in the command line:

```
mvn clean gzoltar:prepare-agent test gzoltar:fl-report
```

## Buggy Program

We have prepared a buggy program (available in this repository) for you to diagnose. 

Star by either importing the program to eclipse or by inspect the `pom.xml` to see the changes to include gzoltar. 

If using maven, type `mvn clean gzoltar:prepare-agent test gzoltar:fl-report` to run the tests using GZoltar. All results will be stored in a folder called `site`. 

## Also: DDU Metric

Install the DDU metric following the instructions in this [link](https://github.com/aperez/ddu-maven-plugin). Apply it. Improve the diagnostic report too. 

# Dockerized Maven

There is a dockerized version of gzoltar running on maven available on Docker hub. Run the following commands to get it up and running:

```
docker pull gzoltar/gzoltar_ddu
docker run --name gzoltar2 -p 8080:80 -d gzoltar/gzoltar_ddu
docker start gzoltar2
```

Once the service has started, go to [http://localhost:8080](http://localhost:8080) to access the reports. 


Once done, run the following commands:

```
docker stop gzoltar2
docker rm gzoltar2
```

You can also login into the container, and check things up there (e.g., try to fix the fault):

```
docker run -it gzoltar /bin/bash
```
