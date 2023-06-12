# Contributing

## Using the Template

This template project <https://github.com/equinix-labs/equinix-labs-workshop> is used for creating consistent workshop experiences on Equinix Labs.

To create a new workshop, use the "Use this template" button on the project. Once you have your new project created, follow these steps:

1. Search and replace "equinix-labs-workshop" with the name of the GitHub repo you created when using the template.
2. Search and replace "Workshop: Equinix Labs" with the name of your workshop.
3. You'll want to enable GitHub Pages for the project:
   * Open <https://github.com/equinix-labs/equinix-labs-workshop/settings/pages> (this link works after following step 1)
   * Control who can view and access your site: Public
   * Source: Deploy from a branch
   * Branch: gh-pages /(root)
4. Update docs/index.md, the docs/part*.md files, and the markdown below for your workshop.
5. Remove this "Using the Template" section.

## Previewing Changes

```sh
pip install mkdocs mkdocs-material mkdocs-glightbox
mkdocs serve
```

## Publishing Changes

This project is published to GitHub Pages using GitHub Actions upon merge.

