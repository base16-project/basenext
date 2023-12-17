# Deprecation Notice

After forking from the original base16, we tried to decide what we wanted the "next generation" version of base16 to look like. Base17 was one of the early iterations. While we may end up going in this direction in the future, we have (currently) decided against this specific iteration. Over time, we plan to add a number of features to our "common scheme format" which would expand it to work like base17, but building it out iteratively rather than all at once.

# BaseNext DRAFT Proposal <img alt="Color wheel" src="./color_wheel.png" width="100" align="right" style="padding-top:0.6rem;">

This repository exists to allow rapid progress to be made on the BaseNext style guide... it may later be merged back into another central repo (or not).


### Motivation

[Base16](https://github.com/chriskempson/base16) is pretty darn awesome at what it's managed to accomplish, but it's not without fault.  BaseNext aims to be a forward-compatible evolution of Base16 that solves some of the known issues.


#### Compared to Base16

*What's the same*

- Same 16 color slots with the same _default_ semantic meanings.
- Same simple YAML schemes.
- Same simple mustache templating system.

*New and Improved*

- Way more control of syntax highlighting (you can now color a `variable` differently than `diff_deleted`)
- custom variables to make authoring schemes easier - allowing designers to describe a theme as they imagine in it in their mind (such as naming hues or UI concepts with no direct translation)
- support `is_light` and `is_dark` flags for templates (builder)


### Issues that BaseNext attempts to solve


#### Sameness

Too often Base16 hues [stick frustratingly close the default scheme hues](https://github.com/base16-project/base16/issues/10#issuecomment-1171593477).  We imagine this may be because many designers start with the default palette as a base. This could also be influenced by semantic pairing.  The end result: a lot of themes look visually similar and there is less diversity in Base16 schemes than you find in other theming ecosystems.

_BaseNext has no default scheme and explicitly discourages designers from trying to hue match other themes._


#### Semantic Pairing

With Base16 `base08` is used for both variables and diff deleted.  If you want deleted lines in diffs to be colored red you're stuck with red variables also, nothing you can do.  [Base16 themes include a lot of red variables.](https://github.com/base16-project/base16/issues/10)  This also entirely breaks the fidelity of some themes (like Nord) that are ported from richer ecosystems without such restrictions.

_BaseNext allows you to override any default pairings and easily define two colors._ Variables blue, diff deleted red, you got it.


## Chat

Feel free to stop by the [#base16 channel](https://web.libera.chat/#base16) on [Libera Chat](https://libera.chat/) or the [bridged Matrix channel](https://matrix.to/#/#base16:libera.chat) to talk about it.

## Credits

Thanks to [Chris Kempson](https://github.com/chriskempson) for the original concept and implementation of Base16.
