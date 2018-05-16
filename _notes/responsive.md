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
* wrap tables in div.
```
   div.contained_table {
      width: 100%;
      overflow-x: auto
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
* **CSS `background-image: url(''); background-size: cover;`** will scale up the image so the image takes up the entire div.

## OPITMIZATION

### Images

### Tables
 * HIDDEN COLUMNS - hide columns based on their importance as the viewports get smaller.
 *
 *


**No More Tables.** turn tables into column/row in a smaller viewport to display all data.
 ```
 
 @media screen and (max-width: 500px) {
    table, thead, tbody, th, td tr {
      display: block;
    }
    
    thead tr { // hide table header. don't use display:none because of screen readers
      position: aboslute;
      top: -9999px;
      left: -9999px;
   }
   
   td { // make room for header
      position: relative;
      padding-left: 50%
   }
   
   td:before { // add row labels
      position: absolute;
      left: 6px;
      content: attr(data-th); // label for each row
      font-weight: bold;
   }
    
 }
 ```
### FONTS
* ~65 characters per line
* at least 16px or 1.2em
* `em` refers to the font size. ie: 50em (element) x 16px (font-size) = 800px (width)

## IMAGES x UNITS

* Total bits = pixels x bits per pixel
* keep images as small as possible, and compression as high as possible.
  * less pixels x better compress = less bytes
* set `max-width` of all images to `100%` so its only as wide as its natural width.
* use `relative` + `aboslute` sizing for images side by side by using: `width: calc((100% - 10px)/2); margin-right: 10px;` for the images to span 100% across screen.
   * `calc()` you take the 100% viewport - the total px of margin space, divided by the number of images.
* also use `img:last-of-type { margin-right:0; }` to make sure the last image doesn't have margin.
* use `height: 100vh` and `width: 100vw` instead of percents.
* `height: 100minvh; weight: 100minvw`
* RESIZE & COMPRESS YOUR IMAGES
   * [Grunt-responsive-images](https://github.com/andismith/grunt-responsive-images)
* Use `<figure>` to contain images, illustrations, diagrams, code snippets, etc. that is a reference in the main flow of a document but can be moved to another part of the document without affecting the main flow.
   ```
  <figure>
      <img src="https://developer.cdn.mozilla.net/media/img/mdn-logo-sm.png" alt="An awesome picture">	
     <figcaption>MDN Logo</figcaption>
  </figure>
  
  // or
  
    <figure>
      <p>
        Depression is running through my head,<br>
        These thoughts make me think of death,<br>
        A darkness which blanks my mind,<br>
        A walk through the graveyard, what can I find?....
      </p>
      <figcaption><cite>Depression</cite>.
      By: Darren Harris</figcaption>
   </figure>
   ```

### `srcset` and `size` attribute
* allows us to provide a set of images that can be potentially served by the browser.
```
<img src="hero-big.jpg" // fallback option
srcset="hero-small.jpg 450w, hero-medium.jpg 960w, hero-big.jpg 1500w" // img source and define actual width of the img
sizes="(max-width: 552px) 450px, (max-width: 1062px) 960px, 1500px" // which vp widths we want a particular image to be downloaded ie. download img with width of 450px on devices with vp width up to 552px. dont need to declare width for biggest img. just need to declare the size for above 1062px.
alt="Learnedia Hero" />
```
* if you specify `srcset` but not `sizes`, it will default it to `100vw`.
* in `srcset` ie. `hero-small.jpg 450w`, define the actual width of the img using the integer representing the width in pixels with w appended. this lets the browser know the actual size of the image before downloading it.


### File Formats
* order of the kind of images you should use:
   1. vector .SVG (logos, small size, sharp images)
   2. vector .PNG (use to preserve fine detail with highest resolution. great for logos and text images. use .png over gif bc of licensing issues)
      * PNG-8: not many colors need to be used
      * PNG-24: many colors need to be used
   3. GIFS (use for images with simple illustrations and blocks of color like logos and icons. not photographs.)
   4. raster .JPEG (for photos or screenshots)
   * browser can reformat vector images at different sizes.

### Image scenarios:
* star icon to be reused and scaled on mobile devices
   * **vector** over raster
   * inline the images with .svg (not too many bytes) _or_
   * set `src` to external reused imgs (cache and not reload)
* self-publishing, mobile photo journal site w/ single use photos
   * **.jpg (raster)** over vector
   * inline the images (reduces requests for mobile)
