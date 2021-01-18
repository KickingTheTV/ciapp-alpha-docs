---
layout: page
title:  GitLab CI
categories: ci gitlab
permalink: /ciprovider/gitlab
parent: Pipeline Instrumentation
---

To enable traces for your GitLab CI pipelines a [native integration](https://gitlab.com/gitlab-org/gitlab/-/merge_requests/46564) has been merged into GitLab and is hidden under a feature flag since the release __v13.7.0__.

If you are a user of _GitLab as SaaS_ and you want to early-adopt this integration, reach out to our PMs so that it can be enabled for your accounts on both GitLab and Datadog.

If on the other hand you are managing your own GitLab installation and your version is recent enough, you can enable the feature flag yourself by pasting the following command in the Rails console: `Feature.enable(:datadog_ci_integration)`.

Once the feature is whitelisted, enabling the integration is as easy as going to the page for the Datadog integration at any level:
- On a per project basis, if you enable the integration in the settings of each project.
- Site-wide for all the projects in your GitLab installation if you enable the integration through the admin.

The integration page looks like this:

![Integration Screenshot](/ciapp-alpha-docs/assets/gitlab-integration.png)

You only need to mark it as active and paste a valid API key. If you do not have an API key you can create one [here](https://app.datadoghq.com/account/settings#api)

__Note__ that support for _datadoghq.eu_ is not ready yet, despite of what the form says. It will be coming soon.

There are a couple of optional parameters:
- __env__: Sets the environment at Datadog for traces for this GitLab instance. Empty by default, but you can set this if your organization has more than one infra for GitLab.
- __service__: Sets the service name for traces for this GitLab instance. Defaults to `gitlab-ci`. Again, you might want to set this in case you have more than one GitLab instance.

The page has a button to send a test request to Datadog, but even if the test is successful you still need to press the _Save_ button to apply the changes.

## Integrating through webhooks

If you are not using a version of GitLab that is recent enough to make the native integration available, you can still have traces for your pipelines by configuring the webhooks yourself. You need to configure the following webhooks in your GitLab site or repository:
- Job Events
- Pipeline Events

Use this URL `https://webhooks-http-intake.logs.datadoghq.com/v1/input/(api-key)`
and if you do not have an API key you can create one [here](https://app.datadoghq.com/account/settings#api)

You can make use of the same optional parameters that the native integration has, if you include them as query parameters in the webhook URL: `?env=(your-env)&service=(your-service-name)`
