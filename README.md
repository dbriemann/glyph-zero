# glyph-zero

The origin template for all [glyph](https://github.com/dbriemann/glyph) powered blogs.

## Project Structure

```bash
├── config.toml					# contains all settings for Glyph
├── docs						# the export folder for Glyph, used by Github pages
├── LICENSE
├── Makefile					# commands for cleaning and building
├── README.md
└── themes						# folder containing all themes
    └── default					# the default theme used by Glyph
        ├── config.toml			# settings file for a theme
        ├── index.mustache		# template for the index page
        ├── issue.mustache		# template for the issue page (mandatory)
        ├── layout.mustache		# template for the site layout (frame for all other templates)
        ├── README.md			# contains info about contributors
        ├── style.css			# \
        ├── tachyons.css		#  > custom styling css
        └── tachyons.min.css	# /
    └── .. more themes
```

## Setup

1. Install [glyph](https://github.com/dbriemann/glyph). Make sure it's in your path.
2. Fork this repository.
3. Rename your new repository to e.g. "blog". Your Github pages address will be `https://<user>.github.io/<repo>`.
4. Enable Github pages via the repository settings. Make sure you choose `master branch /docs folder`. This is currently the only option that is compatible with [glyph](https://github.com/dbriemann/glyph).
5. Clone your repository to your hard disk.
6. Edit the site's `config.toml` and the theme's `config.toml`. The files are documented and should be easy to understand.

Congratulations you set up everything. This step was a one time thing. Now build your blog for the first time by reading the Usage section.

## Usage

Build the site at any time by running `make blog` or `glyph` directly. Remember that [glyph](https://github.com/dbriemann/glyph) needs to be in your path. With `make clean` you can clean all exported files (in the `docs` folder). Usually you won't need to do this.

After building your site don't forget to add your docs folder to git and commit & push to github.

If you just built your blog for the first time go visit `https://<user>.github.io/<repo>` and after a short while you should see the raw skeleton of your blog without any posts (we will call them issues from now on).

Writing issues is as simple as writing new issues in your Github repository. You just use the Github markdown editor directly or pre-write them locally and copy & paste them into a Github issue. When you are finished you run the build step locally and commit/push, done. Your new issue is live on your blog within about a minute.

## Creating Themes

You can just use the default theme provided by Glyph-Zero. How it looks can be seen on [my personal blog](https://dbriemann.github.io/blog/). If you don't like it or just want something entirely different, you should just create a new theme. The easiest way to do this is by copying the default theme and adjusting it to your needs.

Every theme consists of a directory in the themes folder and a few mandatory files (see Project Structure above). The name of the directory is the theme's name. Files that must exist for every theme are: 

- `README.md`: this file should contain the creator(s) and contributors of the theme plus any other information that is needed.
- `config.toml`: this file contains theme specific settings. Have a look at the config.toml of the default theme for a better understanding.
- `issue.mustache`: the only template file that is mandatory is the issue template. It determines how a single issue will look after rendering .

Glyph


