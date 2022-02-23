---
title: "Getting started"
date: 2018-09-09T12:52:46+10:00
description: GraphQL basics. Start here if you're new to GraphQL :-) 
sidebar_position: 1
---
# Getting started

`graphql-java` requires at least Java 8.


## How to use the latest release with Gradle

Make sure ``mavenCentral`` is among your repos:

```groovy
repositories {
    mavenCentral()
}
```


Dependency:

```groovy
dependencies {
  compile 'com.graphql-java:graphql-java:17.3'
}
```


## How to use the latest release with Maven

Dependency:

```xml
<dependency>
    <groupId>com.graphql-java</groupId>
    <artifactId>graphql-java</artifactId>
    <version>17.3</version>
</dependency>
```


## Hello World

This is the famous "hello world" in ``graphql-java``:

```java
import graphql.ExecutionResult;
import graphql.GraphQL;
import graphql.schema.GraphQLSchema;
import graphql.schema.StaticDataFetcher;
import graphql.schema.idl.RuntimeWiring;
import graphql.schema.idl.SchemaGenerator;
import graphql.schema.idl.SchemaParser;
import graphql.schema.idl.TypeDefinitionRegistry;

import static graphql.schema.idl.RuntimeWiring.newRuntimeWiring;

public class HelloWorld {

    public static void main(String[] args) {
        String schema = "type Query{hello: String}";

        SchemaParser schemaParser = new SchemaParser();
        TypeDefinitionRegistry typeDefinitionRegistry = schemaParser.parse(schema);

        RuntimeWiring runtimeWiring = newRuntimeWiring()
                .type("Query", builder -> builder.dataFetcher("hello", new StaticDataFetcher("world")))
                .build();

        SchemaGenerator schemaGenerator = new SchemaGenerator();
        GraphQLSchema graphQLSchema = schemaGenerator.makeExecutableSchema(typeDefinitionRegistry, runtimeWiring);

        GraphQL build = GraphQL.newGraphQL(graphQLSchema).build();
        ExecutionResult executionResult = build.execute("{hello}");

        System.out.println(executionResult.getData().toString());
        // Prints: {hello=world}
    }
}
```

## Using the latest development build
----------------------------------

The latest development build is available on Bintray.

Please look at [Latest Build](https://bintray.com/andimarek/graphql-java/graphql-java/_latestVersion>) for the
latest version value.


### How to use the latest build with Gradle

Add the repositories:

```groovy
repositories {
    mavenCentral()
    maven { url  "https://dl.bintray.com/andimarek/graphql-java" }
}
```

Dependency:

```groovy
dependencies {
  compile 'com.graphql-java:graphql-java:INSERT_LATEST_VERSION_HERE'
}
```



### How to use the latest build with Maven


Add the repository:

```xml
<repository>
    <snapshots>
        <enabled>false</enabled>
    </snapshots>
    <id>bintray-andimarek-graphql-java</id>
    <name>bintray</name>
    <url>https://dl.bintray.com/andimarek/graphql-java</url>
</repository>
```

Dependency:

```xml
<dependency>
    <groupId>com.graphql-java</groupId>
    <artifactId>graphql-java</artifactId>
    <version>INSERT_LATEST_VERSION_HERE</version>
</dependency>
```