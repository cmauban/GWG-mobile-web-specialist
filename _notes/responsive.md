# Accessible & Responsive Web Apps

## Viewports

* DIP (Device Independent Pixels) = 1/2 of Hardware Pixels. or one DIP = two HwP ie: 1280px DIP = 2560 HwP
    * HwP / DPR = DIPs
* CSS Pixels = Hardware Pixels / 2. or 1 css px = 2 hardware px.
* The same website can look different on screens of identical resolutions because:
    * Device pixel ratio differs between devices.
    * The viewport wasn't set.

### Setting the viewport:
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
 * 2-3 breakpoints
 
 ### Grids
 * grid fluid system - column wrap. 960px grid layout or bootstrap
 
 ### Flexbox
 ```
 .container {
   display: flex;
   flex-wrap: wrap;
 }
 ```
* **important** for responsive design
* you can use this to postion elements or the order instead of using floats or changing the HTML.
* the default of display flex is row. they will always be in a single line within the viewport it will put elements in a row instead of a column.
* `flex-wrap: wrap:` this will tell the browser that it is ok for the row of flex elements to wrap onto the next line.
* the `order` CSS attribute: you can change the order of the elements:
   * ```
      {
         .dark_blue {order: 4;}
         .light_blue {order: 5;}
         .green {order: 2;}
         .orange {order: 3;}
         .red {order: 1;}
      }
      ```
## Responsive Patterns

1. **COLUMN DROP** -  elements keep expanding as the viewport gets bigger and breakpoints are added. starts at 100% width at narrowest and stacks.
   * `min-width; display: flex; flex-wrap: wrap; width: 100%;`
2. **MOSTLY FLUID** - just like column drop but more fluid and margins are added at a larger breakpoint (ie. 800px). `margin: 0 auto; max-width: 800px;`
3. **LAYOUT SHIFTER** - most responsive pattern with multiple breakpoints. `flexbox` is required to use `order`.
   * `container {width: 100%; display: flex; flex-wrap: wrap} .box {width: 100%;}
4. **OFF CANVAS** - instead of stacking content vertically, it instead places less frequently used content (ie. navigation/menus) off screen, only showing them if the screen is large enough. ie. hamburger icons.
   * `html, body, main {height: 100%; width: 100%;} nav {width: 300px; height: 100%; position: absolute; transform translate(-300px, 0);} nav.open{transform: translate(0,0);}` in media screen and (min-width: 600px) to show by default:
   * ```
      nav {
         position: relative;
         transform: translate(0,0);
      }
      
      body {
         display: flex;
         flex-flow: row nowrap;
      }
      
      main {
         width: auto;
         flex-grow: 1;
      }
   ```
