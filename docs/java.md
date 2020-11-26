---
layout: page
title:  Java Test Instrumentation
categories: java test
permalink: /java
---

# Installation

Follow the official installation [guide](https://docs.datadoghq.com/tracing/setup_overview/setup/java/) for `dd-trace-java`.

The `-javaagent` property needs to be configured in your build framework.

**Note**: Use `dd-java-agent` combined with `dd-trace-ot` is not allowed. If you use `dd-trace-ot` in your tests, you need to adapt your code to use other Opentracing implementation: E.g. `opentracing-mock`. 

### Maven

Configure the [`Maven Surefire Plugin`](https://maven.apache.org/surefire/maven-surefire-plugin/) and/or the [`Maven Failsafe Plugin`](https://maven.apache.org/surefire/maven-failsafe-plugin/) to use Datadog Java agent:

{% highlight xml %}
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-surefire-plugin</artifactId>
  <configuration>
    <argLine>-javaagent:/path/to/the/dd-java-agent.jar</argLine>
  </configuration>
</plugin>

<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-failsafe-plugin</artifactId>
  <configuration>
     <argLine>-javaagent:/path/to/the/dd-java-agent.jar</argLine>
  </configuration>
  <executions>
      <execution>
        <goals>
           <goal>integration-test</goal>
           <goal>verify</goal>
        </goals>
      </execution>
  </executions>
</plugin>
{% endhighlight %}

After this, you can run your tests as you normally do, for example using the `mvn clean verify` command.

### Gradle

Configure the `test` Gradle task by adding to the `jvmArgs` attribute the `-javaagent` argument targeting the Datadog Java agent.

{% highlight groovy %}
test {
    jvmArgs = ["-javaagent:/path/to/the/dd-java-agent.jar"]
}
{% endhighlight %}

After this, you can run your tests as you normally do, for example using the `gradle cleanTest test --rerun-tasks` command.

## Enabling

All configuration options below have system property and environment variable equivalents. If the same key type is set for both, the system property configuration takes priority. System properties can be set as JVM flags.

| SYSTEM PROPERTY                 | ENVIRONMENT VARIABLE            | DEFAULT | DESCRIPTION                                             |
|---------------------------------|---------------------------------|---------|---------------------------------------------------------|
| `dd.integration.junit.enabled`  | `DD_INTEGRATION_JUNIT_ENABLED`  | `false` | When `true`, tests based on JUnit runners are reported. |
| `dd.integration.testng.enabled` | `DD_INTEGRATION_TESTNG_ENABLED` | `false` | When `true`, tests based on TestNG are reported.       |

## Datadog Agent 

The [Datadog Agent](https://docs.datadoghq.com/agent/) needs to be accessible by the environment you're using to run your tests on.

# Supported Test frameworks

* JUnit 4.10+
* JUnit 5.3+
* TestNG 6.4+

# Supported CI providers

* Appveyor
* Azure Pipelines
* BitBucket
* Build Kite
* Circle CI
* Github Actions
* Gitlab
* Jenkins
* Travis CI
