---
layout: page
title: Release Notes
categories: release notes
permalink: /releasenotes
nav_order: 6
---
# Release Notes

## March 2nd, 2021

**Pipeline & Test data available in Dashboards - Both Tests & Pipelines**

![Pipeline & Test data in Dashboards](/docs/assets/pipeline-test-data-in-dashboards.png)

When creating new Dashboard widgets, you'll now have "CI Pipelines" and "CI Tests" available as data sources. When selecting CI Pipelines, you'll be able to choose whether you want to work with Pipelines, Stages, Jobs, or All.


**Flaky Test Management - Tests**

![Flaky Test Management](/docs/assets/flaky-test-management.png)

Flaky tests can be very problematic in an organization: knowing which tests are flaky is left to tribal knowledge, developers lose trust in their test results, and a tremendous amount of time and resources are wasted on pipeline retries.

Flaky tests are defined as tests that exhibit both a passing and failing status across multiple test runs for the same commit. We now have a Flaky Tests table for a given Test Service & Branch. You'll be able to see all of the tests that have flaked in the time frame you have selected.

When it comes to prioritizing flaky tests, we provide a few different ways for you to better understand each flaky test:

* Occurrences - this is the number of commits in which the test exhibited flaky behavior
* Failure Rate - the percentage of test runs that have failed for this test since it first flaked
* Trend - a visual tool that can help you determine if a flaky test was fixed or it's still actively flaking
* Once you've identified a flaky test you want to fix, clicking on a test will provide useful pointers to the commits in which the test first and last flaked.


**Test Performance Tab - Tests**

![Test Performance](/docs/assets/test-performance.png)

There is a new Performance tab in the detail view of your Tests. You can view all of the test runs for a given test for whatever time frame selected. This provides an easy way to get a historical perspective of your test.

You can see if your test is getting slower over time or if your efforts to improve test speed were effective and held through multiple commits.


**Most Common Errors - Tests**

![Most Common Errors](/docs/assets/most-common-errors.png)

We've updated the Test Summary section in the Test Service Overview page. We've added the Most Common Errors widget, which will show you the most common error types and their number of occurrences, across all of your tests for the time frame selected.

This can be useful for surfacing the highest contributing root causes for test failures across your entire test suite.


**Pipeline, Stage, and Job Selector - Pipelines**

![Pipeline stage job selector](/docs/assets/pipeline-stage-job-selector.png)

We've updated our pipeline tables to include a selector, so you can see a more granular breakdown by Stage or Job.
