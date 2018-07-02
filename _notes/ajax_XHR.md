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
