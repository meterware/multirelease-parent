This POM simplifies the creation of multi-release jars. 

## Setup

Make this your parent POM:

```
    <parent>
        <groupId>com.meterware</groupId>
        <artifactId>multirelease-parent</artifactId>
        <version>1.0</version>
    </parent>
```

You must have a `toolchains.xml` defined in your maven configuration directory (`~/.m2/toolchains.xml` on OS X and Linux)

Code for the main jar (JDK 1.7-1.8) goes under `src/main/java` as usual. 

Code additions for later JDKs, along with `module-info.jar` go under `src/main/java9`, `src/main/java10` or `src/main/java11`

## Unit Testing

`mvn clean test` will use the current JDK (the one running Maven)to run unit tests, 
including the appropriate additional directories.

## Building the MR JAR

`mvn -Dmulti_release clean install` will create the multi-release JAR, using toolchains to select the appropriate
compiler for each jar.  This will automatically happen when using the release plugin.

## Notes:

This parent POM inherits from `org.sonatype.oss:oss-parent:9` and brings with it all associated definitions.

By default, builds with this parent will use JDK 1.7 to build the main jar. You can change that by adding

```
<base.java.version>1.8</base.java.version>
```

to your `<properties>` section.
