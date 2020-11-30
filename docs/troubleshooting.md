---
layout: page
title:  Troubleshooting
categories: troubleshooting
permalink: /troubleshooting
nav_order: 5
---

# Troubleshooting

## I don't see any information in Datadog after instrumenting my platform.

If you don't see any results in Datadog after following the installation guide for your platform, check the following:

**Have you started a Datadog Agent instance?**

The Datadog Tracer may need a [Datadog Agent](https://docs.datadoghq.com/agent/) instance running and accessible from the environment where the tests are being executed.

Additionally, `DD_AGENT_HOST` and `DD_TRACE_AGENT_PORT` options need to be configured properly in case the default values (`localhost`,`8126`) are not correct.  

**Have you forwarded the required environment variables?**

If you are executing your tests in a container, you need to forward several environment variables depending on your CI provider.

You can find further information in [Running tests inside a container](/tests-in-container) section.