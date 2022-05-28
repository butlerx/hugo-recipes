# hugo-theme-recipes

A theme for [Hugo](https://gohugo.io/) for managing a cookbook

## Quick Start

0. Install Hugo with your favorite package manager, or follow their
   [Installation Guide](https://gohugo.io/getting-started/installing/)
   - Note that the _extended_ version of Hugo is required since this theme needs
     SCSS support. At the time of writing, this is the version found by
     installing via
     [HomeBrew](https://github.com/Homebrew/homebrew-core/blob/master/Formula/hugo.rb)
     and the
     [Arch User Repository](https://www.archlinux.org/packages/community/x86_64/hugo/).
     If that isn't the case for your package manager, then install using
     `$ go install --tags extended` as documented in the Hugo Install Docs.
1. Add the repository into your Hugo Project repository as a submodule,
   `git submodule add https://github.com/butlerx/hugo-recipes themes/recipes`.
2. Configure your `config.toml` or `config.yaml`.
3. Build your site with `hugo serve` and see the result at
   `http://localhost:1313/`.

## Using this theme

### Add a new recipe draft

1. Navigate to the root directory of your website folder within a terminal
2. Type `hugo new name-of-your-new-recipe-here`, replacing
   `name-of-your-new-recipe-here` with the name of your recipe

- Note that the default template (archetype in Hugo vernacular) will replace the
  hypens in the provided name with spaces as the title and capitalize the first
  letter of each word. For example, if I were to enter the command
  `hugo new hot-dog`, I would find a new folder at `content/hot-dog`,
  and the title within the `index.md` file in that folder would be `Hot Dog`.

## License

Coder is licensed under the
[MIT license](https://github.com/butlerx/hugo-recipes/blob/master/LICENSE.md).
