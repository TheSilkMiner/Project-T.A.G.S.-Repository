# Project T.A.G.S. Repository
This is the official repository for Project T.A.G.S., hosting all the data to ensure a seamless experience across modpacks.

While forking is not prohibited, modpack developers are encouraged to contribute to this central repository via pull requests.

## Repository structure
### Root directory
The root directory must have a `tags` directory and a `lang` directory. Any other directories or files will be ignored by the mod.

### `tags` directory
The `tags` directory contains all the tags JSON files that will be read and loaded into the game. Non-JSON files are allowed, but they will be ignored by the mod itself.
The structure of the JSON files is fixed and follows the specifications that will be available in `tags/SPECS.md`.
Conventions on the way of naming tags and writing the respective JSON files are outlined in `tags/CONVENTIONS.md`.

### `lang` directory
The `lang` directory contains all the localization for the tags.
Differently from normal ContentTweaker and any other language files, these files are in JSON format, with the specification described in the text that follows.
This not only ensures a seamless transition to 1.14 and newer versions, but also allows easier conflict resolution in packs.
The file shall be named exactly like their `lang` counterpart, meaning `en_us.lang` becomes `en_us.json`.
The contents are described as a set of key-value pairs, where the key represents the translation key for the tag, while the value the corresponding name **without** the dash (`#`).

```json
{
  "key1": "value1",
  "key2": "value2",
  "key3": "value3",

  "keyn": "valuen"
}
```

The key is built in the following way: `prjtags.tag.<tag_name>.name`. `<tag_name>` should be replaced by the name of the tag.
E.g., if the tag name is `early_game`, the corresponding key will be `prjtags.tag.early_game.name`.



