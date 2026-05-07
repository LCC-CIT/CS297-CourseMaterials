---
title: Continuous Delivery
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

Continuous Delivery (CD) is the practice of ensuring that your software is in a releasable state throughout its lifecycle. It picks up where Continuous Integration (CI) leaves off. While CI focuses on frequently building and testing code, CD focuses on the automation required to publish the application&mdash;in our case, publishing a web app to a web server.

In a CD workflow, every change that passes the automated tests in the CI stage is automatically built and prepared for a release. The goal is to make deployments—whether to a test server or production—a simple "non-event" that can be performed at any time with the push of a button.

### Continuous Delivery vs. Continuous Deployment

Although often used interchangeably, there is a subtle but important difference between the two:

- **Continuous Delivery**: The code is always *ready* to be deployed. A human (like a project manager or lead dev) makes the final decision to trigger the actual release to production.
- **Continuous Deployment**: Every change that passes the full pipeline of automated tests is *automatically* deployed to production without human intervention.

For most student projects and enterprise teams, *Continuous Delivery* is the preferred approach as it provides a manual "gate" for final verification before code goes live.

### Benefits of Continuous Delivery

Implementing *Continuous Delivery* provides several advantages for a development team:

1. **Reduced Deployment Risk**: Since you are deploying <u>small, incremental</u> changes frequently, the risk associated with any single deployment is low. If something goes wrong, it is much easier to identify and fix the specific change that caused the issue.
2. **Faster Time to Market**: Automation eliminates the "deployment crunch" at the end of a sprint. Features can be released to stakeholders as soon as they are finished and tested.
3. **Consistency and Reliability**: Automation removes the "it works on my machine" problem. The s<u>ame process is used to deploy to staging as is used for production</u>, ensuring that the environment configuration is consistent.

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

#### Explanation of the Deployment Job

The YAML snippet above describes a **deployment job**. This job is designed to take the code that was built and tested in a previous stage and move it onto a live server.

##### Job Configuration

- `deploy:`**deploy:** This is the name of the job. 
- `runs-on: ubuntu-latest`**runs-on: ubuntu-latest** This specifies the type of virtual machine (runner) that will execute the steps. 
- `needs: build`**needs: build** This creates a dependency. The `deploy` job will not start until the job named `build` has completed successfully. 
- `environment: Production`**environment: Production** This links the job to a specific "Environment" defined in your GitHub repository settings. This is useful for tracking deployment history and applying protection rules, such as requiring an approval before the code goes live.

##### Step-by-Step Execution

**1. Download Artifact**

```yaml
- name: Download Artifact
  uses: actions/download-artifact@v3
  with:
    name: web-app
```

Since each job in a workflow runs on a fresh virtual machine, the files compiled in the `build` job are not automatically present in the `deploy` job. This step uses the `download-artifact` action to fetch the compiled application files (named `web-app`) that were saved during the build phase.

**2A. Deploy to Azure Web App**

```yaml
- name: Deploy to Azure Web App
  uses: azure/webapps-deploy@v2
  with:
    app-name: 'my-capstone-app'
    publish-profile: ${{ secrets.AZURE_PUBLISH_PROFILE }}
    package: .
```

This is the final action that performs the actual delivery:

- `app-name`**app-name**: Identifies the specific service on Azure where the app should be hosted.
- `publish-profile`**publish-profile**: This uses a **GitHub Secret**. Instead of hardcoding sensitive passwords or keys in the YAML file, it references `AZURE_PUBLISH_PROFILE`, which is stored securely in the repository settings.
- `package: .`**package: .**: Tells the runner to take everything in the current directory (the files downloaded in the previous step) and upload them to the web server.

**2B. Deploy to a Web Host using Web Deploy**

To modify the workflow for a host that supports *Microsoft Web Deploy* (often used for on-premises IIS servers or specific Windows-based hosting like [SmarterASP.NET](https://www.smarterasp.net/index?r=profbird)), you must switch the runner to a Windows environment and use the `msdeploy.exe` utility as shown in the deploy step below.

```yaml
jobs:
  deploy:
    runs-on: windows-latest
    needs: build
    environment: Production

    steps:
    - name: Download Artifact
      uses: actions/download-artifact@v3
      with:
        name: web-app
        path: ./publish
    
    - name: Deploy to SmarterASP.NET
      shell: pwsh
      run: |
        & "C:\Program Files (x86)\IIS\Microsoft Web Deploy V3\msdeploy.exe" `
        -verb:sync `
        -source:contentPath='${{ github.workspace }}\publish' `
        -dest:contentPath='${{ secrets.SMARTERASP_SITE_NAME }}',`
        ComputerName='https://${{ secrets.SMARTERASP_SERVER_URL }}:8172/msdeploy.axd?site=${{ secrets.SMARTERASP_SITE_NAME }}',`
        UserName='${{ secrets.SMARTERASP_USER }}',`
        Password='${{ secrets.SMARTERASP_PASSWORD }}',`
        AuthType='Basic' `
        -allowUntrusted `
        -enableRule:DoNotDeleteRule
```

##### Explanation of Web Deploy Steps

Deploying via Microsoft Web Deploy requires a more detailed configuration than the standardized Azure actions. 

- `runs-on: windows-latest`**runs-on: windows-latest**: Unlike the build job which can run on Linux, Web Deploy is a Windows-native technology. Using a Windows runner ensures that `msdeploy.exe` is pre-installed and available in the environment.
- `shell: pwsh`**shell: pwsh**: This specifies PowerShell Core, which handles the multiline command and backtick (```) line continuations more reliably in GitHub Actions.
- `-verb:sync`**-verb:sync**: This is the primary command for Web Deploy. It instructs the tool to synchronize the source (your local GitHub runner files) with the destination (the remote server), only transferring the files that have changed.
- `-source:contentPath`**-source:contentPath**: Defines the local directory containing your compiled ASP.NET application.
- `ComputerName`**ComputerName**: This is the endpoint for the **Web Management Service (WMSvc)**. It typically uses port **8172** and includes the site name in the query string to ensure the files reach the correct IIS website.
- `AuthType='Basic'`**AuthType='Basic'**: While other types exist, `Basic` is the standard for remote synchronization over HTTPS when using a dedicated deployment user.
- `-allowUntrusted`**-allowUntrusted**: This flag is essential if your server uses a self-signed SSL certificate for the management service, which is common in development or academic lab settings.



***Note: These notes were drafted using Gemini 3.1***



## References

Jeevi Academy, [CI/CD for .NET Projects Using GitHub Actions](https://www.jeeviacademy.com/ci-cd-for-net-projects-using-github-actions/), 2024.

Microsoft Docs, [Continuous deployment to Azure App Service](https://learn.microsoft.com/en-us/azure/app-service/deploy-continuous-deployment), 2023.

Adrian Bailador, [GitHub Actions for .NET: Build, Test, and Deploy Your API](https://adrianbailador.github.io/blog/50-github-actions/), 2024.

Milan Jovanović, [Streamlining .NET 9 Deployment With GitHub Actions and Azure](https://www.milanjovanovic.tech/blog/streamlining-dotnet-9-deployment-with-github-actions-and-azure), 2024.

Sten Pittet, [Continuous delivery vs. continuous deployment](https://www.google.com/search?q=https://www.atlassian.com/continuous-delivery/principles/continuous-delivery-vs-continuous-deployment), Atlassian.

----

[](http://creativecommons.org/licenses/by/4.0/)
Capstone Class Lecture Notes by [Brian Bird](https://profbird.dev), 2026, are licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

----
