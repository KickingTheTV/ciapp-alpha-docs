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

Additionally, `DD_AGENT_HOST` and `DD_TRACE_AGENT_PORT` options need to be configured properly in case the Datadog Agent is not using its default url (`localhost:8126`).

Pipeline instrumentation requirements.

| Pipeline Instrumentation | Require Datadog Agent |
|:------------------------:|:---------------------:|
| GitLab                   |           N           |
| Jenkins                  |           Y           |

Test instrumentations requirements.

| Test Instrumentation | Require Datadog Agent |
|:--------------------:|:---------------------:|
| .NET                 |           Y           |
| Java                 |           Y           |
| Javascript           |           Y           |
| Python               |           Y           |
| Ruby                 |           Y           |
| Swift                |           N           |

**Have you forwarded the required environment variables?**

If you are executing your tests in a container, you need to forward several environment variables depending on your CI provider.

You can find further information in [Running tests inside a container](/ciapp-alpha-docs/tests-in-container) section.
