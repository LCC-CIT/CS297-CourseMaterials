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

The script that defines what GitHub Actions will do for you will be a file written in YAML (YAML is a bit like JSON without curly braces).

- Create a directory in your repository with this path:
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

There are two types of data in a yaml file, key-value pairs (aka dictionaries) and lists (aka arrays).

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

In future sessions, we will add integration tests and deployment to our GitHub Actions workflow.



## References

rainer Stropek, [C# ASP.NET 5 - CI/CD with GitHub Actions - Part 2](https://youtu.be/ySVsLE0XWQA) YouTube, 2021.

Cam Soper, Scott Addie, Colin Dembovsky, [DevOps for ASP.NET Core Developers](https://docs.microsoft.com/en-us/dotnet/architecture/devops-for-aspnet-developers/), Microsoft, 2022.

- "Build a .NET web app using GitHub Actions", pg. 39
- "Deploy a .NET web app using GitHub Actions", pg. 48

[GitHub Actions](https://docs.github.com/en/actions), GitHub documentation.

Rick Anderson, Tom Dykstra, [Continuous Integration and Continuous Delivery (Building Real-World Cloud Apps with Azure)](https://docs.microsoft.com/en-us/aspnet/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery), Microsoft, 2022.

[^]: 



------

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/88x31.png)](http://creativecommons.org/licenses/by/4.0/)
Capstone Class Lecture Notes by [Brian Bird](https://profbird.dev), <time>2022</time>, are licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/). 