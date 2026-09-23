# Alexander Seda Personal Site

Source code for [alexanderseda.com](https://alexanderseda.com/), a personal website built with [Hugo](https://gohugo.io/). The site contains an about page, writing, and project pages covering software engineering, technology, faith, and other interests.

## Tech stack

- [Hugo](https://gohugo.io/) Extended
- [Congo](https://jpanther.github.io/congo/) Hugo theme
- Go modules for theme management
- Markdown content with TOML front matter

## Prerequisites

- Hugo Extended
- Go, for resolving the Hugo theme module

The repository currently uses Hugo `0.166.0` and Go `1.26.1` in `go.mod`. Earlier compatible versions may work, but matching these versions is recommended for reproducible builds.

## Local development

Clone the repository and start Hugo's development server:

```sh
git clone https://github.com/Alex-Seda/personal-site-hugo.git
cd personal-site-hugo
hugo server
```

Open [http://localhost:1313](http://localhost:1313) in a browser. Hugo automatically reloads the site when content, configuration, or asset files change.

To include draft content while developing:

```sh
hugo server --buildDrafts
```

## Building the site

Generate the production site in `public/`:

```sh
hugo
```

For a minified production build:

```sh
hugo --minify
```

The `public/` and `resources/` directories are generated build artifacts and are intentionally ignored by Git.

## Project structure

```text
.
├── archetypes/       # Templates used when creating new content
├── assets/           # CSS, images, and other processed assets
├── config/           # Hugo site, language, menu, module, and parameter configuration
├── content/
│   ├── about/        # About page
│   ├── posts/        # Written posts
│   └── projects/     # Project pages
├── layouts/          # Site layout overrides and partials
├── static/           # Files copied directly to the generated site
├── go.mod            # Hugo module and theme dependency
└── go.sum            # Dependency checksums
```

## Creating content

Create a new post with the default archetype:

```sh
hugo new content/posts/my-new-post/index.md
```

Create a project page similarly:

```sh
hugo new content/projects/my-project/index.md
```

New content is created as a draft. Set `draft = false` in its front matter when it is ready to publish.

## Configuration

The main site configuration lives in `config/_default/`. The site imports the Congo theme through `config/_default/module.toml`; Hugo resolves that dependency using the Go module files.

Common site settings are split across:

- `hugo.toml` for the base URL, outputs, pagination, privacy, and services
- `languages.en.toml` for language metadata and the site title
- `menus.en.toml` for navigation
- `params.toml` for appearance, search, image, and theme settings

## License

This repository contains personal site content and assets. Unless otherwise noted, the content and original assets are not licensed for reuse.
