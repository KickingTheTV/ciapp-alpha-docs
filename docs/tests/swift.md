---
layout: page
title:  Swift
categories: swift test
permalink: /tests/swift
parent: Test Instrumentation
---

# Installation

## Using SPM

Add `dd-sdk-swift-testing` package to your project. It is located at https://github.com/DataDog/dd-sdk-swift-testing.
Then link your test targets with the library `DatadogSDKTesting` from the package.
If you are running UITests, your app running the tests should also be linked with this library.

## Binary linking

Download the project at [dd-sdk-swift-testing](https://github.com/DataDog/dd-sdk-swift-testing)
In a terminal go to the project folder and run `make release`, the resulting framework `DatadogSDKTesting.xcframework` can be found at `./build/xcframework`
Then you can copy and link your test targets with the XCFramework.
If you are running UITests, your app running the tests should also be linked with this library.

## Enabling

### Datadog Configuration


To enable testing instrumentation you must add the following environment variables to your test target. For UITests environment variables only need to be set in the test target, since the framework automatically injects these values to the application.

| Key                      | Value                       |
|--------------------------|-----------------------------|
| DD_TEST_RUNNER              |true              |
|DATADOG_CLIENT_TOKEN              | `<your current Datadog Client Token>`              |

You may want to set other environment variables also:

| Key                      | Value                       |
|--------------------------|-----------------------------|
|DD_ENV              |`<The environment you want to report>`              |
|DD_SERVICE              |`<The name of the service you want to report>`              |


### CI configuration

Depending on your CI service, you must also set the following environment variables:

#### Jenkins

| Key                      | Value                       |
|--------------------------|-----------------------------|
|GIT_COMMIT             |$(GIT_COMMIT)             |
|GIT_URL                |$(GIT_URL)                |
|WORKSPACE              |$(WORKSPACE)              |
|GIT_BRANCH             |$(GIT_BRANCH)             |
|JENKINS_URL            |$(JENKINS_URL)            |
|BUILD_ID               |$(BUILD_ID)               |
|BUILD_NUMBER           |$(BUILD_NUMBER)           |
|BUILD_URL           |$(BUILD_URL)           |


#### CircleCI

| Key                        | Value                         |
|--------------------------- |-------------------------------|
|CIRCLE_SHA1              |$(CIRCLE_SHA1)              |
|CIRCLE_REPOSITORY_URL    |$(CIRCLE_REPOSITORY_URL)    |
|CIRCLE_WORKING_DIRECTORY |$(CIRCLE_WORKING_DIRECTORY) |
|CIRCLE_BRANCH            |$(CIRCLE_BRANCH)            |
|CIRCLECI                 |$(CIRCLECI)                 |
|CIRCLE_BUILD_NUM         |$(CIRCLE_BUILD_NUM)         |
|CIRCLE_BUILD_URL         |$(CIRCLE_BUILD_URL)         |


#### GitLab CI

| Key                  | Value                   |
| -------------------  | ----------------------- |
|CI_COMMIT_SHA      |$(CI_COMMIT_SHA)      |
|CI_REPOSITORY_URL  |$(CI_REPOSITORY_URL)  |
|CI_PROJECT_DIR     |$(CI_PROJECT_DIR)     |
|CI_COMMIT_BRANCH   |$(CI_COMMIT_BRANCH)   |
|CI_COMMIT_REF_NAME |$(CI_COMMIT_REF_NAME) |
|CI_COMMIT_REF_NAME |$(CI_COMMIT_TAG) |
|GITLAB_CI          |$(GITLAB_CI)          |
|CI_JOB_URL         |$(CI_JOB_URL)         |
|CI_PIPELINE_ID         |$(CI_PIPELINE_ID)         |
|CI_PIPELINE_IID         |$(CI_PIPELINE_IID)         |
|CI_PIPELINE_URL         |$(CI_PIPELINE_URL)         |


#### Travis

| Key                          | Value                           |
| ---------------------------- | ------------------------------- |
|TRAVIS_COMMIT              |$(TRAVIS_COMMIT)              |
|TRAVIS_BUILD_DIR           |$(TRAVIS_BUILD_DIR)           |
|TRAVIS                     |$(TRAVIS)                     |
|TRAVIS_REPO_SLUG           |$(TRAVIS_REPO_SLUG)           |
|TRAVIS_BUILD_ID            |$(TRAVIS_BUILD_ID)            |
|TRAVIS_BUILD_NUMBER        |$(TRAVIS_BUILD_NUMBER)        |
|TRAVIS_PULL_REQUEST_BRANCH |$(TRAVIS_PULL_REQUEST_BRANCH) |
|TRAVIS_BRANCH              |$(TRAVIS_BRANCH)              |
|TRAVIS_BUILD_WEB_URL       |$(TRAVIS_BUILD_WEB_URL)       |
|TRAVIS_JOB_WEB_URL       |$(TRAVIS_JOB_WEB_URL)       |


#### GitHub Actions

| Key                 | Value                  |
| ------------------- | ---------------------- |
|GITHUB_SHA        |$(GITHUB_SHA)        |
|GITHUB_WORKSPACE  |$(GITHUB_WORKSPACE)  |
|GITHUB_REF        |$(GITHUB_REF)        |
|GITHUB_REPOSITORY |$(GITHUB_REPOSITORY) |
|GITHUB_RUN_ID     |$(GITHUB_RUN_ID)     |
|GITHUB_RUN_NUMBER |$(GITHUB_RUN_NUMBER) |

#### Buildkite

| Key                             | Value                              |
| ------------------------------- | ---------------------------------- |
|BUILDKITE           |$(BUILDKITE)           |
|BUILDKITE_COMMIT              |$(BUILDKITE_COMMIT)              |
|BUILDKITE_REPO                |$(BUILDKITE_REPO)                |
|BUILDKITE_BUILD_CHECKOUT_PATH |$(BUILDKITE_BUILD_CHECKOUT_PATH) |
|BUILDKITE_BRANCH              |$(BUILDKITE_BRANCH)              |
|BUILDKITE_BUILD_ID            |$(BUILDKITE_BUILD_ID)            |
|BUILDKITE_BUILD_NUMBER        |$(BUILDKITE_BUILD_NUMBER)        |
|BUILDKITE_BUILD_URL           |$(BUILDKITE_BUILD_URL)           |

#### Bitbucket Pipelines

| Key                        | Value                              |
| -------------------------- | ---------------------------------- |
|BITBUCKET_COMMIT         |$(BITBUCKET_COMMIT)              |
|BITBUCKET_GIT_SSH_ORIGIN |$(BITBUCKET_GIT_SSH_ORIGIN)      |
|BITBUCKET_CLONE_DIR      |$(BITBUCKET_CLONE_DIR)           |
|BITBUCKET_BRANCH         |$(BITBUCKET_BRANCH)              |
|BITBUCKET_BUILD_NUMBER   |$(BITBUCKET_BUILD_NUMBER)        |
|BITBUCKET_PIPELINE_UUID   |$(BITBUCKET_PIPELINE_UUID)        |

#### AppVeyor

| Key                                      | Value                                       |
| ---------------------------------------- | ------------------------------------------- |
|APPVEYOR                   |$(APPVEYOR)                   |
|APPVEYOR_REPO_COMMIT                   |$(APPVEYOR_REPO_COMMIT)                   |
|APPVEYOR_REPO_NAME                     |$(APPVEYOR_REPO_NAME)                     |
|APPVEYOR_BUILD_FOLDER                  |$(APPVEYOR_BUILD_FOLDER)                  |
|APPVEYOR_PULL_REQUEST_HEAD_REPO_BRANCH |$(APPVEYOR_PULL_REQUEST_HEAD_REPO_BRANCH) |
|APPVEYOR_REPO_BRANCH                   |$(APPVEYOR_REPO_BRANCH)                   |
|APPVEYOR_BUILD_ID                      |$(APPVEYOR_BUILD_ID)                      |
|APPVEYOR_BUILD_NUMBER                  |$(APPVEYOR_BUILD_NUMBER)                  |
|APPVEYOR_PROJECT_SLUG                  |$(APPVEYOR_PROJECT_SLUG)                  |

#### Azure Pipelines

| Key                                  | Value                                   |
| ------------------------------------ | --------------------------------------- |
|TF_BUILD                |$(TF_BUILD)                |
|BUILD_SOURCEVERSION                |$(BUILD_SOURCEVERSION)                |
|BUILD_REPOSITORY_URI               |$(BUILD_REPOSITORY_URI)               |
|BUILD_SOURCESDIRECTORY             |$(BUILD_SOURCESDIRECTORY)             |
|BUILD_SOURCEBRANCHNAME             |$(BUILD_SOURCEBRANCHNAME)             |
|BUILD_SOURCEBRANCH                 |$(BUILD_SOURCEBRANCH)                 |
|BUILD_BUILDID                      |$(BUILD_BUILDID)                      |
|BUILD_BUILDNUMBER                  |$(BUILD_BUILDNUMBER)                  |
|SYSTEM_TEAMPROJECT                 |$(SYSTEM_TEAMPROJECT)                 |
|SYSTEM_TEAMFOUNDATIONCOLLECTIONURI |$(SYSTEM_TEAMFOUNDATIONCOLLECTIONURI) |
|SYSTEM_PULLREQUEST_SOURCECOMMITID |$(SYSTEM_PULLREQUEST_SOURCECOMMITID) |
|SYSTEM_PULLREQUEST_SOURCEBRANCH |$(SYSTEM_PULLREQUEST_SOURCEBRANCH) |

#### Bitrise

| Key                                  | Value                                   |
| ------------------------------------ | --------------------------------------- |
|GIT_REPOSITORY_URL                          |$(GIT_REPOSITORY_URL)                          |
|BITRISE_GIT_COMMIT                |$(BITRISE_GIT_COMMIT)                |
|BITRISE_SOURCE_DIR               |$(BITRISE_SOURCE_DIR)               |
|BITRISE_APP_TITLE             |$(BITRISE_APP_TITLE)             |
|BITRISE_BUILD_SLUG             |$(BITRISE_BUILD_SLUG)             |
|BITRISE_BUILD_NUMBER                 |$(BITRISE_BUILD_NUMBER)                 |
|BITRISE_BUILD_URL                      |$(BITRISE_BUILD_URL)                      |
|BITRISE_APP_URL                  |$(BITRISE_APP_URL)                  |
|BITRISE_GIT_BRANCH                 |$(BITRISE_GIT_BRANCH)                 |
|BITRISEIO_GIT_BRANCH_DEST |$(BITRISEIO_GIT_BRANCH_DEST) |
|BITRISE_GIT_TAG |$(BITRISE_GIT_TAG) |
|GIT_CLONE_COMMIT_HASH |$(GIT_CLONE_COMMIT_HASH) |


## Running tests 

After installation, you can run your tests as you normally do, for example using the `xcodebuild test` command. 

Tests, network requests and application logs will be instrumented automatically.

## Extra configuration

### Disabling Auto Instrumentation

The framework automatically tries to capture the most information possible, but for some situations or tests it can be counter-productive. You can disable some of the autoinstrumentation for all the tests by setting the following environment variables:

> `Boolean` variables can use any of: `1`, `0`, `true`, `false`, `YES` or `NO` 

> `String` list variables accept a list of elements separated by `,` or `;`


{% highlight txt %}
DD_DISABLE_NETWORK_INSTRUMENTATION # Disables all network instrumentation (Boolean)
DD_DISABLE_STDOUT_INSTRUMENTATION # Disables all stdout instrumentation (Boolean)
DD_DISABLE_STDERR_INSTRUMENTATION # Disables all stderr instrumentation (Boolean)
{% endhighlight %}

### Network Auto Instrumentation

For Network autoinstrumentation there are other settings that you can configure

{% highlight txt %}
DD_DISABLE_HEADERS_INJECTION # Disables all injection of tracing headers (Boolean)
DD_INSTRUMENTATION_EXTRA_HEADERS # Specific extra headers that you want to log (String List)
DD_EXCLUDED_URLS # Urls that you don't want to log or inject headers into (String List)
DD_ENABLE_RECORD_PAYLOAD # It enables reporting a subset (512 bytes) of the payloads in 
                        requests and responses (Boolean)
{% endhighlight %}

You can also disable or enable specific autoinstrumentation in some of the tests from Swift or Objective-C by importing the module `DatadogSDKTesting` and using the class: `DDInstrumentationControl`.


## Supported versions

The Swift test instrumentation is compatible with the following platforms:

| PLATFORM    | VERSION |
| ----------- | ----- |
| iOS         |  11.0+  |
| macOS       |  10.13+ |
| tvOS        |  11.0+  |

and the following languages:

| PLATFORM    | VERSION |
| ----------- | ----- |
| Swift       |  5.3+   |
| Objective-C |  2.0+   |

## Supported CI providers

* [Appveyor](https://www.appveyor.com/)
* [Azure Pipelines](https://azure.microsoft.com/en-us/services/devops/pipelines/)
* [BitBucket](https://bitbucket.org/)
* [BuildKite](https://buildkite.com/)
* [CircleCI](https://circleci.com/)
* [Github Actions](https://github.com/features/actions)
* [Gitlab](https://docs.gitlab.com/ee/ci/)
* [Jenkins](https://www.jenkins.io/)
* [TravisCI](https://travis-ci.org/)
* [Bitrise](https://www.bitrise.io)
