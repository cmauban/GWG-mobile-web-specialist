# Accessibility

* [Web Content Accessibility Guidelines 2.0 (WCAG)](https://www.w3.org/TR/WCAG20/)
* [Web Aim Checklist for WCAG 2.0](https://webaim.org/standards/wcag/checklist)
* Chrome Accessibility Dev Tool Extention lets you quickly find accessibility issues in your page
  * adds an `Accessibility Properties` panel to your Elements inspector
  * add an `Accessibility` option to the audits panel

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
