# Accessibility

* [Udacity Accessibility Example code](https://github.com/udacity/ud891)
* [Web Content Accessibility Guidelines 2.0 (WCAG)](https://www.w3.org/TR/WCAG20/)
* [Web Aim Checklist for WCAG 2.0](https://webaim.org/standards/wcag/checklist)
* Chrome Accessibility Dev Tool Extention lets you quickly find accessibility issues in your page
  * adds an `Accessibility Properties` panel to your Elements inspector
  * add an `Accessibility` option to the audits panel
* Web apps can be more accessible using:
  * **DOM ORDER**
  * LOGICAL **FOCUS** STRATEGY
  * RICH **KEYBOARD** EXPERIENCE
  * **SEMANTICS**
  * **LABELING** CONTROLS AND IMAGES
  * PAGE STRUCTURE USING **HEADINGS**
  * PROVIDE **LANDMARK** INFORMATION FOR ASSISTIVE TECHNOLOGY
  * **LINKS**
  

### VoiceOver shortcuts

* `CMD+F5` to turn on VoiceOver on OS X
* Normal keyboard operation (`TAB, Shift+TAB`, arrow keys etc.) work as normal with VoiceOver running
* `CMD+L` to jump to address bar
* `CTRL+Option+U` to open Web Rotor
* Type search term with Web Rotor open to search within Web Rotor
* `CTRL` + `Option` + `← ↑ ↓ →` to explore content
* `CTRL` + `Option` + `CMD` + `H` to move forward by heading
* `CTRL` + `Option` + `CMD` + `Shift` + `H` to move backward by heading

## Focus

* focus - determines were keyboard elements go on the page
* focus on interactions only: CTAs, inputs, dropdowns, etc.
* all page functionality should be available by using the keyboard
* no mouse, more productive
* show highlight in fields for focus
* **implicitly focusable:** automatically in the tab order + build-in keyboard event handling
* DOM order matters = tab order

* keys:
  * `tab` moves focus forward
  * `shift` + `tab` moves focus backwards
  * arrow keys move focus within a component
  * `space bar` selects/de-selects

### [`tabindex`](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex)

* A negative value (usually `tabindex="-1"`) means that the element should be focusable, but should not be reachable in keyboard navigation. Mostly useful to create accessible widgets with JavaScript.
* `tabindex="0"` means that the element should be focusable in sequential keyboard navigation, but its order is defined by the document's source order.
* don't used `tabindex` greater than 1.
* [managing focus with `tabindex` and JavaScript example](https://github.com/udacity/ud891/tree/gh-pages/lesson2-focus/03-managing-focus/solution)
* **the ARIA `role` attribute should ALWAYS be on the same element as the `tabindex` attribute**

### [Skip Links](https://webaim.org/techniques/skipnav/)

* for links you want to skip so you can get to the main content without having to go through the navigation and sidebar every time to improve their experience

```html
<a href="#maincontent" class="skip-link">Skip to main content</a> // you want it before the nav
<nav>
...
</nav>
<main id="maincontent" tabindex="-1"> // tabindex necessary for older browsers
...
</main>
```

```css
.skip-link {
 position: absolute;
 top: -40px; // off screen
 left: 0;
 background: #BF1722;
 color: white;
 padding: 8px;
 z-index: 100;
}

.skip-link:focus {
 top: 0; // move back on screen
}
```

### [Keyboard Design Patterns - Roving Focus/tabindex](https://www.w3.org/TR/wai-aria-practices/#radiobutton)

* [example]()https://github.com/udacity/ud891/tree/gh-pages/lesson2-focus/05-radio-group/solution
* to find missing focus, type in `document.activeElement` in the console

## Navigating Content
* use meaningful headings and good page structure
  * `<header>` `<nav>` `<main>` `<section>` `<article>` `<aside>` `<footer>`

## Semantics

### `<label>`
* all form fields need a label. If a form control does not have a properly associated text label, the function or purpose of that form control may not be presented to screen reader users. Form labels also provide visible descriptions and larger clickable targets for form controls.

```html
<input type="checkbox" id="letter" checked name="jLetter">
<label for="letter">Reciever offers?</label>

OR

<label>
 <input type="checkbox" checked name="jLetter">
 Reciever offers?
</label>

```

### `alt` text

* all images should have `alt` text.
* decorative and descriptive thumbnail images with links should have empty `alt` text to avoid repeition.
* without alternative text, the content of an image will not be available to screen reader users or when the image is unavailable.

### Using Headings for Screen readers
* HEADING HIERARCHY - use headings in a meaningful order down the page, not for styling.

```html
<h2 class="offscreen">Top Story</h2>
```
```css
.offscreen {
  position: absolute;
  left: -10000px;
  top: -10000px;
}
```
## ARIA or "WAI-ARIA"

* we use ARIA to enable us to use non-native elements so screen readers can still understand what it is. Ie. Fake/custom checkbox instead of the native `<input type="checkbox">`
* it can also modify exisiting semantics. ie. from a button to switch toggle.
* this will allow screen readers to know the name AND the **state.** (JS needed)
* use `role=""` and `aria-checked="true"` (or false)
* **the `role` attribute should ALWAYS be on the same element as the `tabindex` attribute**
* aria is the only way we can use labels for description text.

```html
<!-- custom checkbox -->
<div role="checkbox" aria-checked="true">
 Receive offers
</div>
```
* it can add extra labels and description text. ie. button images

```html
<button class="glyph" aria-label="Filter">
 <div class="menu-glyph">
 </div>
</button>
```

### [`role="X"`s](https://www.w3.org/TR/wai-aria-1.0/roles#role_definitions)
 * accordions: `tree`, `treeitem`, `group` - `aria-expanded`
 * checkbox: `checkbox` - `aria-checked`
 * toggle: `switch`
 * live updates: `alert`
 
 #### labels
 * `aria-label` - use on close or hamburger menus. ie: `<button aria-label="close">X</button>` button name = "close"
 * `aria-labelledby` - use to specify and conntect name to option labels. ie: `span id="rg-label">Drink Options</span><div role="radiogroup" aria-labelledby="rg-label">...</div>` radio group name: "Drink options". this will always take precedent.
