---
layout: page
title:  Running tests inside a container
categories: test container
permalink: /tests-in-container
nav_order: 4
---

# Running tests inside a container

If you are running your tests inside a container, forward the following environment variables depending on your CI provider, so the Datadog Tracer can autodetect the build information.

### [Appveyor](https://www.appveyor.com/docs/environment-variables/)

- APPVEYOR
- APPVEYOR_BUILD_ID
- APPVEYOR_BUILD_NUMBER
- APPVEYOR_BUILD_FOLDER
- APPVEYOR_REPO_PROVIDER
- APPVEYOR_REPO_NAME
- APPVEYOR_REPO_BRANCH
- APPVEYOR_REPO_COMMIT
- APPVEYOR_REPO_TAG_NAME
- APPVEYOR_PULL_REQUEST_HEAD_REPO_BRANCH

### [Azure Pipelines](https://docs.microsoft.com/en-us/azure/devops/pipelines/build/variables?view=azure-devops)

- TF_BUILD
- BUILD_DEFINITIONNAME
- BUILD_BUILDID
- BUILD_SOURCESDIRECTORY
- BUILD_REPOSITORY_URI
- BUILD_SOURCEBRANCH
- BUILD_SOURCEVERSION
- BUILD_SOURCEBRANCH
- BUILD_SOURCEVERSION
- SYSTEM_TEAMFOUNDATIONSERVERURI
- SYSTEM_TEAMPROJECT
- SYSTEM_JOBID
- SYSTEM_TASKINSTANCEID
- SYSTEM_PULLREQUEST_SOURCEREPOSITORYURI
- SYSTEM_PULLREQUEST_SOURCEBRANCH
- SYSTEM_PULLREQUEST_SOURCECOMMITID

### [BitBucket](https://support.atlassian.com/bitbucket-cloud/docs/variables-and-secrets/)

- BITBUCKET_PIPELINE_UUID
- BITBUCKET_BUILD_NUMBER
- BITBUCKET_CLONE_DIR
- BITBUCKET_REPO_FULL_NAME
- BITBUCKET_GIT_SSH_ORIGIN
- BITBUCKET_COMMIT
- BITBUCKET_BRANCH
- BITBUCKET_TAG

### [BuildKite](https://buildkite.com/docs/pipelines/environment-variables)

- BUILDKITE
- BUILDKITE_PIPELINE_SLUG
- BUILDKITE_JOB_ID
- BUILDKITE_BUILD_ID
- BUILDKITE_BUILD_NUMBER
- BUILDKITE_BUILD_URL
- BUILDKITE_BUILD_CHECKOUT_PATH
- BUILDKITE_REPO
- BUILDKITE_COMMIT
- BUILDKITE_BRANCH
- BUILDKITE_TAG

### [CircleCI](https://circleci.com/docs/2.0/env-vars/#built-in-environment-variables)

- CIRCLECI
- CIRCLE_PROJECT_REPONAME
- CIRCLE_BUILD_NUM
- CIRCLE_BUILD_URL
- CIRCLE_WORKFLOW_ID
- CIRCLE_WORKING_DIRECTORY
- CIRCLE_REPOSITORY_URL
- CIRCLE_SHA1
- CIRCLE_BRANCH
- CIRCLE_TAG

### [Github Actions](https://docs.github.com/en/free-pro-team@latest/actions/reference/environment-variables#default-environment-variables)

- GITHUB_ACTION
- GITHUB_RUN_ID
- GITHUB_RUN_NUMBER
- GITHUB_WORKFLOW
- GITHUB_WORKSPACE
- GITHUB_REPOSITORY
- GITHUB_SHA
- GITHUB_HEAD_REF
- GITHUB_REF

### [GitLab](https://docs.gitlab.com/ee/ci/variables/predefined_variables.html)

- GITLAB_CI
- CI_PIPELINE_ID
- CI_PIPELINE_URL
- CI_PIPELINE_IID
- CI_PROJECT_PATH
- CI_PROJECT_DIR
- CI_JOB_URL
- CI_REPOSITORY_URL
- CI_COMMIT_SHA
- CI_COMMIT_BRANCH
- CI_COMMIT_TAG

### [Jenkins](https://wiki.jenkins.io/display/JENKINS/Building+a+software+project)

- JENKINS_URL
- BUILD_TAG
- BUILD_NUMBER
- BUILD_URL
- WORKSPACE
- JOB_NAME
- JOB_URL
- GIT_URL
- GIT_COMMIT
- GIT_BRANCH

### [TravisCI](https://docs.travis-ci.com/user/environment-variables/#default-environment-variables)

- TRAVIS
- TRAVIS_BUILD_ID
- TRAVIS_BUILD_NUMBER
- TRAVIS_BUILD_WEB_URL
- TRAVIS_BUILD_DIR
- TRAVIS_JOB_WEB_URL
- TRAVIS_REPO_SLUG
- TRAVIS_COMMIT
- TRAVIS_BRANCH
- TRAVIS_TAG
- TRAVIS_PULL_REQUEST_SLUG
- TRAVIS_PULL_REQUEST_BRANCH