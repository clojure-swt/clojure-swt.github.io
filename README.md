# Eclipse SWT for Maven and Clojure

Originally from https://github.com/maven-eclipse/maven-eclipse.github.io

## This Git repo contains:

1.  A Maven repo containing SWT 4.2 to 4.31 on all supported platforms along with scripts to scrape/merge new releases as they are published at Eclipse.
2.  A (WIP) Clojure deps.edn project with a functional-style SWT DSL/wrapper that makes working with SWT user interfaces straightforward from Clojure

## Why?

Clojure needs a mature UI library with idiomatic FP-style bindings.  SWT is one such UI library; this project aims to supply the bindings.

More generally:

SWT is not available in Maven Central making it difficult to use in Maven and/or Clojure projects. Existing Maven repos are either not maintained and abandoned, don't have all platforms, don't contain sources, don't contain the debug jar, or don't provide a reliable, automatic way to update or reproduce the repository.  

This standard Maven repo is generated by a script that automatically downloads and repackages the official SWT releases.

For more information see this [project's parent fork](https://github.com/maven-eclipse/maven-eclipse.github.io/).

## Prerequisites

*  Maven
*  `aria2`.  On Ubuntu, `sudo apt install aria2`

# How to use

## Scrape new SWT versions

> Note: If you were using [swt-repo on Google Code](http://code.google.com/p/swt-repo/) to maintain a SWT repo, this is a drop in replacement.

More specifically:

```bash
$ ./scrape-check.sh
# stuff scrolls by...

$ ./scrape-swt.sh
# more stuff scrolls by...

$ git add . && git commit -m "your commit message"
```

## Clojure

tbd.

## Maven

Add this to your pom.xml: (Gradle, Ivy, and other builders users: The information is the same)

> Adjust the path below to match your project checkout location:

```
<repositories>
	<repository>
		<id>maven-eclipse-repo</id>
		<url>file://home/djo/code/maven-eclipse.github.io/maven</url>
	</repository>
</repositories>
```

Then add dependencies for each platform you wish to support. The most common are

```
<dependencies>
	<dependency>
		<groupId>org.eclipse.swt</groupId>
		<artifactId>org.eclipse.swt.win32.win32.x86</artifactId>
		<version>${swt.version}</version>
		<!-- To use the debug jar if available, add this -->
		<classifier>debug</classifier>
	</dependency>
	<dependency>
		<groupId>org.eclipse.swt</groupId>
		<artifactId>org.eclipse.swt.win32.win32.x86_64</artifactId>
		<version>${swt.version}</version>
	</dependency>
	<dependency>
		<groupId>org.eclipse.swt</groupId>
		<artifactId>org.eclipse.swt.gtk.linux.x86</artifactId>
		<version>${swt.version}</version>
	</dependency>
	<dependency>
		<groupId>org.eclipse.swt</groupId>
		<artifactId>org.eclipse.swt.gtk.linux.x86_64</artifactId>
		<version>${swt.version}</version>
	</dependency>
	<dependency>
		<groupId>org.eclipse.swt</groupId>
		<artifactId>org.eclipse.swt.cocoa.macosx.x86_64</artifactId>
		<version>${swt.version}</version>
	</dependency>
</dependencies>
```
