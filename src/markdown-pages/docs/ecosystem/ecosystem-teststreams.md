---
path: "/docs/ecosystem/ecosystem-teststreams"
title: "Configuring test streams"
---


Galasa's Ecosystem organises tests into _streams_. A stream is a group of tests that you want to run in automation represented by a single OBR (OSGi Bundle Repository) and its equivalent test catalog. Test streams provide flexibility when it comes to organising test projects, deciding how often they are built, and choosing where they are deployed. You can have as few or as many test streams as you want.


Define these terms ... test ...

package
stream
catalog (and overall catalog)
    The catalog stores related tests within a shared test catalog, enabling tests to be automatically selected to run for any given change set. The test catalog uses the latest version of test cases, so you know the tests that you're running are up-to-date.
portfolio
bundle
class
case

inc which ones runs prepare / submit cmds are applicable to
and also where you are going to need your auth token

Galasa locates your tests along with all of the Managers that a test project requires, by using information contained in the OBR file. 


```
galasactl project create \
        --package dev.galasa.example.banking \
      	--features payee,account \
   		--force \
		--obr \
		--log - \
		--maven \
		--gradle
```

- ```--obr``` Creates an OBR project. For tests to run in the Ecosystem they require compiled artifacts to be hosted in a Maven repository. The artifacts must be bundled as an OSGI bundle. 

```
galasactl runs submit local --log - \
--obr mvn:dev.galasa.example.banking/dev.galasa.example.banking.obr/0.0.1-SNAPSHOT/obr \
--class dev.galasa.example.banking.account/dev.galasa.example.banking.account.TestAccount
```


- `--obr` specifies where the  CLI tool can find an OBR which refers to the bundle where the tests are stored. When running locally, all tests must exist in the OBR (or OBRs) that are passed to the tool. The `--obr` parameter specifies the Maven co-ordinates of the obr jar file, in the format `mvn:groupId/artifactId/version/classifier`.

- ```--obr``` Creates an OBR project. An OBR (OSGi Bundle Repository) is an index of OSGi bundles. Galasa testcases are built into OSGi bundles which are then connected into an OBR. When you specify the location of the OBR to Galasa, the OBR tells Galasa where the tests are stored. You can create an OBR from scratch, or you can create projects and add them into an existing OBR. For more information about OBRs, see the <a href="https://felix.apache.org/documentation/subprojects/apache-felix-osgi-bundle-repository.html" target="_blank"> Apache Felix</a> website.


## About test catalogs 

A test catalog is automatically created by running the `galasactl project create` command. A test catalog is used specify which tests to run in automation. 

## About test streams

A test stream is made of the following components:

- name
- description
- obr
- location
- repo


The `obr` field contains a URL that references the location of the built using to a list of Maven coordinates in the format `mvn:{grp}/{artifact id}/{version}/{obr}`. The `location` field contains a URL that references the location of the test catalog in the format `http://../testcatalog`, and the `repo` field references the Maven repository

The location of the test catalog and the OBR file are held on the Maven repository in URL format, for example, `/../../dev.galasa.example.banking.obr-0.0.1-SNAPSHOT.obr` and `/../../dev.galasa.example.banking.obr-0.0.1-SNAPSHOT-testcatalog.json`.

For example, in dev.galasa.example.banking, you have the following in the OBR project (dev.galasa.example.banking.obr) in the `0.0.1-SNAPSHOT` folder:

```
dev.galasa.example.banking.obr-0.0.1-SNAPSHOT-testcatalog.json
dev.galasa.example.banking.obr-0.0.1-SNAPSHOT.obr
dev.galasa.example.banking.obr-0.0.1-SNAPSHOT.pom
```


## Retrieving test stream information

You can run the following command ...

```
>galasactl properties get --namespace framework --name test.streams
namespace name         value
framework test.streams inttests,cip,simbank,resourcebuilder,pong,zosk8s,galasa-vtp-demo

Total:1
```

## Creating a test stream on an Ecosystem

A Galasa Ecosystem adminstrator can create test streams in the `framework` namespace on an Ecosystem by using the `galasactl properties set` command. 

You must provide the namespace of `framework`, the name of the stream, the location of the test catalog in url format, a list of maven coordinates, and the name of the Maven repository in the command in the following example format:

```
galasactl properties set --namespace framework --name test.stream.mystream.description --value "My stream to use as an example"
galasactl properties set --namespace framework --name test.stream.mystream.repo --value http://points-to-my-maven-repo
galasactl properties set --namespace framework --name test.stream.mystream.location --value http://points-to-my-test-catalog
galasactl properties set --namespace framework --name test.stream.mystream.obr --value mvn:myorg/myartifact/0.0.1/obr
```

where: 

 - `namespace` is the namespace in which the property is stored - for test streams this must be the framework namespace
 - `name` is the name of the stream that you want to create 
 - `location` is the url that points to the location of the test catalog in the Maven repository
 - `obr` is the url that points to the list of Maven coordinates in the Maven repository
 - `repo` is the name of the Maven repository
 - `description` is a description of the purpose of the stream

