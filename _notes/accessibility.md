# Accessibility

* [Web Content Accessibility Guidelines 2.0 (WCAG)](https://www.w3.org/TR/WCAG20/)
* [Web Aim Checklist for WCAG 2.0](https://webaim.org/standards/wcag/checklist)

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
