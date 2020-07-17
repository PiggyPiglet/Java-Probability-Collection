# Java-Probability-Collection
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/lewysDavies/Java-Probability-Collection/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/lewysDavies/Java-Probability-Collection/?branch=master) [![Build Status](https://scrutinizer-ci.com/g/lewysDavies/Java-Probability-Collection/badges/build.png?b=master)](https://scrutinizer-ci.com/g/lewysDavies/Java-Probability-Collection/build-status/master) [![](https://jitpack.io/v/lewysDavies/Java-Probability-Collection.svg)](https://jitpack.io/#lewysDavies/Java-Probability-Collection)<br>
Generic and Highly Optimised Java Data-Structure for Retrieving Random Elements with Probability

# Usage
```
ProbabilityCollection<String> collection = new ProbabilityCollection<>();
collection.add("A", 50); // 50 / 85 (total probability) = 0.588 * 100 = 58.8% Chance
collection.add("B", 25); // 25 / 85 (total probability) = 0.294 * 100 = 29.4% Chance
collection.add("C", 10); // 10 / 85 (total probability) = 0.117 * 100 = 11.7% Chance

String random = collection.get();
```

# Proven Probability
The probability test is run **1,000,000 times**. Each time getting **100,000** random elements and counting the spread. The test would not pass if the spread had over **1%** deviation from the expected probability.

A real world example is provided in ExampleApp.java (within the test folder), Typical Output with 100,000 gets::
```
   Prob     |  Actual
-----------------------
A: 58.824%  |  58.975% 
B: 29.412%  |  29.256% 
C: 11.765%  |  11.769% 
```

# Performance
Get performance has been significantly improved in comparison to my previous map implementation. This has been achieved with custom compared TreeSets.
```
Benchmark                                 Mode  Cnt      Score     Error  Units
BenchmarkProbability.collectionAddSingle  avgt    5    501.688 ±  33.925  ns/op
BenchmarkProbability.collectionGet        avgt    5     69.373 ±   2.198  ns/op
BenchmarkProbability.mapAddSingle         avgt    5  25809.712 ± 984.980  ns/op
BenchmarkProbability.mapGet               avgt    5    902.414 ±  22.388  ns/op
```

# Installation
**Super Simple: Copy ProbabilityCollection.java into your project**<br><br>
or for the fancy users, you could use Maven:<br>
**Repository:**
```
<repository>
    <id>jitpack.io</id>
    <url>https://jitpack.io</url>
</repository>
```
**Dependency:**
```
<dependency>
    <groupId>com.github.lewysDavies</groupId>
    <artifactId>Java-Probability-Collection</artifactId>
    <version>v0.8</version>
</dependency>
```
**Maven Shade This Dependency:**
```
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-shade-plugin</artifactId>
  <version>3.1.1</version>
  <executions>
    <execution>
      <configuration>
        <relocations>
           <relocation>
              <!-- Avoid Name Conflics -->
              <pattern>com.lewdev.probabilitylib</pattern>
              <shadedPattern>***<!--YOUR.PACKAGE.HERE-->***.probabilitylib</shadedPattern>
            </relocation>
          </relocations>
       </configuration>
     <phase>package</phase>
     <goals>
       <goal>shade</goal>
     </goals>
   </execution>
  </executions>
</plugin>
```
