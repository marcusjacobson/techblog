---
title: "Hugo - Add taxonomy to sort blog posts"
date: 2025-02-23
draft: false
categories: ["Hugo"]
---

## The need to sort blog posts

As I have been adding more blog posts, I realized that I needed to start sorting them by category, to make finding relevant articles in the future easier. Fortunately, with a little research, the answer to this was pretty straightforward.

### Add a taxonomy section to hugo.toml

Within the **hugo.toml** file, I added the following section after **["params"]**:

```
[taxonomies]
  category = "categories"
  tag = "tags"
```

This gives me the option to do both categorization and add tags in the future. For now I just added categories, since I don't have a search functionality on my side. If I add search later though, having the option to implement tags will be helpful.

### Add a categories label to the posts

For each post, I then added a **categories** label in the top header section, similar to:

```
---
title: "Hugo - Add taxonomy to sort blog posts"
date: 2025-02-23
draft: false
categories: ["Hugo"]
---
```

### Add links to my Blog Posts page

To add the links to my Blog Posts page, I simply edited the **posts/_index.html** file with links for the categories I have so far. At this point, I just have one - Hugo, but I'll be adding more in the future.

While there are many different ways to format this, I chose to use a table format so the links appear left to right across the screen. I also added in some spacers within the table so the links have some white space between them.

```
Use the links below to navigate to articles on specific subjects:

|  |  |  |  |  |  |  |  |  |
|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|
| [Hugo & Ananke Theme](/categories/Hugo) |  |  |  |  | [*Future Subject*](/) |  |  |  |  | [*Future Subject*](/) |  |  |  |  | [*Future Subject*](/) |  |  |  |  | [*Future Subject*](/) |
```

to filter to the categories, use **/categores/[category_name]**

This makes the page look like this:

![blog-posts-category-links](/techblog/images/customize-hugo/blog-posts-category-links.png).

Clicking on the **Hugo & Ananke Theme** link brings up a page that looks like this:

![blog-category-page-hugo](/techblog/images/customize-hugo/blog-category-page-hugo.png).

I will likely work on customizing this page in the future, but for now I am happy that I got the categories working.

## Learnings

This was pretty simple to implement, since the taxonomies feature is built into Hugo. It would have been nice if it was enabled by default, but figuring out how to add it didn't take much work. From there, it was just customizing how I wanted to present the links to my blog categories.
