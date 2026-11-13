# CSS

CSS

Author

Benedict Thekkel

## Introduction to CSS

> Purpose: CSS is used to style and layout web pages. It allows you to apply styles like fonts, colors, spacing, and positioning to HTML elements.

> How It Works: CSS rules are applied to HTML elements to control their appearance on the web page. These rules can be applied inline, internally within the HTML document, or externally via a separate CSS file.

------------------------------------------------------------------------

## Basic Syntax

- Selectors: CSS selectors are used to select the HTML elements you want to style.
- Properties and Values: CSS properties define the styles (e.g., color, font-size), and values specify the behavior of these properties (e.g., red, 16px).

h1 { color: blue; font-size: 24px; }

## Types of CSS

- Inline CSS: Applied directly to an HTML element using the `style` attribute.

``` css
<h1 style="color: blue; font-size: 24px;">Hello World</h1>
```

- Internal CSS: Defined within a `<style>` block inside the `<head>` section of the HTML document.

``` html
<style>
    h1 {
        color: blue;
        font-size: 24px;
    }
</style>
```

- External CSS: Linked from an external file using the `<link>` tag in the `<head>` section.

``` html
<link rel="stylesheet" href="styles.css">
```

## Selectors in CSS

- Universal Selector (`*`): Selects all elements.
- Element Selector: Selects elements by their name (e.g., `p`, `h1`).
- Class Selector (`.classname`): Selects elements by their class attribute.
- ID Selector (`#idname`): Selects a single element by its ID.
- Attribute Selector: Selects elements based on their attributes.
- Pseudo-Classes and Pseudo-Elements:
  - Pseudo-Classes: `:hover`, `:active`, `:focus` – Apply styles based on user interaction.
  - Pseudo-Elements: `::before`, `::after` – Insert content before or after an element.

> Example

``` css
.example-class {
    color: red;
}

#example-id {
    color: green;
}

a:hover {
    text-decoration: underline;
}
```

## CSS Properties

- Color and Background:
  - `color`: Sets the text color.
  - `background-color`: Sets the background color of an element.
  - `background-image`: Sets an image as the background.
- Text and Font:
  - `font-family`: Sets the font of the text.
  - `font-size`: Sets the size of the text.
  - `font-weight`: Sets the boldness of the text.
  - `text-align`: Aligns the text horizontally (left, right, center).
  - `text-decoration`: Underlines, overlines, or strikes through text.
- Box Model:
  - Box Model Components: Content, padding, border, and margin.
  - `width` and `height`: Set the width and height of an element.
  - `padding`: Creates space inside the element, between the content and the border.
  - `border`: Sets the border around the element.
  - `margin`: Creates space outside the element, separating it from other elements.

> Example

``` css
div {
    width: 300px;
    padding: 20px;
    border: 1px solid black;
    margin: 10px;
}
```

- Positioning:
  - Static (default): Elements are positioned according to the normal flow of the document.
  - Relative: Positioned relative to its normal position.
  - Absolute: Positioned relative to its nearest positioned ancestor.
  - Fixed: Positioned relative to the browser window, stays fixed when scrolling.
  - Sticky: Switches between relative and fixed, depending on the scroll position.

``` css
.relative {
    position: relative;
    top: 10px;
    left: 20px;
}
```

- Display and Visibility:
  - `display`: Controls the display type of an element (e.g., `block`, `inline`, `inline-block`, `none`).
  - `visibility`: Controls the visibility of an element (`visible`, `hidden`).
- Overflow:
  - `overflow`: Controls what happens when content overflows an element’s box (`visible`, `hidden`, `scroll`, `auto`).
- Flexbox:
  - Flexible Box Layout: A modern layout module that provides an efficient way to lay out, align, and distribute space among items in a container.
  - `display: flex`: Enables flexbox for an element.
  - `justify-content`: Aligns flex items along the main axis.
  - `align-items`: Aligns flex items along the cross axis.
  - `flex-direction`: Defines the direction of the flex items (row, column). \> Example \`\`\`css .container { display: flex; justify-content: space-between; align-items: center; }

&nbsp;

    - Grid Layout:
      - CSS Grid Layout: A powerful layout system that allows you to create grid-based layouts.
      - `display: grid`: Enables grid layout for an element.
      - `grid-template-columns`: Defines the columns of the grid.
      - `grid-template-rows`: Defines the rows of the grid.
      - `gap`: Sets the spacing between grid items.

    > Example
    ```css
    .grid-container {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        grid-template-rows: auto;
        gap: 10px;
    }

## Responsive Design with CSS

- Media Queries: Used to apply styles based on the device’s characteristics, such as screen width, height, and orientation.

``` css
@media (max-width: 600px) {
    body {
        background-color: lightblue;
    }
}
```

- Viewport Meta Tag: Ensures proper scaling and sizing on mobile devices.

``` css
<meta name="viewport" content="width=device-width, initial-scale=1">
```

- Flexible Units:
  - Relative Units: `em`, `rem`, `%`, `vw`, `vh`.
  - Absolute Units: `px`, `pt`, `in`, `cm`.
- Responsive Images:
  - `max-width: 100%`: Ensures images scale down when the container is smaller than the image.

## CSS Frameworks

- Bootstrap: A popular front-end framework that includes a responsive grid system, pre-built components, and utility classes.
- Foundation: A responsive front-end framework that provides a grid system and UI components.
- Bulma: A modern CSS framework based on Flexbox.

``` html
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
```

## Preprocessors

- Sass (Syntactically Awesome Style Sheets): A CSS preprocessor that allows the use of variables, nested rules, mixins, and functions.
- LESS: Another CSS preprocessor similar to Sass, but with a different syntax. \> Example

``` css
$primary-color: #333;

body {
    color: $primary-color;
}

.container {
    width: 80%;
    margin: 0 auto;
}
```

## Advanced CSS Techniques

- Transitions: Smoothly animate changes to CSS properties.
- Animations: Create complex animations using keyframes.
- Transformations: Rotate, scale, skew, or translate elements.
- Custom Properties (CSS Variables): Define reusable values with custom properties.

> Example

``` css
.box {
    width: 100px;
    height: 100px;
    background-color: red;
    transition: background-color 0.5s ease;
}

.box:hover {
    background-color: blue;
}

@keyframes example {
    from {background-color: red;}
    to {background-color: yellow;}
}

.animated-box {
    animation: example 2s infinite;
}
```

## CSS Grid and Flexbox

- CSS Grid: Best for two-dimensional layouts, allowing for both rows and columns.
- Flexbox: Best for one-dimensional layouts, controlling the layout of items along a single axis. \> Example (CSS Grid)

``` css
.grid-container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 10px;
}

.grid-item {
    background-color: lightgrey;
    padding: 20px;
    text-align: center;
}
```

> Example (Flexbox)

``` css
.flex-container {
    display: flex;
    justify-content: space-between;
}

.flex-item {
    background-color: lightgrey;
    padding: 20px;
    text-align: center;
}
```

Back to top
