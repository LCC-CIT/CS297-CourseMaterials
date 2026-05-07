---
title: CD
description: Overview of Continuous Delivery using GitHub Actions for ASP.NET
keywords: CD, Continuous Delivery, GitHub Actions, ASP.NET Core, YAML, Environments
material: Lecture Notes
generator: Typora
author: Brian Bird
---

<h1>Continuous Delivery</h1>

**CS297 Software Development Capstone**

<h2>Contents</h2>

[TOC]

## Continuous Delivery

### What is CD?

Continuous Delivery (CD) is the practice of ensuring that your software is always in a releasable state throughout its lifecycle. It picks up where Continuous Integration (CI) leaves off. While CI focuses on frequently building and testing code, CD focuses on the automation required to deliver that code to an environment (like staging or production) quickly and reliably.

In a CD workflow, every change that passes the automated tests in the CI stage is automatically built and prepared for a release. The goal is to make deployments—whether to a test server or to your final customers—a "non-event" that can be performed at any time with the push of a button.

### Continuous Delivery vs. Continuous Deployment

Although often used interchangeably, there is a subtle but important difference between the two:

- **Continuous Delivery**: The code is always *ready* to be deployed. A human (like a project manager or lead dev) makes the final decision to trigger the actual release to production.
- **Continuous Deployment**: Every change that passes the full pipeline of automated tests is *automatically* deployed to production without human intervention.

For most student projects and enterprise teams, Continuous Delivery is the preferred approach as it provides a manual "gate" for final verification before code goes live.

### Benefits of Continuous Delivery

Implementing CD provides several advantages for a development team:

1. **Reduced Deployment Risk**: Since you are deploying small, incremental changes frequently, the risk associated with any single deployment is low. If something goes wrong, it is much easier to identify and fix the specific change that caused the issue.
2. **Faster Time to Market**: Automation eliminates the "deployment crunch" at the end of a sprint. Features can be released to stakeholders as soon as they are finished and tested.
3. **Consistency and Reliability**: Automation removes the "it works on my machine" problem. The same process is used to deploy to staging as is used for production, ensuring that the environment configuration is consistent.

## CD for ASP.NET Core and GitHub Actions

To implement CD for an ASP.NET Core application, you typically extend your CI workflow to include a **Publish** step and a **Deploy** job.

### Publishing the Application

The `dotnet publish` command compiles the application, reads its dependencies, and produces a set of files that are ready to be hosted on a web server. In a GitHub Actions workflow, this is usually done after the tests pass.

```YAML
    - name: Publish
      run: dotnet publish -c Release -o ./publish

```

### GitHub Environments and Secrets

To deploy securely, you should use **GitHub Environments**. Environments allow you to:

* **Store Secrets**: Save sensitive data like API keys, connection strings, or Azure Publish Profiles.
* **Protection Rules**: Require a specific person to approve a deployment before it starts.
* **Track Deployments**: See a history of which version of your code is currently running in "Staging" vs "Production".

### Example CD Workflow for ASP.NET

The following YAML snippet shows a deployment job that runs after a successful build. It uses a **Secret** to store the credentials for an Azure Web App.

```YAML
jobs:
  deploy:
    runs-on: ubuntu-latest
    needs: build  # This job only runs if the 'build' job succeeds
    environment: Production

    steps:
    - name: Download Artifact
      uses: actions/download-artifact@v3
      with:
        name: web-app

    - name: Deploy to Azure Web App
      uses: azure/webapps-deploy@v2
      with:
        app-name: 'my-capstone-app'
        publish-profile: ${{ secrets.AZURE_PUBLISH_PROFILE }}
        package: .

```

## Next Time

Next, we will look at **Infrastructure as Code (IaC)** and how to use tools like Terraform or Bicep to automate the creation of the servers we are deploying to.

## References

Jeevi Academy, [CI/CD for .NET Projects Using GitHub Actions](https://www.jeeviacademy.com/ci-cd-for-net-projects-using-github-actions/), 2024.

Microsoft Docs, [Continuous deployment to Azure App Service](https://learn.microsoft.com/en-us/azure/app-service/deploy-continuous-deployment), 2023.

Adrian Bailador, [GitHub Actions for .NET: Build, Test, and Deploy Your API](https://adrianbailador.github.io/blog/50-github-actions/), 2024.

Milan Jovanović, [Streamlining .NET 9 Deployment With GitHub Actions and Azure](https://www.milanjovanovic.tech/blog/streamlining-dotnet-9-deployment-with-github-actions-and-azure), 2024.

Sten Pittet, [Continuous delivery vs. continuous deployment](https://www.google.com/search?q=https://www.atlassian.com/continuous-delivery/principles/continuous-delivery-vs-continuous-deployment), Atlassian.

[](http://creativecommons.org/licenses/by/4.0/)
Capstone Class Lecture Notes by [Brian Bird](https://profbird.dev), 2022, revised 2026, are licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
