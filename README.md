# glyph-zero

The origin template for all [glyph](https://github.com/dbriemann/glyph) powered blogs.

## Project Structure

```bash
├── config.toml                 # contains all settings for glyph
├── docs                        # the export folder for glyph, used by Github pages
├── LICENSE
├── Makefile                    # commands for cleaning and building
├── README.md
└── themes                      # folder containing all themes
    └── default                 # the default theme used by glyph
        ├── config.toml         # settings file for a theme
        ├── index.mustache      # template for the index page
        ├── issue.mustache      # template for the issue page (mandatory)
        ├── layout.mustache     # template for the site layout (frame for all other templates)
        ├── README.md           # contains info about contributors
        ├── style.css           # \
        ├── tachyons.css        #  > custom styling css
        └── tachyons.min.css    # /
    └── .. more themes
```

## Setup

1. Install [glyph](https://github.com/dbriemann/glyph). Make sure it's in your path.
2. Fork this repository.
3. Rename your new repository to e.g. "blog". Your Github pages address will be `https://<user>.github.io/<repo>`.
4. Enable Github pages via the repository settings. Make sure you choose `master branch /docs folder`. This is currently the only option that is compatible with [glyph](https://github.com/dbriemann/glyph).
5. Clone your repository to your hard disk.
6. Edit the site's `config.toml` and the theme's `config.toml`. The files are documented and should be easy to understand.

Congratulations you set up everything. This step was a one time thing. Now build your blog for the first time. Instructions are in the Usage section.

## Usage

Build the site at any time by running `make blog` or `glyph` directly. Remember that [glyph](https://github.com/dbriemann/glyph) needs to be in your path. With `make clean` you can clean all exported files (in the `docs` folder). Usually you won't need to do this.

After building your site don't forget to add your docs folder to git and commit & push to github. 

If you just built your blog for the first time go visit `https://<user>.github.io/<repo>` and after a short while you should see the raw skeleton of your blog without any posts (we will call them issues from now on).

Writing issues is as simple as writing new issues in your Github repository. You just use the Github markdown editor directly or pre-write them locally and copy & paste them into a Github issue. When you are finished you run the build step locally and commit/push, done. Your new issue is live on your blog within about a minute.

Two important points you should know:

- The first paragraph of your issue is treated as summary for the blog post.
- If you want to _delete_ an issue, just close it and rebuild with glyph. Closed issues will not be exported to HTML. You should also run `make clean` before building to make sure the old file is gone.

## Creating Themes & Customizing

You can just use the default theme provided by glyph-zero. How it looks can be seen on [my personal blog](https://dbriemann.github.io/blog/). If you don't like it or just want something entirely different, you should just create a new theme. The easiest way to do this is by copying the default theme and adjusting it to your needs.

Every theme consists of a directory in the themes folder and a few mandatory files (see Project Structure above). The name of the directory is the theme's name. Files that must exist for every theme are: 

- `README.md`: this file should contain the creator(s) and contributors of the theme plus any other information that is needed.
- `config.toml`: this file contains theme specific settings. Have a look at the config.toml of the default theme for a better understanding.
- `issue.mustache`: the only template file that is mandatory is the issue template. It determines how a single issue will look after rendering .

glyph uses the [mustache](http://mustache.github.io/mustache.5.html) templating system to insert data into the final HTML pages. glyph lets you access the following data in your templates:

### Exports from config.toml

The data here is completely specified in `config.toml` and exported to the template rendering process by glyph.

```
[Site]
    Title       = string, # site/blog title
    Author      = string, # author's name
    OneLineDesc = string, # short description of the site's content
    Twitter     = string, # twitter handle (without @, e.g. john_doe)
    Mail        = string, # mail address for contact (public)
    Theme       = string  # theme name (assumes default if not specified)

[Repository]
    Users   =   []string, # all users that can author blog posts, "owner" must be the first user
    Name    =   string    # name of the repository

    # First user and repo name are integral parts of your repository URL:
    # https://github.com/<user>/<name>
    # and your Github pages URL:
    # https://<user>.github.io/<name>

    # Usually you will only provide 1 user.

Custom = dict[string]:generic # a dictionary that allows definition of custom key/value pairs
```

The `custom` attribute allows to export custom data from the config file to the template rendering process. There is a simple example included in `config.toml`.

### Issue Exports

The export of issues has two possible cases. For the `issue.mustache` template only the current Issue is exported:

```
Issue = Issue object # the issue that is rendered
```

whereas for all other templates all issues are exported:

```
Issues = []Issue # array of all issues
```

In any case a single `Issue` is defined as follows:

```
[Issue]
    Number      = int           # Github issue number (not id)
    Title       = string        # original issue title
    Link        = string        # slugified title
    Content     = string        # content of the issue in HTML
    Summary     = string        # first paragraph of Github Issue in HTML
    Labels      = []string      # all labels assigned to the issue on Github
    GithubLink  = string        # direct link to the issue (and to the comments)
    Created     = time.Time     # time of creation, type from Go standard library
```

### Theme Exports

These exports all come from the theme config file `config.toml` in the theme folder.

```
[Theme]
    Name            = string                # name of the template, must match directory name
    IndexTemplate   = Template              # the template used to render index.html
    IssueTemplate   = Template              # the template used to render a single issue
    OtherTemplates  = []Template            # the rest of the templates used in the theme
    Custom          = dict[string]:generic  # a dictionary that allows definition of custom key/value pairs
```

A single template is structured as follows:

```
    Source = string     # the source template file
    Layout = string     # the layout template file (optional)
                        # a layout acts like a frame for other templates
    Target = string     # the name of the target html file
```

### Utility Exports

```
Today = time.Time type from the Go standard library   # exports the time of building.
```

The Go `time.Time` type is documented [here](https://golang.org/pkg/time/#Time).
