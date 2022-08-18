# BaseX Scheme Guide

An example BaseNext scheme:

### skittles.yaml

```yaml
scheme: "Skittles (dark)"
author: "Josh Goebel"

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
customize:
  diff_inserted: $green_apple
  diff_changed: fg_darker
  diff_deleted: $strawberry

default: # bg/fg/ui
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


### Slot Values

The value of a slot may be a literal hex color value or a reference to another slot.

 ```yaml
$red: "#ff0000"

constant: $red
string: "constant"
number: "constant"
boolean: "constant"
diff_deleted: $red

base05: "#fe0000"
```

- first we label the color `$red` with a variable
  - it's value is the literal color `#ff0000`
- we declare constants are red
- we declare strings, numbers, and booleans should be highlighted as constants
- we declare `diff_deleted` should be highlighted as `$red`
- we set `base05` to the literal hex color "#fe0000"


Note: Ordering does not matter, you can refer to a slot before that slot has been defined.


### Variable Slots

Variable slots make schemes easier to author and maintain. For example when your hues are visually distinct it's often helpful to reference them in your scheme by name:

```yaml
scheme: "Fun Colors"
$lightsaber_purple: "#FE00EF"
$granny_smith_red: "#EE1122"
$mr_blue_sky: "#336699"
base0b: $lightsaber_purple
base0c: $granny_smith_red
base0d: $mr_blue_sky
```

- all variable slot names must start with `$`
