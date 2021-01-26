---
layout: page
title: Custom Instrumentation
categories: ci cli custom
permalink: /ciprovider/datadog-ci
parent: Pipeline Instrumentation
nav_order: 10
---

You can get deeper insights into your pipeline by using the [`datadog-ci`](https://github.com/DataDog/datadog-ci) CLI to wrap your CI commands: 

```bash
$ datadog-ci trace command yarn test
$ datadog-ci trace command mkdir artifacts
```

Whatever command comes after `datadog-ci trace command` will be executed as is. A span that represents the executed command will be created.

## Supported CIs

You may use `datadog-ci trace command` in any CI, but the created span will only be a part of a pipeline trace in the following supported CIs:

- Jenkins. [Datadog Jenkins Plugin](https://docs.datadoghq.com/integrations/jenkins/) v2.4.0 or higher needs to be installed.

## How to install the CLI

The package is under [@datadog/datadog-ci](https://www.npmjs.com/package/@datadog/datadog-ci) and can be installed through NPM or Yarn:

```sh
# NPM
npm install -g @datadog/datadog-ci

# Yarn
yarn global add @datadog/datadog-ci
```

**Note**: The example shows a global installation, but it can also be local, depending on your setup.

## Example

Your `Jenkinsfile` might look like this:

```
pipeline {
    agent any
    stages {
        stage('Hello World') {
            steps {
                sh 'datadog-ci echo "Hello World"'
            }
        }
    }
}
```

Or if you're using GitHub Actions (note that traces will not be continued in this case):

```yml
name: Continuous Integration

on: push

jobs:
  build-and-test:
    name: Build and test
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - name: Install node
        uses: actions/setup-node@v1
        with:
          node-version: '12.x'
      - run: yarn global add @datadog/datadog-ci
      - run: datadog-ci yarn install
      - run: datadog-ci yarn build
      - run: datadog-ci yarn lint
      - run: datadog-ci yarn test
```

## Requirements
* `node>=12`
