# Learning Jekyll

These are my notes from _learning_ how to use _Jekyll_.

I'm specifically focusing on using Jekyll with GitHub Pages, so I'm only interested in doing things
in Jekyll that are supported natively by GitHub.

## Usage

```bash
export GEM_HOME="${HOME}/.gem"
gem install jekyll bundler
bundle install
bundle exec jekyll serve --livereload
```

## What Is Jekyll?

Jekyll is a static site generator written in Ruby. It was created by [Tom Preston-Werner](https://github.com/mojombo),
who also created GitHub (amongst other things). I'm gonna say it was the first mainstream static
site generator as it is almost 13 years old.

## GitHub Pages

GitHub Pages is the hosting service built into GitHub.

The typical workflow these days is to either build your site locally and push your `dist` folder to
a special branch (named `gh-pages` by convention), or to use GitHub Actions to do this whenever you
merge in some new changes.

GitHub Pages supports Jekyll natively, so you actually don't have to build anything yourself. You
can just push up your source code and GitHub will build it behind the scenes and serve your `_site`
folder automatically.

The downside to this approach is that you can only use [Jekyll plugins that GitHub supports](https://pages.github.com/versions).
GitHub does support quite a few, but they don't necessary support the latest versions of them.

## Themes

When using Jekyll outside of GitHub Pages, you can simply use Ruby Gems to install a theme. GitHub
Pages only supports [a handful of official Jekyll themes](https://pages.github.com/themes), but you
can use any theme hosted on GitHub by using the `remote_theme` property in your Jekyll configuration
file.

## Configuration

The [`_config.yml`](./_config.yml) file in the root of the repository is used to configure Jekyll
and also provide data to be used globally across the site (title, description, base href, domain
name, etc).

Any plugins you want to run at build time would be listed in this file, as well as your theme (if
any).

You can read the Jekyll configuration docs [here](https://jekyllrb.com/docs/configuration).

## HTML

Jekyll uses Shopify's [Liquid](https://shopify.github.io/liquid) templating language, which is
similar to Jinja. It's worth mentioning that you can use Liquid templating in your Sass and
CoffeeScript files as well.

## CSS

GitHub Pages uses the [`sass-converter`](https://github.com/jekyll/jekyll-sass-converter) plugin
automatically. Unfortunately, it uses an older version that doesn't support source maps.

Put all your partials in the `_sass` folder. When you import them into your main SCSS file, you'll
need to put frontmatter at the top of the file to instruct Jekyll to process it.

If you want to override a particular file from a theme, just create it in the same folder as the
theme. For example, [`_sass/minima.scss`](./_sass/minima.scss).

You can configure the output style using the `sass.style` setting in `_config.yml`.

## JavaScript

GitHub Pages uses the [`coffeescript`](https://github.com/jekyll/jekyll-coffeescript) plugin to
convert CoffeeScript to JavaScript.

Note that this plugin doesn't support CoffeeScript v2.

## Syntax Highlighting

Jekyll uses the [Rouge](https://github.com/rouge-ruby/rouge) syntax highlighter. In your theme,
you'll need to provide CSS classes. You can generate them with the command `rougify style github` to
get GitHub's color theme. You can also download [one of these](https://github.com/richleland/pygments-css).

## Arbitrary Data

You can put a YAML, JSON, or CSV file in the `_data` folder and reference it in your templates using
the `site.data` variable.

For example, you could access the file `_data/cats.yml` using the variable `site.data.cats`. Note
that Jekyll references the basename of the file, so don't put `cats.yml` and `cats.json` in the same
folder.

If you use a CSV file, then a header is required.

## Custom 404 Page

You can add a custom not found page by creating a `404.html` or `404.md` file. You can read more
[here](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-custom-404-page-for-your-github-pages-site).
