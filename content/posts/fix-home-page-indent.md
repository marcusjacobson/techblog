---
title: "Hugo - Fix home page indentation"
date: 2025-02-23
draft: false
---

## The issue

As part of the Ananke theme for Hugo, the home page by default displays the most current blog posts. This is what I was looking for, and the main reason I chose this theme for the ss. As with the main page for any section, the home page uses a **_index.md** page in the root of the **content** folder, which is empty by default other than the headers. This is because the main purpose for this theme is to be used as a blog.

However, instead of just having my home page display a blog, I also wanted it to have a brief introduction for the site as a whole, since I am publishing more than just a blog. If I edit the **_index.md** file with some text, it does not appear aligned to the Recent blog posts section:

![home-page-bad-indentation](/techblog/images/customize-hugo/home-page-bad-indentation.png).

Being the OCD person that I am, I wanted to make sure these were aligned.

## Adjusting the alignment

The template for the home page is located at **themes/ananke/layout/index.html**. Since I like the alignment of the **Recent blog posts** section, I want to copy that format to the format of the article body.

The default look for this page is:

```
{{ define "main" }}
  <article class="cf ph4 pv3 pv4-1 f4 tl measure-wide center lh-copy {{ $.Param "text_color" | default "mid-gray" }}">
    {{ .Content }}
  </article>
    
    {{/* Define a section to pull recent posts from. For Hugo 0.20 this will default to the section with the most number of pages. */}}
    {{ $mainSections := .Site.Params.mainSections | default (slice "post") }}
    {{ $show_recent_posts := site.Params.ananke.show_recent_posts }}
    
    {{/* Check to see if the section is defined for ranging through it */}}
    {{range ($mainSections)}}
    {{/* Derive the section name  */}}
    {{ $section_name := . }}
    {{/* Create a variable with that section to use in multiple places. */}}
    {{ $section := where $.Site.RegularPages "Section" "in" $section_name }}
    {{ $section_count := len $section }}
    {{ if and ($show_recent_posts) (ge $section_count 1) }}
      <div class="pa3 pa4-ns w-100 w-70-ns center">
        {{/* Use $section_name to get the section title. Use "with" to only show it if it exists */}}
        {{ with $.Site.GetPage "section" $section_name }}
            <h1 class="flex-none">
              {{ $.Param "recent_copy" | default (i18n "recentTitle" .) }}
            </h1>
          {{ end }}

    ...additional code...
```

To fix the alignment, I copy the following value from the **$show_recent_posts** section to the **main** section: ```pa3 pa4-ns w-100 w-70-ns center```

The **main** section now appears as:

```
{{ define "main" }}
  <article class="cf pa3 pa4-ns w-100 w-70-ns center lh-copy {{ $.Param "text_color" | default "mid-gray" }}">
```

With this update, the two sections of the page are now perfectly aligned:

![home-page-bad-indentation](/techblog/images/customize-hugo/home-page-fixed-alignment.png).

## Now the font is mismatched...

I'm glad the alignment is resolved, but now the font sizes and color are mismatched to the Recent Blog posts below. Again, this is not OCD-friendly.

The fix for the font color was pretty simple, I just removed the ```{{ $.Param "text_color" | default "mid-gray" }``` definition for the **main** section, so it now looks like:

```
<article class="cf pa3 pa4-ns w-100 w-70-ns center lh-copy">
    {{ .Content }}
```

At this point, the only remaining issue is that the headers are not the same.

![home-page-bad-indentation](/techblog/images/customize-hugo/home-page-fixed-font.png).

Again, the fix for this is pretty simple. Within **_index.md** I change the formatting of the first header from **##** (proper syntax for Markdown, when a main header is already defined) to **#**. I get a warning in VS Code since it is does not confirm to the Markdown best practices, but hey, at least my site looks good now!

![home-page-bad-indentation](/techblog/images/customize-hugo/home-page-fixed-header.png).

## Learnings

I learned more about how the Markdown files you use to easily build the pages work in tandem with the Ananke layouts. While it is nice to be able to code the pages easily using Markdown, times will come where you need to fine-tune the HTML (or perhaps CSS), so it was good to get exposure to this.