---
layout: page
title:  GitLab CI
categories: ci gitlab
permalink: /ciprovider/gitlab
parent: Pipeline Instrumentation
---

To enable traces for your GitLab CI pipelines a [native integration](https://gitlab.com/gitlab-org/gitlab/-/merge_requests/46564) has been merged into GitLab and is hidden under a [feature flag](https://docs.gitlab.com/ee/administration/feature_flags.html) since the release __v13.7.0__.

If you are a user of [GitLab.com](https://gitlab.com) and you want to early-adopt this integration, reach out to us so we enable it for your account on [GitLab.com](https://gitlab.com).

If you are managing your own GitLab installation and your version is recent enough, you can enable the feature flag yourself by executing the following commands that use GitLab's [Rails Runner](https://docs.gitlab.com/ee/administration/operations/rails_console.html#using-the-rails-runner) depending on your installation type:

For Omnibus installations:

    sudo gitlab-rails runner "Feature.enable(:datadog_ci_integration)"

For installations from source:

    sudo -u git -H bundle exec rails runner -e production "Feature.enable(:datadog_ci_integration)"

For [Kubernetes deployments](https://docs.gitlab.com/ee/administration/troubleshooting/kubernetes_cheat_sheet.html#gitlab-specific-kubernetes-information):

    kubectl exec -it <task-runner-pod-name> -- /srv/gitlab/bin/rails runner "Feature.enable(:datadog_ci_integration)"


Once the feature is enabled, configuring the integration is as easy as going to the page for the Datadog integration at any level:
- On a per project basis, by going to the "Settings > Integrations > Datadog" section of each project.
- For all the projects in your GitLab installation, by going to "Settings > Integrations > Datadog" section of the Admin area.

The Datadog integration page looks like this:

![Integration Screenshot](/ciapp-alpha-docs/assets/gitlab-integration.png)

You only need to mark it as active and paste a valid API key. If you do not have an API key you can create one [here](https://app.datadoghq.com/account/settings#api).

__Note:__ only `datadoghq.com` is currently supported.

There are a couple of optional parameters:
- __service__: Sets the service name for all traces for this GitLab instance. Defaults to `gitlab-ci`. Only useful if there are more than one GitLab instance.
- __env__: Sets the environment tag for all traces for this GitLab instance. Only useful in advanced setups where grouping GitLab instances per environment is required.

The integration can be tested with the "Test settings" button. After it's successful, click on "Save changes" to finish the integration set up.


## Integrating through webhooks

If you are not using a version of GitLab that is recent enough to make the native integration available, you can still have traces for your pipelines by configuring the webhooks yourself. You need to configure the following webhooks in your GitLab site or repository:
- Job Events
- Pipeline Events

Use the following webhooks URL:

    https://webhooks-http-intake.logs.datadoghq.com/v1/input/(api-key)

You can create an API key [here](https://app.datadoghq.com/account/settings#api).

You can make use of the same optional parameters that the native integration has, if you include them as query parameters in the webhook URL: `?env=(your-env)&service=(your-service-name)`

![Webhooks Screenshot](/ciapp-alpha-docs/assets/gitlab-webhooks.png)
