# Nord for Firefox

Dark Firefox theme with the [Nord](https://www.nordtheme.com) palette, as used
for the desktop in [dotfiles](https://github.com/karasibille/dotfiles)
(`config/xrdb/colors/nord`): the same roles as there, so Firefox matches the
terminal, rofi and dunst. Sibling of
[firefox-laser](https://github.com/karasibille/firefox-laser).

## Colors

| Firefox key                                              | Color     | Nord     |
|----------------------------------------------------------|-----------|----------|
| `frame`, `popup`                                         | `#2e3440` | nord0    |
| `toolbar`                                                | `#3b4252` | nord1    |
| `toolbar_field`                                          | `#4c566a` | nord3    |
| `toolbar_text`, `toolbar_field_text`, `popup_text`       | `#d8dee9` | nord4    |
| `tab_background_text`, `tab_line`, `tab_loading`, `toolbar_field_highlight` | `#b48ead` | nord15 |
| `toolbar_bottom_separator`, `toolbar_vertical_separator` | `#bf616a` | nord11   |

nord15 is the accent of the desktop theme, nord11 the border of the focused
window, nord3 the selection.

## Try it

In Firefox, open `about:debugging#/runtime/this-firefox`, then
**Load Temporary Add-on…** and pick `manifest.json`. The theme stays until
Firefox restarts.

## Build

```sh
npx web-ext lint     # the checks addons.mozilla.org runs on upload
npx web-ext build    # web-ext-artifacts/nord-<version>.zip
```

`web-ext-config.mjs` keeps the README and the license out of the package.
The CI runs both on every push and keeps the package as the `nord-xpi`
artifact of the run.

## Release

The first version is submitted by hand on
[addons.mozilla.org](https://addons.mozilla.org/developers/addon/submit/),
which asks for the listing details (name, category, license). After that,
raise `version` in `manifest.json`, commit, then push a tag with that
version:

```sh
git tag v1.1 && git push origin v1.1
```

The release workflow checks that the tag matches the manifest, lints and
builds the theme, submits it to addons.mozilla.org as a new listed version
(AMO reviews it, the workflow does not wait), and creates a GitHub release
with `nord-<version>.xpi`. It needs an AMO API key
([addons.mozilla.org/developers/addon/api/key](https://addons.mozilla.org/developers/addon/api/key/))
in the repository secrets `AMO_JWT_ISSUER` and `AMO_JWT_SECRET`.

The add-on ID in `browser_specific_settings` must stay the same, or AMO
treats the upload as another add-on.

## License

The theme is under [CC BY 3.0](LICENSE). The Nord palette is by Arctic Ice
Studio and Sven Greb, under the MIT license.
