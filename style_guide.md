# Base17 Style System
**Version 0.9-beta**

*The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119).*

<!-- MarkdownTOC levels="2,3,4" autolink="true" -->

- [The Palette](#the-palette)
- [The Default 16 Slots](#the-default-16-slots)
  - [More about Slots](#more-about-slots)
  - [Customize Syntax Highlighting](#customize-syntax-highlighting)
- [Compatibility with Base16](#compatibility-with-base16)
  - [How to Upgrade from Base16](#how-to-upgrade-from-base16)
- [Addendums](#addendums)
  - [You are still limited to a max of 16 colors.](#you-are-still-limited-to-a-max-of-16-colors)
  - [Issues that Base17 attempts to solve](#issues-that-base17-attempts-to-solve)
    - [Sameness](#sameness)
    - [Semantic Pairing](#semantic-pairing)
- [Examples](#examples)
  - [skittles.yaml](#skittlesyaml)

<!-- /MarkdownTOC -->


## The Palette

The Base17 palette consists of 16 colors - an 8 shade gradient ramp for foreground/background and UI plus 8 accent colors for syntax highlighting.  The accent colors for a Base17 scheme should strive to be pleasing and visualy distinctive. Designers may chose any accent colours they desire - in any order. Slots in the palette _purposely_ do not correspond to particular hues. Schemes that all share similar hues results in [sameness](#sameness).

When syntax highlighting certain language constructs are attached to a particular palette "slot" by default (see the table below). For example literals (numbers, booleans, etc) are attached to slot `base09` and will inherit their color from that slot. This inheritance can be changed using [schema:override](./schema_spec.md#override).

Describing syntax highlighting can be tricky - please see [base17-vim](https://github.com/base16-project/base16-vim/), [base17-emacs](https://github.com/base16-project/base16-emacs/), and [base17-highlightjs]() for some real-life examples. It should be noted that each editor will have it's own idiosyncrasies due to having different syntax highlighting engines.



**Guidelines**

- Slots `base00` to `base07` typically capture a wide gradient of a single hue. These slots are used for foreground and background, status bars, line highlighting and such.
	- For a dark scheme, these slots typically span from darkest to lightest. (`base00` is the darkest)
	- For a light scheme, these slots typically span from lightest to darkest. (`base00` is the lightest)
- Slots `base08` to `base0F` typically hold individual accent colors used for syntax highlighting (types, operators, classes, variables, etc.)


## The Default 16 Slots

The default slots, their intended use, and the built-in slots they fill by default (their semantic meaning).


| Slot       | Usage  | Fills named slots by default... |
| :-- | :-- | :-- |
| _base00_ | Default BG  | `background` |
| _base01_ | Lighter BG | `bg_lighter`, `folding_marks`, `line_numbers`, `light_status_bar` |
| _base02_ | ????? BG | `bg_selection`, `bg_?????` |
| _base03_ | Brighest BG | `bg_brightest`, `comment`, `invisible`, `line_highlighting` |
| _base04_ | Dark FG | `fg_darker`, `dark_status_bar` |
| _base05_ | Default FG | `foreground`, `caret`, `delimiter`, `operator` |
| _base06_ | Light FG | `fg_lighter` |
| _base07_ | Brightest FG | `fg_brightest` |
| _base08_ | Syntax | `variable`, `xml_tag`, `markup_link_text`, `markup_list`, `diff_deleted` |
| _base09_ | Syntax | `literal`, `constant`, `xml_attribute`, `markup_link_url` |
| _base0A_ | Syntax | `name_class`, `markup_bold`, `bg_search_text` |
| _base0B_ | Syntax | `string`, `name_class_inherited`, `markup_code`, `diff_inserted` |
| _base0C_ | Syntax | `support`, `regex`, `escape`, `markup_quotes` |
| _base0D_ | Syntax | `function`, `attribute_id`, `heading` |
| _base0E_ | Syntax | `keyword`, `storage`, `selector`, `markup_italic`, `diff_changed` |
| _base0F_ | Syntax | `deprecated`, `embed_tags` |


### More about Slots

- every scheme MUST assign all 16 default Base slots
- older templates may only support the default slots (named could be ignored)
- variable slots may always be used (even with older templates)
- the value of a slot may be a literal hex color value or a reference to another slot.  See the [schema:slot values](./scheme_spec.md#slot_values).
- _variable slots_ make schemes easier to author and maintain.  See the [schema:variable slots](./scheme_spec.md#variable_slots).


### Customize Syntax Highlighting

**Don't let a single use case for a slot dictate that slots color.**

Notice that `base08` by default fills `diff_deleted`.  Red is a popular shade for deletions.  Perhaps you're tempted to make `base08` red.  Pause first and ask: _Do you ALSO want variables, XML tags, markup link text, and markup lists to be red as well?_  Often the answer is _no_.

This problem is easily solved:

```yaml
# assuming we've defined $blue and $red variables
base08: $blue
diff_deleted: $red
```

Now _only deleted diffs will appear red_, the other uses of base08 will be blue.


## Compatibility with Base16

Base17 is an evolution of Chris's [Base16 v0.2 spec](https://github.com/chriskempson/base16/blob/main/styling.md).  It still includes 16 colors.

- Base16 schemes are not compatible Base17.
- Base16 schemes take only a moment to upgrade to Base17. See [How to Upgrade](#upgrade).
- Modern builders can often build a mixed folder of Base16 and Base17 schemes without issue.

**Changes**

- Adds [description](./schema_spec.md#metadata) metadata
- Adds [system](./schema_spec.md#metadata) metadata
- Adds [semantic slots](./schema_spec.md#semantic)
- Adds [variables](./schema_spec.md#variables)
- Moves palette data into [palette key](./schema_spec.md#palette)

### How to Upgrade from Base16

- rename the `scheme:` key to `name:`
- add a `system:` key set to `base17`
- add an optional `description:` entry
- move all your `base00` keys under the new `palette` key


**Base16 (before):**

```yaml
scheme: "Ashes"
author: "Jannik Siebert (https://github.com/janniks)"
base00: "1C2023" # ----
base01: "393F45" # ---
base02: "565E65" # --
base03: "747C84" # -
# etc...
```

**Base17 (after):**

```yaml
name: "Ashes"
description: "you can now add a description"
author: "Jannik Siebert (https://github.com/janniks)"
system: "base17"
palette:
  base00: "1C2023" # ----
  base01: "393F45" # ---
  base02: "565E65" # --
  base03: "747C84" # -
  # etc...
```


<!--

Schemes MAY customize highlighting to precisely fine tune how their palette will be applied inside applications.  For example if you don't desire variable names and xml tags to share the same coloration (slot `base08`) then you can use the `name_variable` and `xml_tag` built-in slots to specify different colors.
-->

<!--

**Foreground / Background**

- `background` - `base00` by default
- `bg_lighter` - `base01` by default
- `bg_????` - `base02` by default
- `bg_brightest` - `base03` by default
- `fg_darker` - `base04` by default
- `foreground` - `base05` by default
- `fg_lighter` - `base06` by default
- `fg_brightest` - `base07` by default


**UI**

- `bg_selection` - `base02` by default
- `bg_line_highlight` - `base03` by default
- `bg_search_text` - `base0A` by default
- `dark_status_bar` - `base04` by default
- `light_status_bar` - `base01` by default
- `caret` - `base05` by default
- `folding_marks` - `base01` by default

**Diff**

- `diff_inserted` - `base0B` by default
- `diff_changed` - `base0E` by default
- `diff_deleted` - `base08` by default

**Markup**

- `markup_link_text` - `base08` by default
- `markup_link_url` - `base09` by default
- `markup_list` - `base08` by default
- `markup_code` - `base0B` by default
- `markup_italic` - `base0E` by default
- `markup_bold` - `base0A` by default
- `markup_quoted` - `base0C` by default

**Editor / Source**

- `delimiter` - `base05` by default
- `operator` - `base05` by default
- `comment` - `base03` (as a FG color) by default
- `invisibles` - `base03` (as foreground) by default
- `name_class` - `base0A` by default
- `name_class_inherited` - `base0B` by default
- `name_function` - `base0D` by default
- `name_support` - `base0C` by default
- `name_variable` - `base08` by default
- `xml_tag` - `base08` by default
- `xml_attribute` - `base09` by default
- `embed_tag` - `base0F` by default
- `constant` - `base09` by default
- `number` - `base09` by default
- `boolean` - `base09` by default
- `string` - `base0B` by default
- `regex` - `base0C` by default
- `escape_chars` - `base0C` by default
- `attribute_id` - `base0D` by default
- `heading` - `base0D` by default
- `keyword` - `base0E` by default
- `storage` - `base0E` by default
- `selector` - `base0E` by default
- `deprecated` - `base0F` by default

-->



## Addendums

### You are still limited to a max of 16 colors.

The number of colors per scheme is still limited to 16.  If your scheme uses more than 16 unique hex colors an error will be thrown during the build process.


### Issues that Base17 attempts to solve

Base16 is pretty darn awesome at what it's managed to accomplish, but it's not without it's issues.

#### Sameness

Too often Base16 hues [stick frustratingly close the default scheme hues](https://github.com/base16-project/base16/issues/10#issuecomment-1171593477).  We imagine this may be because many designers start with the default palette as a base. This could also be influenced by semantic pairing.  The end result: a lot of themes look visually similar and there is less diversity in Base16 schemes than you find in other theming ecosystems.

_Base17 has no default scheme and explicitly discourages designers from trying to hue match other scheme palettes._  Semantic slots may hue align occasionally due to common conventions (using red for diff deleted, etc).  This is OK.


#### Semantic Pairing

Base16 calls this "Rigid syntax highlighting" and lists it as a benefit.  It's definitely rigid.  This spec disagrees strongly that it's a benefit.

With Base16 `base08` is used for both variables and diff deleted.  If you want deleted lines in diffs to be colored red you're stuck with red variables also, nothing you can do.  [Base16 themes include a lot of red variables.](https://github.com/base16-project/base16/issues/10)  This also entirely breaks the fidelity of some themes (like Nord) that are ported from richer ecosystems without such restrictions.

_Base17 allows you to override any default pairings and easily define two colors._ Variables blue, diff deleted red, you got it.


## Examples

### skittles.yaml

```yaml
name: "Skittles (dark)"
author: "Josh Goebel"
description: "Looks as good as it tastes."

variables: # skittles
  $lemon: "#D7CA04"
  $orange: "#EE641C"
  $grape: "#6D5473"
  $raspberry: "#05538B"
  $strawberry: "#9A1518"
  $green_apple: "#28B109"
  $pineapple_passion: "#0098CB"
  $stawberry_starfruit: "#DD7EB2"

# adjust the default highlighting just a bit
# make sure diff is always green/red
override:
  diff_inserted: $green_apple
  diff_changed: fg_darker
  diff_deleted: $strawberry

palette: # bg/fg/ui
  base00: "#1C2023" # ----
  base01: "#393F45" # ---
  base02: "#565E65" # --
  base03: "#747C84" # -
  base04: "#ADB3BA" # +
  base05: "#C7CCD1" # ++
  base06: "#DFE2E5" # +++
  base07: "#F3F4F5" # ++++
  # accents
  base08: $strawberry
  base09: $orange
  base0A: $lemon
  base0B: $green_apple
  base0C: $pineapple_passion
  base0D: $raspberry
  base0E: $strawberry_starfruit
  base0F: $grape
```

