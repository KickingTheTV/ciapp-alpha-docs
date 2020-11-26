---
layout: page
title:  Jenkins Instrumentation
categories: ci jenkins
permalink: /ciprovider/jenkins
---

# Installation

Follow the official installation [guide](https://github.com/jenkinsci/datadog-plugin/blob/master/README.md).

To enable the APM traces collection for Jenkins builds and pipelines, it's needed:

* To have installed the Jenkins plugin v2.1.1+ (Available in the Jenkins marketplace).
* To have configured the Jenkins plugin to use the `Datadog Agent` mode.

APM Traces feature is only available if the `Datadog Agent` mode is selected.

## Enabling

Traces collection UI configuration is hidden for the general public. 

To enable this feature, you need to activate it manually following the next steps:

1. Open a Terminal in the Jenkins instance
2. Navigate to `$JENKINS_HOME` folder
3. Open `org.datadog.jenkins.plugins.datadog.DatadogGlobalConfiguration.xml` file
4. Add or modify the following XML nodes (Change the port to the correspondent with the `Datadog Agent` Traces collection port):
    1. `<targetTraceCollectionPort>8126</targetTraceCollectionPort>`
    2. `<traceServiceName>my jenkins service</traceServiceName>`
    3. `<collectBuildTraces>true</collectBuildTraces>`
5. Save and close.
6. Restart Jenkins.

## Datadog Agent

The [Datadog Agent](https://docs.datadoghq.com/agent/) needs to be accessible by the Jenkins instance you are using.