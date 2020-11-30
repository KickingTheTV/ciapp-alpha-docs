---
layout: page
title:  Jenkins
categories: ci jenkins
permalink: /ciprovider/jenkins
parent: Build Instrumentation
---

# Installation

Follow the official installation [guide](https://github.com/jenkinsci/datadog-plugin/blob/master/README.md).

To enable the APM traces collection for Jenkins builds and pipelines:

* Installed the Jenkins plugin v2.1.1+ (available in the Jenkins marketplace).
* Configure the Jenkins plugin to use the `Datadog Agent` mode.

APM Traces feature is only available if the `Datadog Agent` mode is selected.

## Enabling

Traces collection UI configuration is hidden for the general public. 

To enable this feature, you need to activate it manually following the next steps:

*  Open a Terminal in the Jenkins instance
*  Navigate to `$JENKINS_HOME` folder
*  Open `org.datadog.jenkins.plugins.datadog.DatadogGlobalConfiguration.xml` file
*  Add or modify the following XML nodes:
{% highlight xml %}
  <reportWith>DSD</reportWith>
  <targetApiKey>*******</targetApiKey>
  <targetHost>(use your datadog agent host)</targetHost>
  <targetPort>8125</targetPort>
  <targetLogCollectionPort>8125</targetLogCollectionPort>
  <targetTraceCollectionPort>8126</targetTraceCollectionPort>
  <traceServiceName>my-jenkins-instance</traceServiceName>
  <collectBuildTraces>true</collectBuildTraces>
{% endhighlight %}
*  Save and close.
*  Restart Jenkins.

If everything has been well configured, you should be able to see the following lines in the Jenkins log after restarting it:

{% highlight txt %}
INFO    datadog.trace.core.CoreTracer#<init>: New instance: DDTracer-62fcf62{ ... }
INFO    datadog.trace.core.StatusLogger#logStatus: DATADOG TRACER CONFIGURATION { ... }
{% endhighlight %}

Now you can use your Jenkins as you normally do.

## Datadog Agent

The [Datadog Agent](https://docs.datadoghq.com/agent/) needs to be accessible by the Jenkins instance you are using.
