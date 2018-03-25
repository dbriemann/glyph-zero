# glyph-zero

The origin template for all [glyph](https://github.com/dbriemann/glyph) powered blogs.

## Project Structure

```bash
├── config.toml
├── docs
│   └── _config.yml
├── LICENSE
├── Makefile
├── README.md
└── themes
    └── default
        ├── config.toml
        ├── index.mustache
        ├── issue.mustache
        ├── layout.mustache
        ├── style.css
        ├── tachyons.css
        └── tachyons.min.css
```

## Setup

1. Install [glyph](https://github.com/dbriemann/glyph). Make sure it's in your path.
2. Fork this repository.
3. Rename your new repository to e.g. "blog". Your Github pages address will be `<user>.github.io/<repo>`.
4. Enable Github pages via the repository settings. Make sure you choose `master branch /docs folder`. This is currently the only option that [glyph](https://github.com/dbriemann/glyph) accepts.
5. Clone your repository to your hard disk.
6. Edit the site's `config.toml` and the theme's `config.toml`. The files are documented and should be easy to understand.

Congratulations you set up everything. This step was a one time thing. Now build your blog for the first time by reading the Usage section.

## Usage

Build the site at any time by running `make blog` or `glyph` directly. Remember that [glyph](https://github.com/dbriemann/glyph) needs to be in your path. With `make clean` you can clean all exported files (in the `docs` folder). Usually you won't need to do this.

After building your site don't forget to add your docs folder to git and push to github.

If you just built your blog for the first time go visit `<user>.github.io/<repo>` and after a short while you should see the raw skeleton of your blog without any posts (we will call them issues from now on).

## Creating Themes
