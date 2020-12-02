---
layout: page
title:  .NET
categories: .net test
permalink: /tests/dotnet
parent: Test Instrumentation
---

# Installation

## Using .NET CLI global tool

Install the CLI global tool by executing:

```
dotnet tool install -g dd-trace
```

This will install the `dd-trace` command globally in the machine.

In case your have a previous version of the tool, you can update using:

```
dotnet tool update -g dd-trace
```

## Instrumenting your tests

To instrument your test suite, prefix your test command with `dd-trace`. For example:

```
dd-trace dotnet test
```

All tests will be instrumented automatically.

## CLI configuration settings

Default configuration of the CLI can be changed by using command line arguments or environment variables. For a full list of configuration settings you can execute:

```
dd-trace --help
```

The following table shows the default values for some of these configuration:


| CLI OPTION                     | ENVIRONMENT VARIABLE           | DEFAULT                 | DESCRIPTION                                                             |
|--------------------------------|--------------------------------|-------------------------|-------------------------------------------------------------------------|
| `--set-ci`                     |                                | `false`                 | Sets up the clr profiler environment variables for all the CI pipeline. |
| `--dd-env`                     | `DD_ENV`                       | `(empty)`               | Environment name for the unified service tagging.                       |
| `--dd-service`                 | `DD_SERVICE`                   | `(ProcessName)`         | Service name for the unified service tagging.                           |
| `--dd-version`                 | `DD_VERSION`                   | `(empty)`               | Version for the unified service tagging.                                |
| `--agent-url`                  | `DD_TRACE_AGENT_URL`           | `http://localhost:8126` | Datadog trace agent url.                                                |

Additionally, all [Datadog Tracer configuration](https://docs.datadoghq.com/tracing/setup_overview/setup/dotnet-core/?tab=windows#configuration) options can be used during test phase.

### Example:

Running a test suite with a custom agent url and environment name:

```
dd-trace --agent-url=http://agent:8126 --dd-env=ci dotnet test
```

## Passing parameters to the application

If the application expects command line arguments, a `--` separator should be used before the target application to avoid any parameter collision.

For example:

```
dd-trace --dd-env=ci -- dotnet test --framework netcoreapp3.1
```

This will autoinstrument the command: `dotnet test --framework netcoreapp3.1` with `ci` as environment.

## Datadog Agent 

The [Datadog Agent](https://docs.datadoghq.com/agent/) needs to be accessible by the environment you're using to run your tests on.

## Supported .NET versions

* [.NET Core 2.1+](https://dotnet.microsoft.com/download/dotnet-core/2.1)
* [.NET Core 3.0+](https://dotnet.microsoft.com/download/dotnet-core/3.0)
* [.NET 5.0+](https://dotnet.microsoft.com/download/dotnet/5.0)

## Supported Test frameworks

* [xUnit 2.2+](https://xunit.net/)
* [NUnit 3.0+](https://nunit.org/)

## Supported CI providers

* [Appveyor](https://www.appveyor.com/)
* [Azure Pipelines](https://azure.microsoft.com/en-us/services/devops/pipelines/)
* [BitBucket](https://bitbucket.org/)
* [BuildKite](https://buildkite.com/)
* [CircleCI](https://circleci.com/)
* [Github Actions](https://github.com/features/actions)
* [Gitlab](https://docs.gitlab.com/ee/ci/)
* [Jenkins](https://www.jenkins.io/)
* [TravisCI](https://travis-ci.org/)