---
layout: page
title:  Using a SaaS CI provider
categories: tests saas
permalink: /tests/saas-ci
parent: Test Instrumentation
nav_order: 1
---

# Running tests in a SaaS CI provider

In order to report test traces that run in SaaS-based CI providers, the Datadog Agent is required, configured with the following settings:

```
DD_INSIDE_CI=true
DD_HOSTNAME=none
```

Where:
* `DD_INSIDE_CI=true` will disable reporting host-level infrastructure metrics, and will enable APM listening in non-local traffic if no custom `datadog.yaml` configuration file is provided
(equivalent to `DD_APM_ENABLED=true` and `DD_APM_NON_LOCAL_TRAFFIC=true`)
* `DD_HOSTNAME=none` will disable attaching host information to tests, and will avoid APM per-host billing for test data.

**Note:** this is configuration is currently required for the alpha version, and might change in the future.


## Running the agent using Docker Compose

Independently of the CI provider used, if tests are run using [Docker Compose](https://docs.docker.com/compose/), the agent can be run as one service:

```yaml
# docker-compose.yml
version: '3'
services:
  datadog-agent:
    image: "datadog/agent:latest"
    environment:
      - DD_API_KEY
      - DD_HOSTNAME=none
      - DD_INSIDE_CI=true
    ports:
      - 8126/tcp

  tests:
    build: .
    environment:
      - DD_AGENT_HOST=datadog-agent
```

Another option is to share the same network namespace between the Datadog agent container and the tests container:

```yaml
# docker-compose.yml
version: '3'
services:
  datadog-agent:
    image: "datadog/agent:latest"
    environment:
      - DD_API_KEY
      - DD_HOSTNAME=none
      - DD_INSIDE_CI=true

  tests:
    build: .
    network_mode: "service:datadog-agent"
```

Then, you can run your tests by providing your [Datadog API key](https://app.datadoghq.com/account/settings#api) in the `DD_API_KEY` environment variable:

```sh
DD_API_KEY=xxxx docker-compose up --build --abort-on-container-exit tests
```


## CI provider specific instructions

The following sections provide CI provider-specific instructions to run and configure the Datadog agent to report test information.


### Azure Pipelines

In order to run the Datadog Agent in [Azure Pipelines](https://azure.microsoft.com/en-us/services/devops/pipelines/), the agent container has to be defined under the [`resources` section](https://docs.microsoft.com/en-us/azure/devops/pipelines/process/resources?view=azure-devops&tabs=schema) and linked with the job declaring it as a [`service` container](https://docs.microsoft.com/en-us/azure/devops/pipelines/process/service-containers?view=azure-devops&tabs=yaml):

```yaml
# azure-pipeline.yml
variables:
  ddApiKey: $(DD_API_KEY)

resources:
  containers:
    - container: dd_agent
      image: datadog/agent:latest
      ports:
        - 8126:8126
        env:
          DD_API_KEY: $(ddApiKey)
          DD_HOSTNAME: "none"
          DD_INSIDE_CI: "true"

jobs:	
  - job: test
    services:
      dd_agent: dd_agent
    steps:
      - script: make test
```

Then, add your [Datadog API key](https://app.datadoghq.com/account/settings#api) to your [project environment variables](https://docs.microsoft.com/en-us/azure/devops/pipelines/process/variables?view=azure-devops&tabs=yaml%2Cbatch) with the key `DD_API_KEY`.


### GitLab CI

In order to run the Datadog Agent in [GitLab.com](https://gitlab.com/), the agent container has to be defined under [`services`](https://docs.gitlab.com/ee/ci/docker/using_docker_images.html#what-is-a-service):

```yaml
# .gitlab-ci.yml
variables:
  DD_AGENT_HOST: "dd_agent"
  DD_HOSTNAME: "none"
  DD_INSIDE_CI: "true"

test:
  services:
    - name: datadog/agent:latest
      alias: dd_agent
  script:
    - make test
```

Then, add your [Datadog API key](https://app.datadoghq.com/account/settings#api) to your [project environment variables](https://docs.gitlab.com/ee/ci/variables/README.html#custom-environment-variables) with the key `DD_API_KEY`.



### GitHub Actions

In order to run the Datadog Agent in [GitHub Actions](https://docs.github.com/en/actions), the agent container has to be defined under [`services`](https://docs.github.com/en/actions/guides/about-service-containers):

{% raw %}
```yaml
jobs:
  test:
    services:
      datadog-agent:
        image: datadog/agent:latest
        ports:
          - 8126:8126
        env:
          DD_API_KEY: ${{ secrets.DD_API_KEY }}
          DD_HOSTNAME: "none"
          DD_INSIDE_CI: "true"
    steps:
      - run: make test
```
{% endraw %}

Then, add your [Datadog API key](https://app.datadoghq.com/account/settings#api) to your [project secrets](https://docs.github.com/en/actions/reference/encrypted-secrets) with the key `DD_API_KEY`.
