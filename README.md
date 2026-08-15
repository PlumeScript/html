<p align="center">
    <img src="logo.svg" width="400" height="200">
</p>

HTML generator written in Plume: tags, typed attributes, serialized to HTML text.

## Installation

```
quill add html
```

## Usage

```plume
use html, css

@Div
    class: do
        app: $true
        main: $false
    end
    - @P(style: (color: red, fontSize: $unit(2, rem)))
        World
    end
end
```

```html
<div class="app"><p style="color: red;font-size: 2rem;">World</p></div>
```

### `Tag(name, content, ?autoClose, ?noClose, ...attrs)`

Core renderer. Predefined tag macros (`Div`, `P`, `Ul`, …) are shorthands for it; use `Tag` directly for any tag not in the list.

- string keys in `attrs` → attributes, names converted `camelCase` → `kebab-case`
- value `true` → presence attribute (`disabled`); `false` → omitted
- value `string` → `attr="value"` (escaped)
- `autoClose` → self-closing (`<input/>`); `noClose` → void, no close tag (`<img>`)

### `style` / `class` as tables

| key | input | output |
|-----|-------|--------|
| `style` | table | serialized via the `css` lib |
| `class` | table of booleans `{a: true, b: false}` | `"a"` (truthy keys only) |
| `class` | table of strings `{1: "x", 2: "y"}` | `"x y"` (values joined) |
