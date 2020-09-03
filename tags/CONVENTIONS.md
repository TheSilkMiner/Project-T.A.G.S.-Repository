# Tag Conventions
To ensure common ground between all the modders that may want to write or use Project T.A.G.S., a set of conventions has been estabilished.
The following is a list of all the currently agreed upon conventions. If something is missing, feel free to drop by and discuss on Discord or open an issue about it.

**Conventions for pack-specific data** are given below.

## JSON Files Location
- The name of the JSON file should reflect the tag that is currently filling (e.g. `early_game.json` would specify items that fit in the `early_game` tag).
  If this isn't possible, then the file name should be as close as possible to the tag's name (e.g. `early_game_conditional.json`).
- The JSON should be located in a subdirectory representing the mod ID whose items are being targeted (e.g. `tconstruct` for Tinkers' Construct items, `minecraft` for vanilla).
- No JSON should identify items that are defined by a mod other than the one currently being considered (e.g. `tconstruct/weapons.json` cannot reference items outside Tinkers' Construct).
  The only exception is with NBT-based items (e.g. Patchouli books).

## Target Structure
- Metadata `0` shouldn't be specified explicitly in the targets (e.g. `minecraft:apple` should be preferred to `minecraft:apple:0`).
  On the other hand, if there's a list of more than one element with the same registry name, but different metadata, it is suggested to refer to the first item in the list as `name:0`.
- If a list has more than three elements, it is suggested to use either the metadata wildcard (`:*`) or the `dymm:item_meta_range` construct (see documentation).
- Minecraft Tags should generally be preferred to ore dictionary names (e.g. `#forge:ingots/iron` should be preferred to `@ingotIron`).

## Tag Naming
- Tag names should be written in `snake_case`: all lowercase, with multiple words separated using an underscore (namely `_`; e.g. `early_game` represents the tag named "Early Game").
- Common tag names should be preferred, rather than specific ones (e.g. `pipe` rather than `item_duct`).

## Tag Localization
- Every tag should have an American English localization (`en_us.json`); additional localizations should not be generated.
- Localizations should be written in `PascalCase`, in order to allow looking data up in JEI (e.g. `EarlyGame` rather than `Early Game`).

## Minecraft Versions
- Every tag should specify for which Minecraft version it is being written in its `conditions`. It is allowed to specify more than one target version via an OR condition (see documentation).
- It is suggested to have all tags apply for as many Minecraft versions as possible. Unknown items will automatically be skipped by the reader.

## Pack-Specific Tags
- Pack-specific JSON files should have a slug condition in their `conditions` block identifying the target pack or packs (see `prjtags:slug`).
- Pack-specific JSON files for tags should follow the same conventions as above, except for being located in a subdirectory of the target mod (e.g. `botania/project_ozone_3/expert.json`).
- Pack-specific tags should otherwise respect all the above conventions.
