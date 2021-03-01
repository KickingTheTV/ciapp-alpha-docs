---
layout: page
title:  Ruby
categories: ruby rspec cucumber
permalink: /tests/ruby
parent: Test Instrumentation
---

# Installation

Follow the official installation [guide](https://docs.datadoghq.com/tracing/setup_overview/setup/ruby/) for `dd-trace-rb`.


## Cucumber Instrumentation

Cucumber integration will trace all executions of scenarios and steps when using `cucumber` framework.

To activate your integration, use the `Datadog.configure` method:

{% highlight ruby %}
require 'cucumber'
require 'ddtrace'

# Configure default Cucumber integration
Datadog.configure do |c|
  c.use :cucumber, options
end

# Example of how to attach tags from scenario to active span
Around do |scenario, block|
  active_span = Datadog.configuration[:cucumber][:tracer].active_span
  unless active_span.nil?
    scenario.tags.filter { |tag| tag.include? ':' }.each do |tag|
      active_span.set_tag(*tag.name.split(':', 2))
    end
  end
  block.call
end
{% endhighlight %}

Where `options` is an optional `Hash` that accepts the following parameters:

| Key | Description | Default |
| --- | ----------- | ------- |
| `enabled` | Defines whether Cucumber tests should be traced. Useful for temporarily disabling tracing. `true` or `false` | `true` |
| `service_name` | Service name used for `cucumber` instrumentation. | `'cucumber'` |
| `operation_name` | Operation name used for `cucumber` instrumentation. Useful if you want rename automatic trace metrics e.g. `trace.#{operation_name}.errors`. | `'cucumber.test'` |


The lastest documentation can be found [here](https://github.com/DataDog/dd-trace-rb/blob/master/docs/GettingStarted.md#cucumber).


## RSpec Instrumentation

RSpec integration will trace all executions of example groups and examples when using `rspec` test framework.

To activate your integration, use the `Datadog.configure` method. You can add this to the `spec_helper.rb`

{% highlight ruby %}
require 'rspec'
require 'ddtrace'

# Configure default RSpec integration
Datadog.configure do |c|
  c.use :rspec, options
  c.tracer writer_options: { buffer_size: 5000, flush_interval: 0.5 }
end
{% endhighlight %}

If you have many fast unit tests, you will need to tweak flushing settings. You can enable `health_metrics` to tweak the numbers. This will send a metric called `datadog.tracer.queue.dropped.traces`

{% highlight ruby %}
Datadog.configure do |c|
  c.use :rspec, options
  c.diagnostics.health_metrics.enabled = true
end
{% endhighlight %}

Where `options` is an optional `Hash` that accepts the following parameters:

| Key | Description | Default |
| --- | ----------- | ------- |
| `enabled` | Defines whether RSpec tests should be traced. Useful for temporarily disabling tracing. `true` or `false` | `true` |
| `service_name` | Service name used for `rspec` instrumentation. | `'rspec'` |
| `operation_name` | Operation name used for `rspec` instrumentation. Useful if you want rename automatic trace metrics e.g. `trace.#{operation_name}.errors`. | `'rspec.example'` |

The lastest documentation can be found [here](https://github.com/DataDog/dd-trace-rb/blob/master/docs/GettingStarted.md#rspec).

## Datadog Agent

The [Datadog Agent](https://docs.datadoghq.com/agent/) needs to be accessible by the environment you're using to run your tests on.


## Supported CI providers

* [Appveyor](https://www.appveyor.com/)
* [Azure Pipelines](https://azure.microsoft.com/en-us/services/devops/pipelines/)
* [BitBucket](https://bitbucket.org/)
* [BuildKite](https://buildkite.com/)
* [CircleCI](https://circleci.com/)
* [GitHub Actions](https://github.com/features/actions)
* [GitLab](https://docs.gitlab.com/ee/ci/)
* [Jenkins](https://www.jenkins.io/)
* [TravisCI](https://travis-ci.org/)
