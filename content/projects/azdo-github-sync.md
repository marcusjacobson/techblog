---
title: "GitHub & AzDO - Sync an existing AzureDevOps Repository to GitHub"
date: 2025-03-08
draft: false
categories: ["Github", "AzDO"]
---

**Version**:    1.0.0

**Author**:     Marcus Jacobson

**License**:    [MIT](https://opensource.org/licenses/MIT)

**Repository**: [GitHub](https://github.com/marcusjacobson/Projects/tree/main/Github-Sync)

## Project Goal

Create a one-way sync from Azure DevOps to GitHub, for the purpose of publishing projects created in Azure DevOps to the shareable GitHub repo.

## Project Outcomes

Upon running the pipeline in AzureDevops, any new or changed files in the Azure DevOps repo will be updated in the GitHub repository.

**Limitations**:

- Due to the allowable permissions for GitHub personal access tokens, only read & write permissions are allowed, but delete permissions are not available. Therefore any deleted files in the Azure DevOps will not be deleted in GitHub.
- Any files that are moved within Azure DevOps will be duplicated, one version in each locations. Therefore any deleted or moved files will need to be manually remediated in GitHub.
- Another remediation option would be to empty the GitHub repository and then run the pipeline again in Azure DevOps. This will make sure that only the most recent files and folder structure is live in GitHub.

## Features

There are three files that are included as part of this project:

- **pipeline\github-sync.yml** - The pipeline file to run within Azure DevOps
- **pipeline\pipeline-variables.yml** - The file containing the variables that are referenced in the pipeline and script.
- **scripts\sync-to-github.sh** - The script that is run as part of the pipeline, that performs the one-way sync from Azure DevOps to GitHub.

These files are meant to be deployed together, maintaining the provided folder structure.

## Installation

To "install" this project, perform the following actions:

1. Create a fork of the the Projects repository to your own GitHub account.
2. From your forked repository, copy the contents of the GitHub-Sync folder into the Azure DevOps repository you want to sync.
3. Follow the steps within the project **README** file to set up the GitHub personal access token and Azure DevOps service connection.
4. Edit the **pipeline-variables.yml** file to include your current environment details.
5. Create a new manual pipeline in Azure DevOps, using the **github-sync.yml** file as the reference, and run the pipeline.

## Usage

Once the pipeline has been set up in Azure DevOps, it is designed to be run any time there is an update to the main brach in the Azure DevOps repo. For the most efficient use of this pipeline, it is recommended to follow the branching practices below:

- Any time you intend to make edits within the Azure DevOps repo, first create a branch off of main.
- Make your edits within the branch.
- Once the edits are completed within the branch, run a pull request back into main. This action will cause the pipeline to run to back up any changes to GitHub.

**Note:** While making changes directly in main will not "break" the backup process, it will cause the pipeline to run every time a change is committed, which is overkill and not a great use of the VM pools used to run pipelines. If you intend to make changes directly in Main, it is recommended to change the trigger value within github-sync,yml to **none**, and then run the pipeline manually when you intend to push your changes to GitHub.

```yml
trigger:
- none
```

## Contributing

I welcome your feedback and contributions to improve this project. To provide feedback or ask questions, please use [GitHub Discussions](https://github.com/marcusjacobson/Projects/discussions).

Thank you for your contributions and feedback!

## License

I distribute my projects under the MIT Open Source license. You are welcome to re-use any of these projects for your own personal deployments, though I ask they are not used directly for any for-profit initiatives.

## Additional Resources

For specific project details, please visit the [GitHub-Sync repository](https://github.com/marcusjacobson/Projects/tree/main/Github-Sync).

To see my other projects, please visit the root of my [Projects repository](https://github.com/marcusjacobson/Projects).