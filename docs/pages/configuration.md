---
title: Configuration
---

Pēji provide simple configuration file in YAML format.

<details markdown="1">
<summary>Config example...</summary>
```yaml
# Site title.
title: Pēji
# Site meta description.
description: Stupidly simple static site generator.
# Site default theme.
theme: default
# Site menu.
menu:
    Home: /
    Quickstart: /quickstart.html
    Configuration: /configuration.html
    Download: /download.html
# Markdown extensions.
# See https://python-markdown.github.io/extensions/
markdown_extensions:
    - admonition
    - codehilite
    - extra
    - meta
    - toc
markdown_extension_configs:
    codehilite:
        noclasses: true
        use_pygments: true
        pygments_style: default
    toc:
        title: Table of contents
        toc_depth: 2-5
```
</details>

[TOC]

## Title and description

The **title** on each page looks like this:

```jinja2
# In browser:
page title | site title.
# In template (default layout):
{% block title %}{{ title }} | {{ site_title }}{% endblock %}
```

Of course, the view can be changed in the layout. Pēji will pass both values to the template.

The *page* title is specified in the markdown file metadata (See: [Page metadata](/quickstart.html#page-metadata)). The *site* title is set in the `config.yaml`. If `title` is not specified, it will be accepted as an empty string.

Site **description** in unused in default layout, but you can use it if you want. Also if `description` is not specified, it will be accepted as an empty string.

## Themes

A **theme** is just a collection of static JS, CSS, and images. Any code can be there, there are no restrictions.

To make it easier to "switch themes", each theme is located in its own folder inside `themes/`, for example:

```
themes
    ├── default
    │   ├── css
    │   ├── images
    │   └── js
    └── my_theme
        ├── css
        ├── images
        └── js
```

In the standard layout theme is connected in the `index.j2`, but it can be set in a layout that is convenient for you.

```jinja2
<link rel="stylesheet" href="/themes/{{ theme }}/css/main.css">
```

`config.yaml`  sets the default theme, which is used if a page does not have a theme specified in the metadata.