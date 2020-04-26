# JSON tag format specifications

## Grammar
The following grammar is represented as a context-free grammar (albeit not with much rigor).

- *Tag* represents a tag file: this file must be a JSON and its name has to be all lowercase and contain no spaces or have special characters.
- Elements that are represented within code blocks (e.g. `{`) indicate symbols that have to appear as is in the file.
- Elements that are written in italic (e.g. *TagName*) indicate elements that are later defined in the grammar.
- Elements between curly brackets ({} - **not** `{}`) indicate elements that can be omitted.
- Elements between square brackets ([] - **not** `[]`) indicate sentences in natural language that describe a set of possible tokens.
- Whitespace declaration is omitted, but can appear whenever as per JSON rules. Use an online JSON linter to ensure your JSON is valid.

### Generic tag grammar

*Tag*<br />
&nbsp;&nbsp;&nbsp;&nbsp;`{` *GenericLoader* `,` {*Conditions* `,`} *TagName* `,` {*TagColor* `,`} *Targets* `}`

*GenericLoader*<br />
&nbsp;&nbsp;&nbsp;&nbsp;`"loader": "prjtags:tag"`

*Conditions*<br />
&nbsp;&nbsp;&nbsp;&nbsp;`"conditions": [` [zero, one, or more *Condition* followed by `,` except the last] `]`

*Condition*<br />
&nbsp;&nbsp;&nbsp;&nbsp;`{` [a condition object, structure depends on the specific condition desired, see examples] `}`

*TagName*<br />
&nbsp;&nbsp;&nbsp;&nbsp;`"tag": "` [any string you choose: must be at least two characters long and have only lowercase letters from a to z and `_`] `"`

*TagColor*<br />
&nbsp;&nbsp;&nbsp;&nbsp;`"color": ` *ColorString*

*ColorString*<br />
&nbsp;&nbsp;&nbsp;&nbsp;[one of `"black"`, `"dark_blue"`, `"dark_green"`, `"dark_aqua"`, `"dark_red"`, `"dark_purple"`, `"gold"`, `"gray"`, `"dark_gray"`, `"blue"`, `"green"`, `"aqua"`, `"red"`, `"light_purple"`, `"yellow`", `"white"`]

*Targets*<br />
&nbsp;&nbsp;&nbsp;&nbsp;`"targets": [` [one or more *Target* followed by `,` except the last] `]`

*Target*<br />
&nbsp;&nbsp;&nbsp;&nbsp;[either a *DymmTarget* or a *StringTarget*]

*DymmTarget*<br />
&nbsp;&nbsp;&nbsp;&nbsp;`{` [a target object, structure depends on the specific considered target] `}`

*StringTarget*<br />
&nbsp;&nbsp;&nbsp;&nbsp;[either a *PlainString*, an *OreString*, or a *TagString*]

*PlainString*<br />
&nbsp;&nbsp;&nbsp;&nbsp;[either a *WildcardString* or a *ExactMetadataString*]

*WildcardString*<br />
&nbsp;&nbsp;&nbsp;&nbsp;`"` *ItemNameString* `:*"`

*ExactMetadataString*<br />
&nbsp;&nbsp;&nbsp;&nbsp;`"` *ItemNameString* {`:` [a positive number representing metadata]} `"`

*ItemNameString*<br />
&nbsp;&nbsp;&nbsp;&nbsp;[the registry name of the target item, e.g. `minecraft:wheat_seeds` for the seeds]

*OreString*<br />
&nbsp;&nbsp;&nbsp;&nbsp;`"@` [the name of the ore dictionary entry you want to target] `"`

*TagString*<br />
&nbsp;&nbsp;&nbsp;&nbsp;`"#` [the name of the tag you want to target - note that this refers to the 1.14.4 concept of tags, not this mod's one] `"`

### Tag removal Grammar

*Tag*<br />
&nbsp;&nbsp;&nbsp;&nbsp;`{` *RemovalLoader* `,` {*Conditions* `,`} [either a *TagName*, a *Targets*, or both] `}`

*RemovalLoader*<br />
&nbsp;&nbsp;&nbsp;&nbsp;`"loader": "prjtags:remove"`

For *Conditions*, *TagName*, *Targets* refer to the Generic tag grammar

## Conditions
The conditions that are added by Project T.A.G.S. are the following:

### `prjtags:slug`
Loads the tag only if the pack slug configured in the configuration matches one of the `slugs` defined in the condition

The structure is as follows:

```
{
  "type": "prjtags:slug",
  "slugs": // either a string representing the only slug or an array of string representing the possible slugs
}
```

### `prjtags:mc`
Loads the tag only if the minecraft version matches the one specified in the `version` field of the condition.

The structure is as follows:

```
{
  "type": "prjtags:mc",
  "version": "1.12.2"
}
```

## Example generic tag that shows all features

```json
{
  "loader": "prjtags:tag",
  "conditions": [
    {
      "type": "prjtags:slug",
      "slugs": [
        "enigmatica2expert",
        "projectozone3"
      ]
    }
  ]
  "tag": "early_game",
  "color": "red",
  "targets": [
    "minecraft:anvil:1",
    "minecraft:dye:*",
    "minecraft:wheat_seeds",
    "#forge:ingots/iron",
    "@logWood"
  ]
}
```