Alternatively, you can use a resource file to set up the test stream using the following command:

```
galasactl resources apply -f myteststream.yaml
```

where:

- `myteststream.yaml` is a resource file containing the property definitions of the test stream

If you upgrade to a new version of Galasa, you can update the URLs that contain the version numbers by using the `galasctl properties` set command. Alternatively, you can set the URLs to point to `0.0.1-SNAPSHOT` so that the stream always points to the latest version.



The following diagram shows the architecture for the authentication process:

![Galasa ecosystem architecture:](ecosystem-cluster-auth.svg)


## Creating OSGi bundle repositories and test catalogs using Gradle

OSGI bundle repositories contain all the project information, configuration details and dependencies that are needed for building and running Galasa projects. Test catalogs are used to manage Galasa test cases. Attributes that are associated with test cases that are held in the test catalog are used to schedule test runs.

The OBR plugin in the [Gradle repository] enables you to build OSGi Bundle Repositories using Gradle.

Complete the following steps to use the Gradle OBR plugin in a Gradle test project:

1. Add the `galasa.tests` plugin to your `build.gradle` file by adding the following lines in each of your testcase projects:
```
plugins {
    ...
    id 'java' 
    id 'maven-publish'
    id 'dev.galasa.tests' version '0.33.0'
    ...
}
```
The `java` plugin builds the testcase code, the `maven-publish` plugin pushes the built artifacts to a Maven repository, and the `dev.galasa.tests` plugin builds a test catalog. This test catalog is later added to an overall test catalog which can be then published to an Ecosystem.
1. Create a `build.gradle` file in your project's OBR directory with the following contents:
```
plugins {
    ...
    id 'dev.galasa.obr' version '0.33.0'
    id 'dev.galasa.testcatalog' version '0.33.0'
    ...
}

repositories {
    mavenLocal()
    mavenCentral()
    maven {
        url = 'https://development.galasa.dev/prod/maven-repo/obr'
    }
}

// Here, all OSGi Bundles to be included in the OBR must be listed using the 'bundle' configuration
dependencies {
    bundle project(':com.example.tests.manager')
    bundle project(':com.example.tests.mytests')
}
```
This content applies the OBR plugin to the OBR subproject and specifies the bundles to be included in the OBR that will be built. It also defines the repositories that Gradle will search within to resolve dependencies and applies the java plugin to enable Java compilation, testing, and build features.

Declare the obr file as an artifact, and add it to the list of artifacts which get published for the OBR project.
```
def obrFile = file('build/galasa.obr')
artifacts {
    archives obrFile
}

// Tell gradle to publish the built OBR as a maven artifact on the 
// local maven repository.
publishing {
    publications {
        maven(MavenPublication) {
            artifact obrFile
        }
    }
}
```
1. Create a `settings.gradle` file in your project's root directory with the following contents:
```
pluginManagement {
    repositories {
        mavenLocal()
        mavenCentral()
        maven {
            url = "https://development.galasa.dev/prod/maven-repo/obr"
        }
        gradlePluginPortal()
    }
}

include 'com.example.tests.obr' // This must match the name of your OBR subproject.
```
This content defines the repositories that Gradle will search to find requested plugins. It also includes the OBR subproject in Gradle builds.

If you would like to give your OBR subproject a different name, you can create a `settings.gradle` file in your OBR directory containing the following line:
```
rootProject.name='obrProjectName'
```
If you do this, ensure that the `include` statement in your root project's `settings.gradle` file matches the name given to your OBR subproject.
1. Verify that the OBR was successfully built by checking that you have a `gradle build` directory in your OBR directory, and that the `gradle build` directory contains a `galasa.obr` file.
1. Publish artifacts to the local Maven repository by running the following command:
```
gradle clean build publishToMavenLocal
```
The built artifacts are published to the local Maven folders on the build machine.
1. Deploy the test catalog to the Galasa Ecosystem by running the `galasactl properties set` command to set the `location` field of your test stream to refer directly to the URL of the location of the test catalog in your Maven repository.

To build the plugin locally, use the `.build-locally.sh` script to invoke a build.


## Creating OSGi bundle repositories and test catalogs using Maven

OSGI bundle repositories contain all the project information, configuration details and dependencies that are needed for building and running Galasa projects. Test catalogs are used to manage Galasa test cases. Attributes that are associated with test cases that are held in the test catalog are used to schedule test runs.

The OBR plugin in the [Maven repository] enables you to build OSGi Bundle Repositories using Maven.

Complete the following steps to use the Maven OBR plugin in a Maven test project:

1. Build a test catalog for a Java bundle by adding the following . This goal creates a test catalog for all the tests in the child bundles of the Maven project:
```
<plugin>
    <groupId>dev.galasa</groupId>
    <artifactId>galasa-maven-plugin</artifactId>
    <extensions>true</extensions>
    <executions>
        <execution>
        <id>build-testcatalog</id>
        <phase>package</phase>
        <goals>
            <goal>bundletestcat</goal>
        </goals>
        </execution>
    </executions>
</plugin>
```

To build the plugin locally, use the `.build-locally.sh` script to invoke a build.