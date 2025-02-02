---
title: "First Blog Post - Creating this Blog"
date: 2025-02-01
draft: false
---

# Why I created this blog

My name is Marcus, and I am an IT professional focused in Azure Cloud Deployments, and working to improve my skills in the Security and AI spaces. This blog is meant to be a space for me to focus on the following subjects:

- Discussions on personal projects I am working on
- Details on deployments with screenshots and code snippets, to help others as they come across the content
- Posts relating to learning activities I am working on, including certifications.

This blog is posted using the Hugo framework within GitHub pages. I chose this method since it is a free way to host content and it allows me to still have the control around content publishing and site theming. For more details on using Hugo, please visit [https://gohugo.io/](https://gohugo.io/).

I was also inspired to use this method to deploy my blog after coming across the following YouTube video: [Frontend Tutorials: How to create and host a blog on Github](https://www.youtube.com/watch?v=nTLzLhFG9mc). If you are interested in deploying a blog using this method, please check out the video and support the creator. He did a fantastic job of explaining the process.

# How I created this blog

Put simply, I followed the steps outlined in the video. However, please read on for a text breakdown.

## Install Hugo

The method to install Hugo will vary depending on which operating system you use. The process I describe below was done on a Windows 11 PC, however you can find instructions for all operating systems at [Hugo - Installation](https://gohugo.io/installation/).

- From a **PowerShell 7** terminal, run the command ```winget install Hugo.Hugo.Extended```.
  - It is not recommended to use the default **Windows-PowerShell** terminal that comes pre-installed.
  - I installed the **Extended** edition. Review the documentation on the Installation link above for details on the different versions.
- Once Hugo is confirmed to be installed, restart your terminal or close/re-open your coding environment (I use Visual Studio Code).
  - The **hugo** commands will not be recognized until the terminal is restarted.
- Run ```hugo version``` to check install status.
  - You should see an output similar to *hugo v0.142.0-1f746a872442e66b6afd47c8c04ac42dc92cdb6f+extended windows/amd64 BuildDate=2025-01-22T12:20:52Z VendorInfo=gohugoio*

## Create a new repo in GitHub

You will want a dedicated repo for this deployment in GitHub. I chose to title mine **techblog**, but you can choose whatever name you like. 

It is recommended to clone your repo on your local device so that you can make edits in VS Code or a similar editor.

## Create a new blank Hugo site

To create a new site with the same name as the repo, in my case **techblog**, use the command ```hugo new site . --force```.

## Deploy a theme to the Hugo site

Since nobody wants to read a blog site with no formatting, the next step would be to deploy a theme for your site. I chose the **Ananke** theme, but there are several others located at [Hugo - Themes](https://themes.gohugo.io/).

To deploy the **Ananke** theme, use the command ```git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke```. Once the theme is installed, you will want to configure your site to reference the theme by editing the **hugo.toml** file and add the line: **theme = 'ananke'**

## Create a Hello World page

In true form for IT people, you will want to follow etiquette and create your first page called **Hello World!**. To set this up within your repository:

- Create a new subfolder under **content** called **posts**
- Create a new file **hello-world.md** with the following content:

You can leverage the following text for the hello-world.md file:

**Note** the metadata at the top that is between the block in between the lines with **---** provides details required for the post. Do not skip this step.

```
---
title: "Hello World!"
date: 2025-02-01
draft: false
---

# Hello World

This is a test Hello World post, using Hugo.
```

## Check the localhost version of the file

In your PowerShell Terminal, run the command ```hugo server``` to start the local server. Once the message comes up that it is available, copy the localhost URL (mine is http://localhost:1313/) to view your local page with your first blog post.

**Note** If you already had the local server running, you may need to stop and start it before seeing the page update.

## Set up Github workflow

The next step is to set up the GitHub workflow. When run. the workflow in the code block below will deploy a branch within your GitHub repository titled **gh-pages**, which can then be used to deploy your site within GitHub pages.

Follow the steps below to set up this GitHub workflow: 

- Create a new folder in your repo called **.githib**, with a subfolder **workflows**
- Within the **workflows** folder, create a new YML file for the workflow. Mine is called **hugo-build.yml**, but you can call yours whatever you want.
- Insert the following codeblock into your YML file.

```
name: Build Hugo Site

on:
  push:
    branches:
      - main 

jobs:
  deploy:
    runs-on: ubuntu-latest
    concurrency:
      group: ${{ github.workflow }}-${{ github.ref }}
    steps:
      - name: Checkout repo
        uses: actions/checkout@v3
        with:
          submodules: true # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0   # Fetch all history for .GitInfo and .Lastmod
      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: '0.142.0'
          extended: true
      - name: Build
        run: hugo --minify
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        if: ${{ github.ref == 'main' }}
        with: 
          personal_token: ${{ secrets.ACCESS_TOKEN }}
          publish_dir: ./public
```

## Commit all files to github

Once you have made all of these edits in your local editor, commit the files up to github and make sure they show up for you within your GitHub site.

## Configure the GitHub action with permissions to write to your repo.

- Within GitHub, go to Actions and locate your deployed action.
- Go to **settings**, and then enable the workflow permissions to **Read and write permissions**
- Re-run your GitHub action. If completed successfully, it will have deployed a **gh-pages** branch within your repo.

## Configure GitHub to deploy the branch to GitHub Pages:

Perform the following steps to deploy the files from your **gh-pages** branch to GitHub Pages:

- From the **main** branch, go to **settings > pages**
- Set the **Build and deployment** settings to **Deploy from a branch**, and point it to the **gh-pages** branch. Remember to save this change.
- Return to GitHub actions and confirm the **pages build and deployment** action ran successfully. If deployed successfully, you will be presented with your new GitHub Pages URL.
- Launch your generated URL and ensure it loads successfully. At this point it will not have a theme, but you should at least see content.

To add the theme for your deployed site:

- Edit the **hugo.toml** file in the **main** branch, and set the **baseURL** to your generated URL.
- Confirm the associated GitHub actions ran successfully.
- Refresh the published webpage and ensure the theme shows up successfully. Congratulations!

## Reflections on this project

I am happy I went through this process to create my new blog. It is very lightweight and fast, and I prefer to have full control over my hosting without needing to subscribe to a particular platform and/or pay for their services. I was able to learn about a new way to deploy a website, and I look forward to building out my blog and customizing my theme further. 

I hope you found this blog post useful!