---
layout: page
title:  Java Test Instrumentation
categories: java test
permalink: /java
---

# Installation

## Maven

Add a new Maven profile in your root `pom.xml` configuring the Datadog Java agent dependency and the `javaagent` arg property, replacing `0.68.0` with the latest version of the agent: 

{% highlight xml %}
<profile>
  <id>ci-app</id>
  <activation>
    <activeByDefault>false</activeByDefault>
  </activation>

  <properties>
    <dd.java.agent.arg>-javaagent:${settings.localRepository}/com/datadoghq/dd-java-agent/0.68.0/dd-java-agent-0.68.0.jar</dd.java.agent.arg>
  </properties>

  <dependencies>
    <dependency>
        <groupId>com.datadoghq</groupId>
        <artifactId>dd-java-agent</artifactId>
        <version>0.68.0</version>
        <scope>provided</scope>
    </dependency>  
  </dependencies> 
</profile>
{% endhighlight %}

### Instrumenting your tests

Configure the [`Maven Surefire Plugin`](https://maven.apache.org/surefire/maven-surefire-plugin/) and/or the [`Maven Failsafe Plugin`](https://maven.apache.org/surefire/maven-failsafe-plugin/) to use Datadog Java agent:

{% highlight xml %}
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-surefire-plugin</artifactId>
  <configuration>
    <argLine>${dd.java.agent.arg}</argLine>
  </configuration>
</plugin>

<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-failsafe-plugin</artifactId>
  <configuration>
     <argLine>${dd.java.agent.arg}</argLine>
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

After this, you can run your tests using the `ci-app` profile, for example using the `mvn clean verify -Pci-app` command.

## Gradle

Add the `ddJavaAgent` entry to the `configurations` task block and add the Datadog Java agent dependency, replacing `0.68.0` with the latest version of the agent.

{% highlight groovy %}
configurations {
    ddJavaAgent
}

dependencies {
    ddJavaAgent "com.datadoghq:dd-java-agent:0.68.0"
}
{% endhighlight %}

### Instrumenting your tests

Configure the `test` Gradle task by adding to the `jvmArgs` attribute the `-javaagent` argument targeting the Datadog Java agent based on the `configurations.ddJavaAgent` property.

{% highlight groovy %}
test {
    jvmArgs = ["-javaagent:${configurations.ddJavaAgent.asPath}"]
}
{% endhighlight %}

After this, you can run your tests as you normally do, for example using the `./gradlew cleanTest test --rerun-tasks` command.

## Enabling

All configuration options below have system property and environment variable equivalents. If the same key type is set for both, the system property configuration takes priority. System properties can be set as JVM flags.

| SYSTEM PROPERTY                 | ENVIRONMENT VARIABLE            | DEFAULT | DESCRIPTION                                             |
|---------------------------------|---------------------------------|---------|---------------------------------------------------------|
| `dd.integration.junit.enabled`  | `DD_INTEGRATION_JUNIT_ENABLED`  | `false` | When `true`, tests based on JUnit runners are reported. |
| `dd.integration.testng.enabled` | `DD_INTEGRATION_TESTNG_ENABLED` | `false` | When `true`, tests based on TestNG are reported.        |

Additionally, all [Datadog Tracer configuration](https://docs.datadoghq.com/tracing/setup_overview/setup/java/?tab=containers#configuration) options can be used to during test phase.

### Recommended configuration

To improve the Datadog Java agent startup, follow the next recommended configuration:

| SYSTEM PROPERTY                | ENVIRONMENT VARIABLE           | DEFAULT            | RECOMMENDATION                                                         |
|--------------------------------|--------------------------------|--------------------|------------------------------------------------------------------------|
| `dd.service`                   | `DD_SERVICE`                   | `unnamed-java-app` | The name of the Test Plan that will appear in the CI/CD Test Plan tab. |
| `dd.agent.host`                | `DD_AGENT_HOST`                | `localhost`        | Make sure this property targets the Datadog Agent host.                |
| `dd.trace.agent.port`          | `DD_TRACE_AGENT_PORT`          | `8126`             | Make sure this property targets the Datadog Agent port.                |
| `dd.integrations.enabled`      | `DD_INTEGRATIONS_ENABLED`      | `true`             | `false`                                                                |
| `dd.integration.junit.enabled` | `DD_INTEGRATION_JUNIT_ENABLED` | `false`            | `true`                                                                 |
| `dd.jmxfetch.enabled`          | `DD_JMXFETCH_ENABLED`          | `true`             | `false`                                                                |

You can change the test integration from `JUnit` to `TestNG` modifying the correspondent option.

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
* BuildKite
* CircleCI
* Github Actions
* Gitlab
* Jenkins
* TravisCI

# Troubleshooting

## I don't see my tests in Datadog after installing the Datadog Java agent

If you don't see any results in Datadog after following the [Java Test Instrumentation guide](#installation), check the following:

**Have you started a Datadog Agent instance?**

The Datadog Java agent needs a [Datadog Agent](https://docs.datadoghq.com/agent/) instance running and accessible from the environment where the tests are being executed to send the traces to Datadog.

Additionally, `DD_AGENT_HOST` and `DD_TRACE_AGENT_PORT` options need to be configured properly in case the default values (`localhost`,`8126`) are not correct.  

**Have you forwarded the required environment variables?**

If you are executing your tests in a container, you need to forward several environment variables depending on your CI provider.

You can find further information in [Running tests inside a container](common/tests_in_container) section.