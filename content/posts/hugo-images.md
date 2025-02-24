---
title: "Hugo - Fixing broken image links"
date: 2025-02-23
draft: false
---

## My Hugo images were broken!

Quick update for today, with another Hugo tip. As I have worked with markdown before, specifically while managing Wikis in Azure DevOps and GitHub, I simply created a subdirectory within my repository in the same area as the markdown files for my articles, and then pointed to my image files using the typical syntax of ```![alt text](imagelink)```. When building my site within Hugo, it even properly ported these image files into the **public** site files, however no matter what I did, my links were broken.

Naturally, I went down the more complicated rabbit whole for way too long. Based on research, I tried some of the following solutions.

- I learned that Hugo will naturally point to the **static/images** folder for the image files. I copied my stack of images to that folder.
  - Hugo documentation states that these should be referenced in your mardown using ```images/...```. I did this, no dice.
  - I updated my image mapping to specifically point to ```static\images...```, still no dice.
- I added an additional parameter within my hugo.toml file: ```imageDir = "images"``` to try and make a static reference, and then make an update within the **single.html** file (the template used for blog posts) similar to below. Still nothing.

![single-html-image-directory-map-fail](/techblog/images/customize-hugo/single-html-image-directory-map-fail.png)

At this point, I deleted the static mappings from the last step as not to screw up anything in the future. 

## The solution!

Then I thought, wait a minute! My content is posted on github pages. Like any other website, I should be pointing to where the images are hosted online, not where they are hosted locally (Duh!). With a little research, it looks like images hosted within the same Github repo as the pages are hosted from should start with a reference to the repository. In my case, my repository is called **techblog** so my image reference will need to look like this:

```![single-html-image-directory-map-fail](/techblog/images/customize-hugo/single-html-image-directory-map-fail.png)```

**Note**: The reference above is for the link referenced in this article. Circular logic is the best!

You should immediately see the reference while using checking locally using hugo (```hugo server -D --disableFastRender```), and have the images show on your live website once you sync the updates back to Github and the action takes place to publish the update to Github pages.

## Learnings

Put simply, keep it simple! To be fair, I am not a web developer by trade. As with the case normally though, the solution is normally more simple than an over-thinker like me typically thinks it is.