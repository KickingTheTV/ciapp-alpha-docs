---
layout: page
title:  Javascript
categories: javascript jest
permalink: /tests/javascript
parent: Test Instrumentation
---

# Installation

## Jest Instrumentation

The Datadog Javascript Tracer now exports a function `getEnvironment` to wrap your [testEnvironment](https://jestjs.io/docs/en/configuration#testenvironment-string):

{% highlight javascript %}
// testEnvironment.js in your repository's root folder
const { getEnvironment } = require('dd-trace/packages/datadog-plugin-jest/src/index')

// it can be jest-environment-jsdom for ui tests or any other environment you use
const JestEnvironment = require('jest-environment-node') 

module.exports = getEnvironment(JestEnvironment)
{% endhighlight %}


Then you need to configure `testEnvironment` in your `jest.config.js` or however you normally configure [jest](https://jestjs.io/docs/en/configuration):

{% highlight javascript %}
module.exports = {
  // ...
  testEnvironment: '<rootDir>/testEnvironment.js', // refers to the file above
  // ...
}
{% endhighlight %}

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