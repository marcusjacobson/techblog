---
title: "Project Release - Sync an Azure DevOps repo to GitHub"
date: 2025-03-08
draft: false
categories: ["Github", "AzDO", "Projects"]
---

**Project Page**: [GitHub-Sync](/projects/azdo-github-sync/index.html)

## Project Introduction

I work in Azure DevOps daily to deploy resources using Azure using pipelines. Therefore, I have a high familiarity with using Azure DevOps for deployments and build both personal and professional projects in the environment. However, I also want to be able to share my personal projects more widely using GitHub, since it is a more recognized tool for this purpose. I also want to consolidate all of my projects in one place (GitHub), regardless of whether they were built using Azure DevOps.

While I could easily just manually copy and paste files between by Azure DevOps repo and my GitHub repository, I thought it would be an interesting thought exercise to see if I could figure out how to automate it using Azure Pipelines.

## Building the project

I built the project using a similar method that I use for most project in Azure DevOps. The main components are:

- Pipeline file - used by Azure Pipelines to automate the deployment.
- Pipleine-variables file - used to define the variables needed for the pipeline to run, such as the GitHub personal access token and Azure DevOps service connection.
- Script file - the pipeline is designed to run the script every time a run is initiated. The script contains the logic to perform the sync.

I started by searching the internet to see if I could find any existing tools that could perform this sync, but I wasn't able to find any solutions that were available off the shelf. There were some scripts that people published that provide ways to deploy the git commands manually (which I did use for inspiration), but they all required manual authentication which would not work within a pipeline.

**Note:** There is an Azure Boards plugin for GitHub which serves to sync work items between Azure Boards and GitHub Projects, but does not provide a solution to sync the repo contents.

Therefore I started down the path of:

1. Learning how to set up a programmatic link between GitHub and Azure DevOps. This is done by first setting up a [Fine-Grained GitHub Personal Access Token (PAT)](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens), and then creating an [Azure DevOps Service Connection](https://learn.microsoft.com/en-us/azure/devops/pipelines/library/service-endpoints?view=azure-devops) that links to GitHub, and enter the PAT into the service connection.
2. Learning the correct **git** commands to perform the sync and saving it into a **.sh** file.
3. Learning the way to call the Shell script within Azure Pipelines, and which variables are required to run the pipeline and pass to the script.
4. Create the pipeline-variables link according to the values needed in step 3, and reference the pipeline file.
5. Test and adjust accordingly until I achieved the results I was looking for.

## Project limitations

Due to limitations of the GitHub PAT, only write and update permissions are allowed, therefore the following idiosyncrasies are in place:

- Deleted files in Azure DevOps will need to be remediated manually in GitHub.
- Moved files in Azure DevOps will be duplicated, one instance of the original location and one instance of the new location.

The project page goes into more details on how to remediate these situations.

## Project specifics

To learn more about this project and link to where it is hosted in GitHub, see the [GitHub-Sync project page](/projects/azdo-github-sync.md). This contains more specifics on how the project was built, link to the project files in GitHub, and instructions to reuse it.

## Learnings

Most of the scripting work I perform daily within Azure DevOps is performed in PowerShell, however the best language I could find to use to run the required git commands is **Shell**. Therefore, I had to learn how to write the commands I wanted to do within Shell, and also learn how to build the pipeline file to use the Shell script. GitHub Copilot in VS Code was a great resource for this, however (as per usual) I am not satisfied with deploying any code unless I understand how it works. Therefore, I made sure to add appropriate comments throughout the script so any future user will also know what each action does.

I spent some time trying to figure out how I can sync deleted/moved items, but then I came to the realization that this is a limitation of the GitHub PAT.
