---
layout: page
title:  GitLab CI
categories: ci gitlab
permalink: /ciprovider/gitlab
parent: Pipeline Instrumentation
---

To enable traces for your Gitlab CI pipelines you need to configure the following webhooks in your GitLab site or repository:
- Job Events
- Pipeline Events

![Webhooks Screenshot](/ciapp-alpha-docs/assets/gitlab-webhooks.png)

Use this URL `https://webhooks-http-intake.logs.datadoghq.com/v1/input/(api-key)`
and if you do not have an API key you can create one [here](https://app.datadoghq.com/account/settings#api)

_Optionally_, you can pass these query parameters in the URL:
- __env__: Sets the environment at Datadog for traces for this GitLab instance. Empty by default, but you can set this if your organization has more than one infra for GitLab.
- __service__: Sets the service name for traces for this GitLab instance. Defaults to `gitlab-ci`. Again, you might want to set this in case you have more than one GitLab instance.

The webhook configuration can be done at a global level for all your GitLab projects, or specifically for some.

## Coming soon

A [native integration](https://gitlab.com/gitlab-org/gitlab/-/merge_requests/46564) has been merged into GitLab and will be available soon.
Reach out to PMs if you want to early-adopt this integration instead, but you will need a very recent version of GitLab.
