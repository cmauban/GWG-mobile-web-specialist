# Accessibility Styles

## Focus CSS

* do not get rid of focus.
* keyboards need to know what element they are interacting with.
* add `:focus` whereever there is a `:hover`

### buttons
```css
:focus {
  outline: 1px dotted #fff;
}

OR

:focus {
  outline: 0;
  box-shadow: 0 0 8px 3px rgba(255, 255, 255, 0.8);
}

```

### radio buttons
```css
radio:focus {
  outline: 0;
}

radio:focus::before {
  box-shadow: 0 0 1px 2px #5b9dd9; // give them a blue circle JUST around the radio button
}

```

### links
```css
:focus {
  outline: 0;
  text-decoration: none;
}

:focus,
:hover {
  background: #c2185b;
  color: #ffffff;
  text-decoration: underline;
  box-shadow: 0 2px 2px 0 rgba(0, 0, 0, .14),
              0 3px 1px -2px rgba(0, 0, 0, .2),
              0 1px 5px 0 rgba(0, 0, 0, .12),
}

```

### use Aria CSS instead of a CSS selector
```css
.disclosure-button[aria-expanded="false"] .icon::after{
  content: '▶';
}

.disclosure-button[aria-expanded="true"] .icon::after{
   content: '▼';
}

INSTEAD OF..

.disclosure-button .icon::after {
  content: '▶';
}

.disclosure-button.expanded .icon::after {
  content: '▼';
}

.disclosure-content[aria-hidden="true"] {
  visibility: hidden;
  opacity: 0;
}

.disclosure-content[aria-hidden="false"] {
  visibility: visible;
  opacity: 1;
}

```

## Color Contrast

* minimum contrasts ratio of body text and images is at least 4.5:1
* larget text (over 18 pt or 14 pt bold) has to have at least 3:1
