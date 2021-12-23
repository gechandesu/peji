---
title: Quickstart
---

# Quickstart

[TOC]

## Installation options

### Via pip from PyPI

Just run:

```bash
pip install Peji
```

### Via setup.py

You should already have the Python `setuptools` package installed.

Clone repo:

```bash
git clone https://gitea.gch.icu/ge/peji.git
cd peji/
```

Run:

```bash
pip install .
```

pip automatically runs `setup.py` and install all dependencies.

## Command line interface

Pēji provides small command line interface.

App supports only two commands:

`create SITE`
:   Create new site in directory SITE. For example:

    ```
    peji create mysite
    ```

    In `mysite/` dir will be created standard file structure. See [Site structure](#site-structure) below.

`build`
:   Render HTML pages and place it with other static content into `mysite/build/` directory.

    You can choose specific directory instead of `build/` if pass `-d` (or `--dir`) option. For example, build site into `my_static_site/`:

    ```
    peji build -d my_static_site/
    ```

## Site structure

After creating site you have this site structure:

```
mysite/
├── config.yaml
├── layouts
│   ├── base.j2
│   └── index.j2
├── pages
└── themes
    └── default
        ├── css
        │   └── main.css
        ├── images
        └── js
```

There is:

config.yaml
:   Site configuration file. See more [here](/configuration.html).

layouts/
:   This folder contains Jinja2 templates. By default `base.j2` and `index.j2` is used.

pages/
:   Place your markdown files here.

themes/
:   Contains CSS, JS and images that need for page design.

build/
:   Generated HTML files. Creates after running `peji build`.

## Pages

### Page metadata.

Like many other static site generators and flat-file CMS, in Pēji metadata is required for Markdown files.

Metadata must be appended to the beginning of the markdown file and is surrounded by a triple minus sign at the beginning and end. Data are presented in YAML format. Example:

```yaml
---
title: My page title
layout: index.j2
theme: my_theme
---

# Your markdown text here
```

At the moment the application only supports these three properties. Consider each:

title
:   Page title. Is appended in HTML `<title></title>`.

    Default: No default value. This property is required.

layout
:   You can set custom template for specific page. Template file must be placed into `layouts/` directory.

    Default: `index.j2`

theme
:   Custom theme (CSS) for page. By default themes are placed into `themes/<theme_name>/`. In this property you only need to specify the `<theme_name>`, you don't need to specify the path.

    Default: `default`

## Templates (Layouts)

### Page variables

Page variables are passed to Jinja2 templates. Below is a description of each variable. A colon separated from the name of a variable indicates its type (see [Python Data Types](https://www.w3schools.com/python/python_datatypes.asp){target="_blank"}, [[Docs]](https://docs.python.org/3/library/datatypes.html){target="_blank"}).

theme: str
:   Page theme. Can be specified in page metadata. Otherwise, the value from `config.yaml` is used.

title: str
:   Required property, set in the page metadata.

site_title: str
:   Site title. Optional, set in `config.yaml` (named `title`). See [Configuration](/configuration.html#title-and-description).

description: str
:   See. [Configuration](/configuration.html#title-and-description).

menu: dict
:   Contains a dictionary where the key is the title of the link and the key value is the URL of the link. The data is filled from `config.yaml`'s `menu`.

content: str
:   This is a string containing HTML-converted Markdown text. In the template, this variable must be used with `safe` to avoid escaping HTML tags. Usage example:

    `{{ content | safe }}`
