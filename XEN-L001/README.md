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
| in  | R    | byte    | 0d      | Red
| in  | G    | byte    | 0d      | Green
| in  | B    | byte    | 0d      | Blue
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

- [in] R :: Number — Red
- [in] G :: Number — Green
- [in] B :: Number — Blue
- [out] :: color

### to-rgb

Destructs a color value into red, green, and blue components. Each component is in range [0, 1].

- [in] :: color
- [out] R :: Number — Red
- [out] G :: Number — Green
- [out] B :: Number — Blue

### color-hsl

Constructs a color value from hue, saturation, and lightness values (HSL model).

- [in] H :: Number — Hue. Should be in the range [0, 1). 0 is for red, 0.33 for green, and 0.66 for blue. Some systems use degrees for the hue component. The value of 1.0 corresponds to 360° of such systems.
- [in] S :: Number = 1.0 — Saturation. Should be in the range [0, 1]. 0.0 corresponds to fully-gray shade and 1.0 to saturated color shade.
- [in] L :: Number = 0.5 — Lightness. Should be in the range [0, 1]. 0.0 corresponds to black; 0.5 to pure color; 1.0 to white.
- [out] :: color

See [Wikipedia article](https://en.wikipedia.org/wiki/HSL_and_HSV) for details about the HSL color space.

To get a pure vivid color use S = 0 and L = 0.5.

### to-hsl

Destructs a color value to hue, saturation, and lightness values. See `color-hsl` docs for more details.

- [in] :: color
- [out] H :: Number — Hue
- [out] S :: Number — Saturation
- [out] L :: Number — Lightness

### format-color

Formats a color as a 6-digit hexadecimal value (ex.: "FF3300").

- [in] :: color
- [out] :: String
