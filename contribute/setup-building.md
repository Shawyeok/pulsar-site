---
id: setup-building
title: Setup and building
---

## Prerequisites

| Dependency | Description                                                                                                                                                                                                         |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Git        | The source code of Pulsar is hosted on GitHub as a git repository. To work with the git repository, please [install git](https://git-scm.com/downloads). We highly recommend that you also [set up a Git mergetool](setup-git.md#mergetool) for resolving merge conflicts. |
| JDK        | The source code of Pulsar is primarily written in Java. Therefore, you need a working Java Development Kit (JDK) to build it. It recommended to use SDKMAN to install Corretto OpenJDK 21 and 17, see ["Setting up JDKs and Maven using SDKMAN"](setup-buildtools.md) for details. |
| Maven      | The source code of Pulsar is managed by [Apache Maven](https://maven.apache.org/) The recommended Maven version is 3.9.9. It is recommended to use SDKMAN to install Maven, see ["Setting up JDKs and Maven using SDKMAN"](setup-buildtools.md) for details. |
| Zip        | The build process requires Zip as a utility tool. |

:::note

On Windows, replace `./mvnw` with `mvnw.cmd` in the commands below.

:::

:::note

Pulsar does not support running server on Windows yet, you have to use Docker to run Pulsar. 
Please consider checking [Run Pulsar In Docker](https://pulsar.apache.org/docs/3.1.x/getting-started-docker/)

:::

## Clone

Clone the source code to your development machine:

```bash
git clone https://github.com/apache/pulsar
```

The following commands are assumed to be executed from the project root directory:

```bash
cd pulsar
```

## Build

Compile and install to local Maven repository:

```bash
./mvnw clean install -DskipTests
```

## Run

```bash
bin/pulsar standalone
```

## Connect

```bash
bin/pulsar-shell
```