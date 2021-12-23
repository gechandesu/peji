---
title: Home
---

**Pēji** (Japanese: ページ, "page") is simple way to generate small static site like this site.

If you need to collect several pages from the Markdown, then Pēji are great for you.

!!! note "**Note**"
    Pēji is not intended to generate a blog site. Its single pages only. You can link pages with hyper-links, but you have to do it manually.

Features:

- [Python-Markdown](https://python-markdown.github.io/){target="_blank"} is used.
- Code syntax highlighting via [Pygments](https://pygments.org/){target="_blank"}.
- [Jinja2](https://jinja.palletsprojects.com/en/2.11.x/){target="_blank"} template engine.
- Custom style and layout for specific page.
- Site menu bar can be edited through the config.
- YAML config file.

## Installation and quickstart

Install Pēji globally or into virtual environment:

```bash
pip install Peji
```

Create your site:

```bash
peji create mysite
cd mysite/
```

Create your first page and place it into `mysite/pages/`:

`index.md`:

```markdown
---
title: My first page
---

# My heading

It works!
```

Build your site:

```
peji build
```

Site will be placed in `./mysite/build`.

Also you can run Python built-in HTTP Server:

```bash
python3 -m http.server --directory build/
```

## License

Pēji is released under The Unlicense. See [https://unlicense.org/](https://unlicense.org/){target="_blank"} for detais.