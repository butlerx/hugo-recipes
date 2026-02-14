# hugo-theme-recipes

A [Hugo](https://gohugo.io/) theme for managing a personal cookbook. Recipes are
written in Markdown with structured front matter for prep times, servings, and
tags. The theme generates Schema.org Recipe JSON-LD, Open Graph meta tags, a
fediverse creator tag, an RSS feed, and a PWA manifest out of the box.

## Features

- Recipe pages with stats bar (servings, prep time, cook/cool time)
- Tag-based categorisation with a recipe index on the homepage
- [Schema.org Recipe](https://schema.org/Recipe) structured data (JSON-LD)
- Open Graph meta tags (Mastodon, Bluesky, and other platforms)
- Fediverse creator tag for author attribution on Mastodon
- RSS feed with autodiscovery
- Progressive Web App (PWA) manifest with auto-generated icons
- Print stylesheet (hides nav and footer)
- Responsive, dark-themed design using modern CSS (no SCSS required)
- `img` shortcode for figures with optional caption, attribution, and links

## Quick Start

1. Install Hugo **v0.128.0 or later**. Any standard edition works — the extended
   version is not required. See the
   [Hugo Installation Guide](https://gohugo.io/getting-started/installing/).

2. Add the theme to your Hugo project:

   ```sh
   git submodule add https://github.com/butlerx/hugo-recipes themes/hugo-recipes
   ```

3. Configure your site (see [Site Configuration](#site-configuration) below).

4. Start the development server:

   ```sh
   hugo serve
   ```

   View your site at `http://localhost:1313/`.

A complete working example is included in the
[`exampleSite/`](exampleSite/) directory.

## Site Configuration

Add the following to your `hugo.toml` (or equivalent `config.toml` / `config.yaml`):

```toml
baseURL = "https://example.com/"
languageCode = "en-us"
title = "My Family Cookbook"
theme = "hugo-recipes"

[params]
  # Site description — used in meta tags, Open Graph, and the homepage blurb.
  description = "A collection of our favourite family recipes."

  # Theme colour — used for the browser toolbar, PWA manifest, and
  # apple-mobile-web-app-status-bar.
  theme = "#2d2d2d"

  [params.author]
    # Default author name — shown on recipe pages and in meta tags.
    # Can be overridden per-recipe in front matter.
    name = "Home Chef"

    # Fediverse handle — used for fediverse:creator meta tag (Mastodon, etc.).
    # Format: @username@instance.social
    fediverse = "@homechef@mastodon.social"

# Optional navigation menu links.
[[menus.main]]
  name = "About"
  url = "/about/"
  weight = 1

[[menus.main]]
  name = "Recipe Index"
  url = "/tags/"
  weight = 2
```

### Required Parameters

| Parameter             | Description                                            |
| --------------------- | ------------------------------------------------------ |
| `params.description`  | Site description for meta tags and the homepage         |
| `params.theme`        | Hex colour for browser chrome and PWA theme             |
| `params.author.name`  | Default author name for recipes and meta tags           |

### Optional Parameters

| Parameter                 | Description                                                    |
| ------------------------- | -------------------------------------------------------------- |
| `params.author.fediverse` | Fediverse handle for `fediverse:creator` meta tag (`@user@instance.social`) |

### Optional: Custom Icon

Place a PNG image at `assets/images/icon.png` (minimum 512×512px) in your site
to override the default theme icon. Hugo will automatically generate favicon,
Apple touch icon, and PWA icon sizes from it.

## Adding Recipes

Create a new recipe using the built-in archetype:

```sh
hugo new content my-recipe-name/index.md
```

This creates a page bundle at `content/my-recipe-name/` with the following front
matter:

```yaml
---
draft: true
title: My Recipe Name
author:              # Leave blank to use the site default
recipe_image:        # Filename of an image in the page bundle (e.g. "photo.jpg")
images: []           # List of image URLs for Open Graph / social sharing
date: 2025-01-01
tags: []             # e.g. [dinner, Italian, pasta]
servings: 4
prep_time: 15        # Numeric value
prep_increment: minutes  # "minutes" or "hours"
cook: true           # true = cooking time, false = cooling time
cook_increment: minutes  # "minutes" or "hours"
cook_time: 8         # Numeric value
---
```

### Front Matter Reference

| Field            | Type     | Default     | Description                                                       |
| ---------------- | -------- | ----------- | ----------------------------------------------------------------- |
| `title`          | string   | (from slug) | Recipe name                                                       |
| `author`         | string   | site author | Override the default author for this recipe                       |
| `date`           | date     | now         | Publication date                                                  |
| `draft`          | bool     | `true`      | Set to `false` to publish                                         |
| `tags`           | list     | `[]`        | Tags for categorisation (shown on recipe page and in the recipe index) |
| `servings`       | number   | `4`         | Number of servings                                                |
| `prep_time`      | number   | `15`        | Preparation time (numeric)                                        |
| `prep_increment` | string   | `minutes`   | Unit for prep time — `minutes` or `hours`                         |
| `cook`           | bool     | `true`      | `true` shows "Cooking Time", `false` shows "Cooling Time"         |
| `cook_time`      | number   | `8`         | Cook or cool time (numeric)                                       |
| `cook_increment` | string   | `minutes`   | Unit for cook time — `minutes` or `hours`                         |
| `recipe_image`   | string   |             | Filename of an image in the page bundle to display above the recipe |
| `images`         | list     | `[]`        | Image URLs for Open Graph and Schema.org                          |

### Adding Images to a Recipe

Recipes are [page bundles](https://gohugo.io/content-management/page-bundles/),
so images live alongside the content file:

```
content/
  my-recipe/
    index.md
    photo.jpg
```

Set `recipe_image: photo.jpg` in the front matter to display it at the top of
the recipe page.

For social sharing previews (Open Graph), add the image URL to
the `images` list:

```yaml
images:
  - photo.jpg
```

### Recipe Content Structure

Recipes should use `## Ingredients` and `## Directions` as the main headings.
Use `####` subheadings to group ingredients:

```markdown
## Ingredients

#### Sauce

- 400g tinned tomatoes
- 2 cloves garlic

#### Pasta

- 400g spaghetti

## Directions

1. Heat the oil in a pan
1. Add the garlic
   1. Cook until fragrant
1. Add the tomatoes
```

## Shortcodes

### `img`

A figure shortcode with support for captions, attribution, and links:

```markdown
{{</* img src="photo.jpg" alt="My dish" title="Plated dish" caption="Served with a side salad" */>}}
```

| Parameter  | Description                            |
| ---------- | -------------------------------------- |
| `src`      | Image source URL (required)            |
| `alt`      | Alt text (falls back to `caption`)     |
| `title`    | Figure title (shown as `<h4>`)         |
| `caption`  | Caption text below the image           |
| `class`    | CSS class on the `<figure>` element    |
| `link`     | Wraps the image in a link              |
| `attr`     | Attribution text                       |
| `attrlink` | URL for the attribution link           |
| `mouse`    | Tooltip text on hover                  |

## License

This theme is licensed under the
[MIT License](https://github.com/butlerx/hugo-recipes/blob/master/LICENSE).
