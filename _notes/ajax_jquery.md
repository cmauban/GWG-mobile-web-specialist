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
## Example of Ajax request with jQuery
```javascript
/* eslint-env jquery */

(function () {
    const form = document.querySelector('#search-form');
    const searchField = document.querySelector('#search-keyword');
    let searchedForText;
    const responseContainer = document.querySelector('#response-container');

    form.addEventListener('submit', function (e) {
        e.preventDefault();
        responseContainer.innerHTML = '';
        searchedForText = searchField.value;

        // SEND AN ASYNC REQUEST FOR AN IMAGE FROM A WEBSITE API

        $.ajax({
          // source to be fetched
          url: `https://api.unsplash.com/search/photos?page=1&query=${searchedForText}`,
          // same as .setRequestHeader in XHR
          headers: {
            Authorization: 'Client-ID 3117fd9f785f6c5eceeeda79657a28679b86c789d26b299158c14bb0b7b51582'
          }
          // send the request
        }).done(addImage)
        .fail(function(error) {
          requestError(error, 'image');
        });


        // Request articles from NY times
        $.ajax({
          url: `http://api.nytimes.com/svc/search/v2/articlesearch.json?q=${searchedForText}&api-key=fe09ea4030d04edf9c54262f647288fd`
        }).done(addArticles)
        .fail(function(error){
          requestError(error, 'art');
        });

    });

    function addImage(image){
      let htmlContent = '';

      // check to see if image is returned
      if (image && image.results && image.results[0]) {
      const firstImage = image.results[0];

      htmlContent = `<figure><img src="${firstImage.urls.regular}" alt="${searchedForText}"</figure>`;

    } else {
        htmlContent = '<div class="error-no-image">No image available</div>';
    }

      responseContainer.insertAdjacentHTML('afterBegin', htmlContent);
    }


    function addArticles (art) {
      let htmlContent = '';

      if (art.response && art.response.docs && art.response.docs.length > 1) {
        htmlContent = '<ul>' + art.response.docs.map(article => `<li class="article">
        <h2><a href="${article.web_url}">${article.headline.main}</a></h2>
        <p>${article.snippet}</p>
        </li>`).join('') + '</ul>';
      } else {
        htmlContent = '<div class="error-no-articles>">No articles available</div>';
      }

      responseContainer.insertAdjacentHTML('beforeBegin', htmlContent);

    }


})();

```
