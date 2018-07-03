# Ajax with jQuery

* Use this instead of Ajax with XHR
    * you won't need to create a XHR obj
    * instead of a specifying that it's a `GET` request, it will default to one and we only need to provide the source URL
    * instead of setting `onload`, use the `.done()` method

## `.ajax()` Method

```javascript
$.ajax(<url-to-fetch>, <a-configuration-object>);

// or the more common way..

$.ajax(<just a configuration object>);

```
* **Configuration Objection** - plain javascript obj that's used to configure someting. for example:
    ```javascript
    var settings = {
       frosting: 'buttercream',
       colors: ['orange', 'blue'],
       layers: 2,
       isRound: true
    };
    ```
### An Ajax w/ jQuery request vs. w/ XHR :
```javascript
// THIS:
$.ajax({
    url: `https://api.unsplash.com/search/photos?page=1&query=${searchedForText}`
    headers: {
      Authorization: 'Client-ID <your-client-id-here>'
    }
}).done(addImage);


// REPLACES THIS:
const imgRequest = new XMLHttpRequest();
imgRequest.onload = addImage;
imgRequest.open('GET', `https://api.unsplash.com/search/photos?page=1&query=${searchedForText}`);
imgRequest.setRequestHeader('Authorization', 'Client-ID <your-client-id-here>');
imgRequest.send();
```
