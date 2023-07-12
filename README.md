# b-x

A custom HTML element built to be a reimagining of html and css that just works every time. Or at least eventually it will. It's well under way, but still has plenty of rough edges.

## Installation

- 1. Run `npm install b-x` in your project directory.
- 2. In main add `import "b-x";` to the top of your file.
- 3. If you are using typescript declare a global component
  - Vue:
    ```ts
    declare global {
      namespace preact.createElement.JSX {
        interface IntrinsicElements {
          "b-x": {
            role?: string;
            sty?: Sty;
          };
        }
      }
    }
    ```
  - Preact:
    ```ts
    declare module "vue" {
      export interface GlobalComponents {
        "b-x": {
          role?: string;
          sty?: Sty;
        };
      }
    }
    ```

## Usage

Use wherever you would use a base html element. Use the `role` attribute for accessibility, and use the `sty` attiribute for styling.

Here is a Preact example:

```tsx
export function App() {
  return (
    <b-x
      role="button"
      sty={{
        background: "red",
        textColor: "white",
      }}
    >
      Click Me!
    </b-x>
  );
}
```

## Styling

The `sty` attribute is a custom attribute that takes an object with the following properties:

```ts
type Sty = {
  /**
   * width & height: Can be `1f`, `2f`, etc.. to set flex size; a
   * number for a multiple of rem, a css string, or -1 to shrink to
   * fit contents(default).
   */ ;
  width: `${number}f` | number | CssString | -1;
  height: `${number}f` | number | CssString | -1;

  /**
   * Sets the layout direction of children. Setting to "row" or
   * "column" does what you'd think, setting to "stack" layers
   * children along the z-index.
   * NOTE: Stack is still under development.
   */
  axis: "row" | "column" | "stack";

  /**
   * pad: Sets the space between the box and its contents, and between
   * each of the contents of the box. More specific options override
   * less specific options. Set to a number for a multiple of rem, or
   * a css string.
   */
  pad: number | CssString;
  padAround: number | CssString;
  padAroundX: number | CssString;
  padAroundY: number | CssString;
  padTop: number | CssString;
  padRight: number | CssString;
  padBottom: number | CssString;
  padLeft: number | CssString;
  padBetween: number | CssString;
  padBetweenRows: number | CssString;
  padBetweenColumns: number | CssString;

  /**
   * overflow: Sets the overflow of the box. Most values do what you'd
   * expect. Setting to "forceStretchParent" will behave like css's
   * "visible".
   * NOTE: Overflow is a bit buggy right now. It'll worked on it in the
   * coming weeks.
   * NOTE: an "overflow" option that behaves similarly to spreadsheet
   * cells is coming soon.
   */
  overflowX: "crop" | "wrap" | "scroll" | "forceStretchParent";
  overflowY: "crop" | "wrap" | "scroll" | "forceStretchParent";

  /**
   * These are all failry strait forward. They style the box. "background"
   * though can be either a color or a base64 encoded image. We'll expand
   * the functionality of this in the future.
   */
  cornerRadius: number | CssString;
  outlineColor: string;
  outlineSize: number;
  background: string;
  shadowSize: number;
  shadowDirection: ShadowDirection;

  /**
   * Not entirely sure how this will be implemented in future, but is
   * provided as a work around for now.
   */
  zIndex: number;

  /**
   * These set the text styling. Scale sets the font size, and the rest
   * are self explanatory.
   */
  scale: number | CssString;
  textColor: ColorString;
  /** NOTE: Eventually we might want to make this a number so it can be
   * granularly controlled. With presets for thin, normal, and bold. */
  textIsBold: boolean;
  textIsItalic: boolean;
  textIsUnderlined: boolean;

  /**
   * Box itneractions are new and will change a lot in the coming weeks.
   */
  isInteractable: boolean;
  // Adds a bonus touch area around the box. It's a bit buggy right now.
  bonusTouch: boolean;
};
```
