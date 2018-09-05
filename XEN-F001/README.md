# XEN-F001: Enums

Enumerations are common in the programming world. Most languages provide either built-in facilities for defining enum types or recommendations for emulating them. While some languages provide very basic support which is a layer on top of numbers or strings (C, Python), other languages offer powerful ADT (Algebraic Data Types) systems where an enum item can carry some additional payload.

XOD lacks enumerations. This XEN suggests a minimalistic approach to bring a kind of enums to the language.

## Practical scenario

Consider a smart accelerometer module which can be configured by a user to measure at one of the predefined sensitivity levels. A particular model might allow choosing between ±2g, ±4g, and ±16g. So, this parameter might be an input of the accelerometer node. But what type should it have?

It is possible to use a simple `Number`. But what does it mean if a user sets the sensitivity value to 8.23? Should the accelerometer round it to 4? 16? Output errors? It can be hard for a newcomer to understand all available options. It would be much easier for him to select a variant from a drop-down list. In our case, the sensitivity parameter acts more like an enum then like a number.

How can XOD know that available options for the parameter are 2, 4, and 16g and nothing beside them?

## Possible solution

An accelerometer library author can introduce a new custom type: `sensitivity`. The exact internal representation does not matter much as it might be opaque for library users. The important thing is defining few “constant” patch nodes which take nothing as input and output a single value of type `sensitivity`. Let’s name the patch nodes `2g`, `4g`, and `16g`.
The default value output by the original `sensitivity` constructor should be a sane default, e.g., the same as `2g`.

Now, a library user can’t bind an arbitrary value to the sensitivity input. He has to place one of `2g`/`4g`/`16g` nodes explicitly and link it to the parameter pin. Or the pin will default to `2g`.

In any case, a user has no chance to send a wrong value to the strictly-one-of input.

## XX improvemet

Searching for nodes compatible with a particular parameter can discourage a library newbie. It would be more convenient to show all variants to choose from.

Here XOD might provide something more useful than just a disabled “custom type” input in the inspector pane. In other words, XOD can allow binding values to custom type pins. How can it extract all available options?

For any particular type, XOD can look for all patches in the project and available libraries to find those who have a single out of the specific type and have no inputs. That way it will see `2g`, `4g`, and `16g`.  The inspector then can suggest these three variants along with “(default)” corresponding to the current behavior for binding.

Furthermore, an `input-sensitivity` terminal can also suggest choosing from these values to set the default for a node. The accelerometer node can, for example, has the default value bound to `4g` and it will be shown as `4g` in the inspector when a user places the node.

## More examples

- color: red, green, blue, orange, pink, white, black
- i2c: i2c-0, i2c-1
- uart: uart-0, uart-1, uart-2, uart-3

## Pulses

The pulse type might follow the convention and provide a choice between `never`, `on-boot`, `continuously` defined as regular nodes in `xod/core`.

Besides the consistency, it will also allow other users to provide additional variants like 1-hertz, hourly, etc (see below).

## Extensions from libraries

The available options might be discovered not only in the project/library where the type is defined but also inside sibling libraries. There might be even libraries entirely made to provide new color choices, pulse frequencies, etc.

To avoid drop-down variants mess, the options found in the “home” library should go first and contain no prefixes. Other found variants should be listed below, sorted alphabetically, and fully qualified:

- black
- blue
- green
- orange
- pink
- red
- white
- bob/funkolorz/cyan
- bob/funkolorz/haki
- vasya/alarm/amber
- vasya/alarm/green

## Utilities and deprecations

Utilities and deprecations must not appear in lists of available options.

## Literals

Every value bound should be expressed as a literal. To avoid conflicts with other types, we can reserve “owner/lib/node” and “@/node” forms for the enum literals.
