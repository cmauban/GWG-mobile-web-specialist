# Ajax with XHR

**A**synchronous **J**avaScript **A**nd **X**ML requests: client sends GET request to server and then gives a response back to client.

* **GET Request**: An internet request for data. Sent from a client to a server.

* **Response**: A server's response to a request. Sent from a server to a client. A response to a GET request will usually include data that the client needs to load the page's content.
  * Data:
     * XML `<entry></entry>`
     * JSON `{property: data}`
     * HTML `<div></div>`

## `XMLHttpRequest`
* MDN's docs - https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/open
* WHATWG Spec - https://xhr.spec.whatwg.org/
* W3C Spec - https://www.w3.org/TR/XMLHttpRequest/

## Handling Success and Errors - Creating XHR object
This creates the XHR object, tells it what info to request, sets up handlers for a successes or error, and then actually send the request:

```javascript

function handleSuccess () {
    // in the function, the `this` value is the XHR object
    // this.responseText holds the response from the server
    console.log( this.responseText ); // the HTML of https://unsplash.com/
}

function handleError () {
    // in the function, the `this` value is the XHR object
    console.log( 'An error occurred 😞' );
}

const asyncRequestObject = new XMLHttpRequest();
asyncRequestObject.open('GET', 'https://unsplash.com');
asyncRequestObject.onload = handleSuccess;
asyncRequestObject.onerror = handleError;
asyncRequestObject.send();

```

## Requests from API that returns JSON

```javascript

function handleSuccess () {
const data = JSON.parse( this.responseText ); // convert data from JSON to a JavaScript object
console.log( data );
}

asyncRequestObject.onload = handleSuccess;

```

## Example of an HTTP request asynchronously with JavaScript

```javascript

(function () {
    const form = document.querySelector('#search-form');
    const searchField = document.querySelector('#search-keyword');
    let searchedForText;
    const unsplashRequest = new XMLHttpRequest();
    const responseContainer = document.querySelector('#response-container');

    form.addEventListener('submit', function (e) {
        e.preventDefault();
        responseContainer.innerHTML = '';
        searchedForText = searchField.value;

        // SEND AN ASYNC REQUEST FOR AN IMAGE FROM A WEBSITE API

        // 1. create an XHR object
        const imgRequest = new XMLHttpRequest();

        // 2. set HTTP method and the URL of the resource to be fetched
        imgRequest.open('GET', `https://api.unsplash.com/search/photos?page=1&query=${searchedForText}`);

        // 3. set this to a func that will run upon a successful fetch
        imgRequest.onload = addImage; // when the unsplashed image returns, it calls the addImage function

        // 4. set this to a functhat will run when an error occurs
        imgRequest.onerror = function (error) {
          requestError(error, 'image');
        };

        imgRequest.setRequestHeader('Authorization', 'Client-ID 3117fd9f785f6c5eceeeda79657a28679b86c789d26b299158c14bb0b7b51582');

        // 5. send the request
        imgRequest.send();


        // request articles from NY times
        const articleRequest = new XMLHttpRequest();
        articleRequest.onload = addArticles; // when the NY times article returns, it calls the addArticles function
        articleRequest.open('GET', `http://api.nytimes.com/svc/search/v2/articlesearch.json?q=${searchedForText}&api-key=fe09ea4030d04edf9c54262f647288fd`);
        articleRequest.send();

    });

    function addImage(){
      let htmlContent = '';
      const data = JSON.parse(this.responseText);

      // check to see if image is returned
      if (data && data.results && data.results[0]) {
      const firstImage = data.results[0];

      htmlContent = `<figure><img src="${firstImage.urls.regular}" alt="${searchedForText}"</figure>`;

    } else {
        htmlContent = '<div class="error-no-image">No image available</div>';
    }

      responseContainer.insertAdjacentHTML('afterBegin', htmlContent);
    }


    function addArticles () {
      let htmlContent = '';
      const data = JSON.parse(this.responseText);

      if (data.response && data.response.docs && data.response.docs.length > 1) {
        htmlContent = '<ul>' + data.response.docs.map(article => `<li class="article">
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
