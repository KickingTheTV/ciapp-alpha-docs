---
layout: home
title: Home
permalink: /
nav_order: 1
---

# Tracing CI/CD with Datadog
{: .fs-9 }

You can start tracing your development workflow since a commit is pushed to your repository until the build is ready to be deployed.
{: .fs-6 .fw-300 }

---

## Tracing your builds

You will obtain different insights about your build in the `Build Pipelines` and `Build Executions` sections under the CI menu in Datadog once your CI provider has been instrumented.

Some of those insights are:
* Status of the last build.
* Average, P95 and last build duration.
* Finished builds per hour.
* Failure rate of a certain build.
* Stage breakdown.

You can find an example of these build insights [here](https://app.datadoghq.com/ci/build-pipeline-dashboard/DataDog%2Flogs-backend?env=prod&service=gitlab-ci&branch=prod&repoUrl=https%3A%2F%2Fgitlab.ddbuild.io%2FDataDog%2Flogs-backend.git) for one repository that is currently reporting to Datadog.

## Tracing your tests

You will obtain different insights about your tests in the `Test Plans` and `Test Executions` sections under the CI menu in Datadog once your tests had been instrumented.

Some of those insights for a certain commit are:
* Test statuses.
* Total number of executed tests.
* Failure rate.
* Wall time clock duration for the test phase.
* Avg delta duration change between commits.

You can find an example of these test insights [here](https://app.datadoghq.com/ci/test-dashboard/logs-backend-tests?env=ci&branch=prod&repoUrl=https%3A%2F%2Fgitlab.ddbuild.io%2FDataDog%2Flogs-backend.git) for one repository that is currently reporting to Datadog.

## Contact

We love your feedback! 

Do not hesitate to contact us on the [#ci-app](https://dd.slack.com/archives/C016LJLRZQ9) Slack channel if you have some questions or suggestions. 
 
