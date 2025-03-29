---
​---
title: CI
description: Overview of Continuous Integration using GitHub Actions
keywords: CI, Continuous Integration, GitHub Actions, yaml
material: Lecture Notes
generator: Typora
author: Brian Bird
​---
---

<h1>Start of Sprint 3, Continuous Integration</h1>

**CS297 Programming Capstone**



<h2>Schedule</h2>

| Sprint | Week | Focus                                              |      | Sprint | Week | Focus                        |
| ------ | ---- | -------------------------------------------------- | ---- | ------ | ---- | ---------------------------- |
| 1      | 1    | Design review<br />project mgmt.<br />Git workflow |      | 4      | 7    | DevOps                       |
|        | 2    | First end of sprint meetings                       |      |        | 8    | <u>Beta release</u>          |
| 2      | 3    | Functional testing                                 |      | 5      | 9    | Code freeze                  |
|        | 4    |                                                    |      |        | 10   | <u>Release to production</u> |
| 3      | 5    | <mark>Continuous Integration</mark>                |      |        | 11   | Final presentation           |
|        | 6    | <u>Alpha release</u><br />Continuous Deployment    |      |        |      |                              |



<h2>Contents</h2>

[TOC]

## Introduction

### Spring 2024 Discussion

- Sprint 2 finished last week. Two teams have submitted their reports. A couple teams are having the product review meeting with their client today or tomorrow, so those sprint meeting reports will be turned in later this week.

### Week 5 Overview

- Sprint 3
  - Sprint planning meeting today or tomorrow.

  - Product review and team retrospective meetings at the end of next week.
- Alpha release at the end of this sprint (week 6)

  - Alpha testing
    - UX testing
    - Functional testing
  - Alpha presentations to the class by each team at the end of week 7 (two weeks from now).



## Continuous Integration

### What is CI?

Continuous Integration (CI) refers to multiple devs on a team frequently merging small changes with the main branch of their central repository. They are *integrating* changes *continuously* rather than periodically&mdash;hence the name, *Continuous Integration*.  The merge starts when a developer finishes a task (as long as it constitutes working, testable code) or a whole user story and sends a PR to the team.

One of the most important practices of CI is to <u>review and test</u> all the changes that you are making to your code before merging it to the main branch. You can do this with unit tests, integration tests, and/or functional tests[^1]. Automating the test process makes in practical to merge more often.

### Frequent Reverse Merging

Integrating code "continuously", means that devs merge their code once a day or even more often (Fowler, 2006). This doesn't mean devs need to send PRs that often. A dev can do frequent "reverse merges" where they merge the code from the main branch into their own development branch and test it&mdash;preferably with an automated test. (Of course, it only makes sense to do this after the main branch has changed.) This practice reduces integration problems when they do issue a PR and merge their code into the main branch. 

PRs to merge code into the main branch should be issued after each task (or set of tasks, if an individual task can't be tested) in a user story is completed. This is why automated testing is so important. If devs have to spend time manually testing code for daily PRs it will slow down development.

### Automated Building and Testing

All of the major Git central repository services, like GitHub, GitLab, BitBucket, and Azure DevOps, offer automated build and test services. These services require that environments be set up for both building and testing the software that is being developed. We will focus on doing this with GitHub Actions which allows a dev to automate workflows in response to events that are triggered in GitHub.

The most common way to automate functional testing of web apps is to use a test system that automates the browser. A popular browser test automation system is [Selenium](https://www.selenium.dev/).

#### Build and Test Using GitHub Actions

The basic idea behind GitHub Actions is that you set up a *workflow* to be triggered by some *event*.

- 
  Event

  An event is a specific activity in a repository. For example: creating a pull request, opening an issue, or pushing a commit.
  
- Workflow
  
  A workflow is an automated process that will run one or more *jobs*. Workflows are defined by a YAML[^2] file checked in to your repository.
  
- 
  Job

  A job is a set of steps in a workflow that execute on a runner.
  
- 
  Runner

  A runner is a server that runs your workflows.

##### Example YAML workflow file

The example below will build and test a .NET app whenever a PR is opened to merge code into the main branch. This file was autogenerated by GitHub.

```YAML
 pull_request:
    branches: [ main ]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    - name: Setup .NET
      uses: actions/setup-dotnet@v2
      with:
        dotnet-version: 5.0.x
    - name: Restore dependencies
      run: dotnet restore
    - name: Build
      run: dotnet build --no-restore
    - name: Test
      run: dotnet test --no-build --verbosity normal

```



## Next Time

In a future session, we will write some YAML workflows and experiment with several different triggers for building and testing code.



## References

David Posin, Paul Duvall, [Ref Card: Continuous Integration](https://dzone.com/refcardz/continuous-integration), DZone, 2018.

Martin Fowler, [Continuous Integration](https://www.martinfowler.com/articles/continuousIntegration.html), Martin Fowler' blog, 2006.

Cam Soper, Scott Addie, Colin Dembovsky, [DevOps for ASP.NET Core Developers](https://docs.microsoft.com/en-us/dotnet/architecture/devops-for-aspnet-developers/), Microsoft, 2022.

- "Build a .NET web app using GitHub Actions", pg. 39
- "Deploy a .NET web app using GitHub Actions", pg. 48

[GitHub Actions](https://docs.github.com/en/actions), GitHub documentation.

rainer Stropek, [C# ASP.NET 5 - CI/CD with GitHub Actions - Part 1](https://youtu.be/R5ppadIsGbA) YouTube, 2021.

Rick Anderson, Tom Dykstra, [Continuous Integration and Continuous Delivery (Building Real-World Cloud Apps with Azure)](https://docs.microsoft.com/en-us/aspnet/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery), Microsoft, 2022.

Sten Pittet, [The different types of software testing](https://www.atlassian.com/continuous-delivery/software-testing/types-of-software-testing), Atlassian.

Haris Khan, [Automated Testing with Selenium Using GitHub Actions – A Step-by-Step Guide](https://www.blazemeter.com/blog/automated-testing-selenium-github-actions), BlazeMeter, 2022.

[^1]: Integration tests are done to verify that the code modules that are being merged work together correctly. Functional tests verify that the end result of any action meets the business requirements&mdash;it doesn't check intermediate states or interactions between code modules. See the article by Sten Pittet.
[^2]: YAML, is a human-readable computer language used for configuration and meta-data for a variety of different computer applications. The syntax is a bit like JSON without curly braces.



------

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/88x31.png)](http://creativecommons.org/licenses/by/4.0/)
Capstone Class Lecture Notes by [Brian Bird](https://profbird.dev), 2022, revised <time>2024</time>, are licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/). 