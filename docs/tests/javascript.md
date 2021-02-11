---
layout: page
title:  Javascript
categories: javascript jest
permalink: /tests/javascript
parent: Test Instrumentation
---

# Installation

## Jest Instrumentation

If you have not installed `dd-trace` yet you need to do it first:

```bash
yarn add --dev dd-trace
```

You need to configure a custom [testEnvironment](https://jestjs.io/docs/en/configuration#testenvironment-string) in your `jest.config.js` or however you are configuring [jest](https://jestjs.io/docs/en/configuration):

{% highlight javascript %}
// jest.config.js
module.exports = {
  // ...
  testEnvironment: '<rootDir>/testEnvironment.js', // refers to the file below
  // ...
}
{% endhighlight %}

And in `testEnvironment.js` in your repository's root folder:
{% highlight javascript %}
require('dd-trace').init()
// it can also be jest-environment-jsdom
module.exports = require('jest-environment-node') 
{% endhighlight %}

## Mocha instrumentation

If you have not installed `dd-trace` yet you need to do it first:

```bash
yarn add --dev dd-trace
```

To instrument your mocha tests, add `--require dd-trace/init` however you normally run them, e.g. update your `package.json`:

{% highlight javascript %}
// package.json
'scripts': {
  'test': 'mocha --require dd-trace/init'
},
{% endhighlight %}


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