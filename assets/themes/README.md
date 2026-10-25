# Themes

This folder holds the data behind [THEMES.md](../../THEMES.md). Each theme has one YAML file in `themes.d`. The bot generates `THEMES.md` from those files with `THEMES.md.tmpl`, so do not edit `THEMES.md` by hand.

## Adding a theme

1. Copy `themes.d/_template.yaml` to `themes.d/<name>.yaml`. Use a lowercase, hyphenated name, for example `my-theme.yaml`.
2. Fill it in. The template has a comment above every field.
3. Open a pull request.

If you use an editor with YAML language server support, the first line of the file gives you completion and error hints from `schema.json`.

## Fields

| Field | Required | What it is |
| --- | --- | --- |
| `owners` | yes | GitHub handles of the people who maintain the file. At least one. |
| `name` | yes | Display name of the theme. |
| `author` | yes | Name of the author. |
| `repo` | yes | Link to the theme's repository. |
| `status` | yes | `listed` shows the theme in THEMES.md. `hidden` keeps it in the data only. |
| `variants` | yes | Versions of the theme. The first one is the default. Can be empty only if `requires_js` is `true`. |
| `author_url` | no | Link to the author's profile. |
| `website` | no | Link to the theme's website or demo. |
| `description` | no | A short description. |
| `note` | no | Something users should know first. |
| `requires_js` | no | `true` if the theme needs JavaScript or a plugin, so a CSS-only preview is not possible. |
| `screenshots` | no | List of screenshot links. |
| `settings` | no | Optional add-ons, see below. |
| `stale` | no | Set by the maintainers. Do not add it. |

Each variant has an `id`, a `name` and the `css` users paste into Jellyfin's Custom CSS. A variant can also set `settings` to change the default of a setting for that variant.

A setting has an `id`, a `label` and a `type`:

- `toggle` adds its `css` when switched on.
- `select` offers two or more `options`, each with a `value`, a `label` and optional `css`.
- `color` sets a CSS variable (`var`) to a color.
- `number` sets a CSS variable (`var`) to a number, with optional `min`, `max`, `step` and `unit`.

## Variants and settings

Variants are mutually exclusive versions of a theme, such as a light and a dark edition. A visitor uses exactly one of them.

Settings are optional add-ons on top of the chosen variant. A visitor can switch them on or change them in the preview site.

## What happens on the pull request

The bot posts a comment that shows your entry as it will appear in THEMES.md. It also runs checks:

- Blocking checks must pass before the pull request can be merged. Examples are schema errors and install CSS that cannot be reached.
- Warnings do not block. For example, a screenshot that does not load.

## The stale tag

The stale tag in THEMES.md marks themes that look unmaintained. The maintainers' stale scan sets it. Do not set it by hand.
