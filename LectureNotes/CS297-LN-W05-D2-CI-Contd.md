---
​---
title: CI
description: Overview of Continuous Integration using GitHub Actions
keywords: CI, Continuous Integration, GitHub Actions, yaml, unit test, test runner, workflow
material: Lecture Notes
generator: Typora
author: Brian Bird
​---
---

<h1>Continuous Integration, Continued</h1>

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

## Creating a GitHub Actions Workflow File in YAML

The script that defines what GitHub Actions will do will be a file written in YAML (YAML is a bit like JSON without curly braces).

- Create a directory in your repository, on the main branch, with this path:
  `.github/workflows`
- Create a workflow file by creating a text file with the extension `.yaml` and give it a name, like:
  `ci-workflow.yaml`
- The easiest way to edit this file is to use Visual Studio Code with an extension that provides help writing GitHub Actions yaml files. I've tried these three:
  - YAML v1.7.0 by Red Hat. <u>This one works quite well!</u>
  - GitHub Actions v0.24.1 by Christopher Schleiden. This worked, but provided somewhat minimal syntax checking.
  - GitHub`v0.30.7`by KnisterPeter. Even after providing the app with a GitHub Personal Authentication Token, I didn't get any help with my yaml file.

### YAML Syntax

#### File Beginning and End

YAML files start with `---` and end with `...`

#### Data

There are two types of data in a yaml file: key-value pairs (aka dictionaries) and arrays (aka lists).

- Key-value pairs: use a colon to separate the key and value. 
  For example: `name: CI`

- Arrays: multiple items prefixed with a dash. For example:
  ```yaml
  - Squash
  - Cucumber
  - Potato
  ```

- Mix of key-value pairs and arrays. Example:
  ```
  - Vegetables:
  	- Squash
  	- Cucumber
  	- Potato
  - Fruit:
  	- Apple
  	- Orange
  	- Bannana
  ```

### Parts of an Actions Workflow

#### on

Specifies a trigger for the workflow. [Here is a list of triggers](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows).

#### steps

Tasks to execute when running a job.

#### jobs

A job is a set of steps in a workflow that execute on the same runner.

#### uses

This is where we describe the actions that will be taken. We find the actions that are possible in the [GitHub Actions Marketplace](https://github.com/marketplace?type=actions). Here are the ones we are using:

- [checkout](https://github.com/marketplace/actions/checkout)
- [setup-dotnet](https://github.com/marketplace/actions/setup-dotnet)



##### YAML workflow file for the Book Reviews project

The example below will build and test the Book Reviews project whenever code is pushed to the Test branch. 

```YAML
name: Continuous Integration

on:
  push:
    branches: 
    - Test
    - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - name: Check out code
      uses: actions/checkout@v3
    
    - name: Setup .NET Core 3.1
      uses: xt0rted/setup-dotnet@v1.3.0
      with:
        dotnet-version: '3.1.x'
    - name: Restore dependencies
      run: dotnet restore BookReviews/BookReviews.sln

    - name: Build app
      run: dotnet build BookReviews/BookReviews.sln -c Release --no-restore

    - name: Run Unit Tests
      run: dotnet test BookReviews/Tests/Tests.csproj -c Release --no-build
```



### Unit Test Issues

The first time I tried to run this, I ran into issues with my unit tests. When the Test Runner reached the "Run Unit Tests" step, it would get as far as:

> Starting test execution, please wait...   
> A total of 1 test files matched the specified pattern.

And then it would hang indefinitely.

#### Debugging the unit tests

- I ran my tests from the command line on Ubuntu Linux, using the same parameters as in the Actions file, and everything passed. So, it seemed that the a problem was with the way the Actions workflow runner runs the tests.

- I tried commenting out tests and it seemed that if I commented out one or more of the tests that called `async` controller methods, then the test would run. It seemed that there was a problem with running tests in parallel. 

- I checked my tests to see if they were *thread-safe* and found that my repository was <u>not</u> thread-safe. The `List` that I used as a data store was `static` and C# Lists themselves are not thread-safe. To make my repository thread-safe, I made these two changes:

  - I changed the List to a `ConcurrentBag` which is a thread-safe collection object.
  - I made the ConcurrentBag not static, the repository now uses a ConcurrentBag object.

  These changes did not solve the problem of my tests hanging on GitHub Actions.

- I tried changing the .NET version to 5.0. This did not solve the problem.

- 
  I tried adding a command line option to turn off running the tests in parallel:

  `run: dotnet test BookReviews/Tests/Tests.csproj -c Release --no-build  -- MSTest.parallelizeTestCollections=false`

  This didn't solve the problem either.

#### Solving the unit test problem

Finally, I added attributes to the test classes that specify that all of the classes are in one *collection*. By default, xUnit will run each collection in parallel (simultaneously). This attribute, `[Collection("All Tests")]`, puts all the tests in one collection, so they are not run in parallel.

This solved the problem. My tests now run and pass!

## Development Workflow

This is one possible *development workflow* (not to be confused with the Actions *workflow* file) for implementing *Continuous Integration*. 

When you have code that you want to test with code from one or more team-mates, but you (or they) aren't ready to merge code into the main branch:

1. 
   Make a *test* branch, merge the *main* branch into it, and push it to GitHub.

   This triggers the Actions CI workflow to execute. This is good. It will verify that the code merged from main passes. you now have a verified baseline for testing new code.

2. Merge the new code from everyone's branch who wants to do integration testing into the test branch.

   This triggers the CI workflow to run again to verify that my new code builds without errors and unit tests pass (or not).

When you have code that is ready for a PR and to be merged into main:

1. Do a *reverse merge* (merging the main into your new code branch). Build and test the code locally to verify everything is ok.
2. Create a PR to get the code reviewed and merged into main. When the new code is merged into main, the CI workflow is triggered to run and verify that all is well.



## Example

[CS 296N Book Reviews Web Site (2022 Version)](https://github.com/LCC-CIT/CS296N-Example-BookReviews)



## Next Time

In future sessions, we will add integration tests and deployment to our GitHub Actions workflow.



## References

rainer Stropek, [C# ASP.NET 5 - CI/CD with GitHub Actions - Part 2](https://youtu.be/ySVsLE0XWQA) YouTube, 2021.

Cam Soper, Scott Addie, Colin Dembovsky, [DevOps for ASP.NET Core Developers](https://docs.microsoft.com/en-us/dotnet/architecture/devops-for-aspnet-developers/), Microsoft, 2022.

- "Build a .NET web app using GitHub Actions", pg. 39
- "Deploy a .NET web app using GitHub Actions", pg. 48

[GitHub Actions](https://docs.github.com/en/actions), GitHub documentation.

Rick Anderson, Tom Dykstra, [Continuous Integration and Continuous Delivery (Building Real-World Cloud Apps with Azure)](https://docs.microsoft.com/en-us/aspnet/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery), Microsoft, 2022.



------

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/88x31.png)](http://creativecommons.org/licenses/by/4.0/)
Capstone Class Lecture Notes by [Brian Bird](https://profbird.dev), <time>2022</time>, revised <time>2023</time> are licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/). 