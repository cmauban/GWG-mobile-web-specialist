# Accessible & Responsive Web Apps

## Viewports

* DIP (Device Independent Pixels) = 1/2 of Hardware Pixels. or one DIP = two HwP ie: 1280px DIP = 2560 HwP
    * HwP / DPR = DIPs
* CSS Pixels = Hardware Pixels / 2. or 1 css px = 2 hardware px.
* The same website can look different on screens of identical resolutions because:
    * Device pixel ratio differs between devices.
    * The viewport wasn't set.

#### Setting the viewport:
```
<meta name="viewport" content="width=device-width, initial-scale=1">
```
`initial-scale=1` sets a 1:1 ratio of CSS pixels and Device independent pixels.

## MOBILE TIPS: 
* start mobile first. this prioritizies content. performance is better.
* add in main.css:
```
img, embed, object, video {
  max-width: 100%;
}

```

* tap targets should be at least `40px x 40px`. `48px` is good.
  * ```
    nav a, button {
      min-width: 48px;
      min-height: 48px;
    }
    ```
 
 ## Media Queries
 * Linked CSS: `<link rel="stylesheet" media="screen and (min-width: 550px)" href="weather-medium.css">` `<link rel="stylesheet" media="screen and (min-width: 700px)" href="weather-large.css">`
 * Media query CSS: `@media screen and (min-width: 550px) {}`
 
 ### Picking Breakpoints
 * start with the smallest first
 * pick your breakpoints based on the content
 
