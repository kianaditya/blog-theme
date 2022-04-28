## Codex

A minimal blog theme built for [Hugo](https://gohugo.io/) 🍜

![Hugo desktop screenshot](/images/screenshot.png)

- An about page 👋🏻 and a blog 📝
- Blog posts can be tagged 🏷
- Mathematical notations are supported with KaTex 📐
- Sass/SCSS for styling ✨
- Support for Google Analytics 📈 and Disqus 💬
- i18n support

### Prerequisites

Hugo **extended version** (for Sass/SCSS support).

For macOS users, the extended version is installed by default if you use `homebrew`.

For Windows users, you can install with `choco`:
```
choco install hugo-extended -confirm
```

Note that this theme only supports Hugo version 82 and above.

### Getting started

~~At the root of your Hugo project, run:~~

```bash
git submodule add https://github.com/kianaditya/blog-theme.git themes/hugo-theme-codex
```

> **I am using hugo modules to pull in this theme for my blog repo**

Next, copy the contents of the [`exampleSite/config.toml`](https://github.com/kianaditya/blog-theme/blob/master/exampleSite/config.toml) to your site's `config.toml`. Make sure to read all the comments, as there a few nuances with Hugo themes that require some changes to that file.

The most important change you will need to make to the `config.toml` is removing [this line](https://github.com/kianaditya/blog-theme/blob/master/exampleSite/config.toml#L2):

```
themesDir = "../../"
```

It only exists in the example site so that the demo can function properly.

Finally, run:

```
hugo server -D
```

**Note: If you are seeing a blank page it is probably because you have nothing in your `content/` directory. Read on to fix that.**

### Configuring the Home Page

The site's home page can be configured by creating a `content/_index.md` file. This file can use the following frontmatter:

```md
---
heading: "Hi, I'm Codex"
subheading: "A minimal blog theme for hugo."
handle: "hugo-theme-codex"
---
```

If you would rather override the about page's layout with your own, you can do so by creating a `layouts/index.html`. You can find the `index.html` file that `hugo-theme-codex` uses [here](https://github.com/kianaditya/blog-theme/blob/master/layouts/index.html).

### Configuring Social Icons

Social Icons are optional. To show any of these icons, just provide the value in the `[params]` section of `config.toml`.

```toml
# config.toml

[params]
  twitter = "https://twitter.com/GoHugoIO"
  github = "https://github.com/kianaditya/blog-theme"
  # ...

  iconOrder = ["Twitter", "GitHub"]
```

If any of these options are given, `hugo-theme-codex` will render the social icon in the footer, using the order specified in `iconOrder`.

See the contents of the [example site](https://github.com/kianaditya/blog-theme/tree/master/exampleSite) for more details.

You can also create additional social icons by:
1. Adding your own SVGs in `static/svg/`, for example `static/svg/reddit.svg`.
2. Modifying your site's config as follows:
   ```toml
   [params]
      # ...
      reddit = "<url to your reddit>"

      iconOrder = ["Reddit"]
   ```

Make sure that the icon title must match the icon's file name. If the title contains more than one word, say "My Awesome Site",
you can use dash "-" for the icon name: `my-awesome-site.svg`.

### Creating a blog post

You can create a new blog post page by going to the root of your project and typing:

```
hugo new blog/:blog-post.md
```

Where `:blog-post.md` is the name of the file of your new post.

This will execute the theme's `blog` archetype to create a new markdown file in `contents/blog/:blog-post.md` with the following frontmatter:

```md
# Default post frontmatter:

# The title of your post. Default value is generated
# From the markdown filename
title: "{{ replace .TranslationBaseName "-" " " | title }}"
# The date the post was created
date: {{ .Date }}
# The post filename
slug: ""
# Post description used for seo
description: ""
# Post keywords used for seo
keywords: []
# If true, the blog post will not be included in static build
draft: true
# Categorize your post with tags
tags: []
# Uses math typesetting
math: false
# Includes a table of contents on screens >1024px
toc: false
```

The frontmatter above is the default for a new post, but all values can be changed.

### Configuring Table of Contents in blog posts

To display post title in Table of Contents in blog posts, set `showPageTitleInTOC`
to `true` in the `[params]` section of `config.toml`.

```toml
# config.toml

[params]
  # ...
  showPageTitleInTOC = true
```

### Adding a new section menu

In your site's `config.toml`, add a new menu definition for say, "photos":
```toml
# config.toml

[[menu.main]]
    identifier = "photos"
    name = "photos"
    title = "Photos"
    url = "/photos"
```

Then, put your posts under "content/photos".

### Custom styling

You have two options for custom styling. The first is to create an `assets/scss/custom.scss` in your project and put your custom styling there. For example, the snippet below changes the dot's color on your About page to blue:

```scss
// custom.scss
.fancy {
  color: #1e88e5;
}
```

You can even use Hugo variables/params in your custom styles too!

```scss
// custom.scss
.fancy {
  color: {{ .Site.Params.colors.fancy | default "#1e88e5" }}
}
```

```toml
# config.toml
[params.colors]
    fancy = "#f06292"
```

The second option is to use the supported scss overrides. You can do this by creating an `assets/scss/overrides/scss` file in your project. The following overrides are supported:

```scss
// overrides.scss

// The primary accent color used throughout the site
$primary: ''
```

### Tags

Right now `hugo-theme-codex` uses the `tags` taxonomy for blog posts. You can view all the blog posts of a given tag by going to `/tags/:tag-name`, where `:tag-name` is the name of your tag.

### i18n

Support for [`i18n`](https://gohugo.io/functions/i18n/#readout) is currently available for the following languages:

- English
- German

If you would like to have another language supported, create a post in the [Discussions](https://github.com/kianaditya/blog-theme/discussions) section of the repository. You may also support your language of choice by creating a `i18n/` directory in your project with a `.toml` file named after the language you are supporting.

There are not many UI-related strings to override in this theme. If you are looking to support a language of your own, refer to [the `i18n/en.toml` file](https://github.com/kianaditya/blog-theme/blob/a7800567242b6c7d3b4bd8b36dd329c3232faf5a/i18n/en.toml) to see which strings can be overridden.

### Favicon

To update favicon of the site, replace the one in `static/favicon.ico` with your own.