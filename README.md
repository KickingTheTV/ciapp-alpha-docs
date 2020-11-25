# CI App alpha docs

[See the docs online](https://datadoghq.dev/ciapp-alpha-docs/).

## How to add documentation

* Clone the repository
```
git clone git@github.com:DataDog/ci-app-alpha-docs.git
```
* Change to the docs folder
```
cd ci-app-alpha-docs/docs
```
* Create your markdown file
```
touch java.md
```
* Add the metadata on top of the file (see [javascript.md](/docs/javascript.md) for an example):
```
---
layout: page
title:  Java Tracer - Test Instrumentation
permalink: /java
---
```
* Add your instructions to the file.
* Push your code to the `main` branch or create a pull request.

## How to add syntax highlighted code

You can add syntax highlighted code through this tag:
```
{% highlight javascript %}
...
{% endhighlight %}
```

See [javascript.md](/docs/javascript.md) for an example.
