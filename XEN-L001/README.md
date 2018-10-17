---
status: draft
champion: https://xod.io/users/nkrkv
---

# XEN-L001: Color library

Many hardware projects involve some light effects. To achieve the effects various colorful LEDs and LED strips are widely used. Color is not a trivial scalar. Several notations exist to define a color. For example RGB, HSV, and HSL. XOD should provide a standard library to hold and transfer color values so that library authors don’t reinvent color-related nodes again and again.

Let it be `xod/color`.

## Internal Representation

A color value can be stored as three bytes:

```cpp
struct Type {
    uint8_t r, g, b;
};
```

## Nodes

### color

(utility) Color type constructor.

### color-rgb-bytes

Constructs a color value from red, green, and blue components expressed as byte values. Use decimal (0d to 255d) or hexadecimal (00h to FFh) byte literals. For example, if a graphical editor shows a blue as “#287ec9” or “rgb(40, 126, 201)” use the following literals for R/G/B: 28h/7Eh/C9h or 40d/126d/201d.

| Dir | Pin  | Type    | Default | Description
| --- | ---- | ------- | ------- | -----------
| in  | R    | byte    |         | Red
| in  | G    | byte    |         | Green
| in  | B    | byte    |         | Blue
| out |      | color   |         |

### to-rgb-bytes

Destructs a color value into red, green, and blue components encoded as byte values.

| Dir | Pin  | Type    | Default | Description
| --- | ---- | ------- | ------- | -----------
| in  |      | color   |         |
| out | R    | byte    |         | Red
| out | G    | byte    |         | Green
| out | B    | byte    |         | Blue

### color-rgb

Constructs a color value from red, green, and blue components. Each component should be in the range [0, 1]. Values out of this range are truncated to 0 or 1.

| Dir | Pin  | Type    | Default | Description
| --- | ---- | ------- | ------- | -----------
| in  | R    | number  |         | Red
| in  | G    | number  |         | Green
| in  | B    | number  |         | Blue
| out |      | color   |         |

### to-rgb

Destructs a color value into red, green, and blue components. Each component is in range [0, 1].

| Dir | Pin  | Type    | Default | Description
| --- | ---- | ------- | ------- | -----------
| in  |      | color   |         |
| out | R    | number  |         | Red
| out | G    | number  |         | Green
| out | B    | number  |         | Blue

### color-hsl

Constructs a color value from hue, saturation, and lightness values (HSL model).

| Dir | Pin  | Type    | Default | Description
| --- | ---- | ------- | ------- | -----------
| in  | H    | number  | 0       | 0 is for red, 0.33 for green, 0.66 for blue, and 0.99 is for red again. Some systems use degrees for the hue component. The value of 1.0 corresponds to 360° of such systems. When out out of [0; 1) range only the fractional part is taken into account.
| in  | S    | number  | 1.0     | Saturation. Should be in the range [0, 1]. 0.0 corresponds to fully-gray shade and 1.0 to saturated color shade. Values out of the range are truncated to 0 or 1.
| in  | L    | number  | 0.5     | Lightness. Should be in the range [0, 1]. 0.0 corresponds to black; 0.5 to pure color; 1.0 to white. Values out of the range are truncated to 0 or 1.
| out |      | color   |         |

See [Wikipedia article](https://en.wikipedia.org/wiki/HSL_and_HSV) for details about the HSL color space.

To get a pure vivid color use S = 0 and L = 0.5.

### to-hsl

Destructs a color value to hue, saturation, and lightness values. See `color-hsl` docs for more details.

| Dir | Pin  | Type    | Default | Description
| --- | ---- | ------- | ------- | -----------
| in  |      | color   |         |
| out | H    | number  |         | Hue
| out | S    | number  |         | Saturation
| out | L    | number  |         | Lightness

### format-color

Formats a color as a 6-digit hexadecimal value (ex.: "FF3300").

| Dir | Pin  | Type    | Default | Description
| --- | ---- | ------- | ------- | -----------
| in  |      | color   |         |
| out |      | string  |         |
