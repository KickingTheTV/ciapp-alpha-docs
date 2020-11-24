---
layout: page
title:  "Javascript Tracer - Jest Instrumentation"
date:   2020-11-24 14:37:09 +0100
categories: javascript jest
---

# Javascript Tracer - Jest Instrumentation

To instrument your tests you'll need a custom [testEnvironment](https://jestjs.io/docs/en/configuration#testenvironment-string):
{% highlight javascript %}
// testEnvironment.js in your repository's root folder
const NodeEnvironment = require('jest-environment-node') // jest-environment-jsdom for ui tests
const { getEnvironment } = require('dd-trace/packages/datadog-plugin-jest/src/index')

module.exports = getEnvironment(NodeEnvironment)
{% endhighlight %}

And then in your `jest.config.js`: 

{% highlight javascript %}
module.exports = {
  // ...
  testEnvironment: '<rootDir>/testEnvironment.js',
  // ...
}
{% endhighlight %}