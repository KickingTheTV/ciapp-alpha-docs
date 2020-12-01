---
layout: page
title:  Python
categories: python pytest
permalink: /tests/python
parent: Test Instrumentation
---

# Installation

Follow the official installation [guide](https://docs.datadoghq.com/tracing/setup_overview/setup/python/) for `dd-trace-py`.

## Pytest Instrumentation

The pytest integration traces test executions.

### Enabling

Enable traced execution of tests using ``pytest`` runner by
running ``pytest --ddtrace`` or by modifying any configuration
file read by pytest (``pytest.ini``, ``setup.cfg``, ...).

{% highlight ini %}
[pytest]
ddtrace = 1
{% endhighlight %}

### Global Configuration

* `ddtrace.config.pytest["service"]`: The service name reported by default for pytest traces.
   This option can also be set with the ``DD_PYTEST_SERVICE`` environment
   variable. Default: ``"pytest"``

* `ddtrace.config.pytest["operation_name"]`: The operation name reported by default for pytest traces.
   This option can also be set with the ``DD_PYTEST_OPERATION_NAME`` environment
   variable. Default: ``"pytest.test"``


## Datadog Agent

The [Datadog Agent](https://docs.datadoghq.com/agent/) needs to be accessible by the environment you're using to run your tests on.


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
