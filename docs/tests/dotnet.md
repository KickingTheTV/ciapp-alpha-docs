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


## Datadog Agent 

The [Datadog Agent](https://docs.datadoghq.com/agent/) needs to be accessible by the environment you're using to run your tests on.

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