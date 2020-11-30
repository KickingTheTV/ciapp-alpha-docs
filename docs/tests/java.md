---
layout: page
title:  Java
categories: java test
permalink: /tests/java
parent: Test Instrumentation
---

# Installation

# Using Maven

Add a new Maven profile in your root `pom.xml` configuring the Datadog Java tracer dependency and the `javaagent` arg property, replacing `0.68.0` with the latest version of the tracer: 

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

## Instrumenting your tests

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

# Using Gradle

Add the `ddTracerAgent` entry to the `configurations` task block and add the Datadog Java tracer dependency, replacing `0.68.0` with the latest version of the tracer.

{% highlight groovy %}
configurations {
    ddTracerAgent
}

dependencies {
    ddTracerAgent "com.datadoghq:dd-java-agent:0.68.0"
}
{% endhighlight %}

## Instrumenting your tests

Configure the `test` Gradle task by adding to the `jvmArgs` attribute the `-javaagent` argument targeting the Datadog Java tracer based on the `configurations.ddTracerAgent` property.

{% highlight groovy %}
test {
    jvmArgs = ["-javaagent:${configurations.ddTracerAgent.asPath}"]
}
{% endhighlight %}

After this, you can run your tests as you normally do, for example using the `./gradlew cleanTest test --rerun-tasks` command.

# Enabling

All configuration options below have system property and environment variable equivalents. If the same key type is set for both, the system property configuration takes priority. System properties can be set as JVM flags.

| SYSTEM PROPERTY                 | ENVIRONMENT VARIABLE            | DEFAULT | DESCRIPTION                                             |
|---------------------------------|---------------------------------|---------|---------------------------------------------------------|
| `dd.integration.junit.enabled`  | `DD_INTEGRATION_JUNIT_ENABLED`  | `false` | When `true`, tests based on JUnit runners are reported. |
| `dd.integration.testng.enabled` | `DD_INTEGRATION_TESTNG_ENABLED` | `false` | When `true`, tests based on TestNG are reported.        |

Additionally, all [Datadog Tracer configuration](https://docs.datadoghq.com/tracing/setup_overview/setup/java/?tab=containers#configuration) options can be used to during test phase.

## Recommended configuration

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

* [JUnit 4.10+](https://junit.org/junit4/)
* [JUnit 5.3+](https://junit.org/junit5/)
* [TestNG 6.4+](https://testng.org/doc/)

Additionally, we support the test frameworks which are based on JUnit, such as [Spock Framework](http://spockframework.org/), [Cucumber-Junit](https://cucumber.io/docs/cucumber/api/), etc

# Supported CI providers

* [Appveyor](https://www.appveyor.com/)
* [Azure Pipelines](https://azure.microsoft.com/en-us/services/devops/pipelines/)
* [BitBucket](https://bitbucket.org/)
* [BuildKite](https://buildkite.com/)
* [CircleCI](https://circleci.com/)
* [Github Actions](https://github.com/features/actions)
* [Gitlab](https://docs.gitlab.com/ee/ci/)
* [Jenkins](https://www.jenkins.io/)
* [TravisCI](https://travis-ci.org/)