# Lesson 3: Service Workers

**Service worker** - javascript file that runs between you and your request. cannot access the DOM but it controls pages. its a script that your browser runs in the background, separate from a webpage, opening the door to features that don’t need a web page or user interaction. (ie. push notifications and background syncs)
* Scope. Needs a trailing `/` (good ex. is github)
* only works in Chrome and Ophra
* The service worker will control any page URL that begins with the scope
* HTTPS only
* Service worker is a programmable network proxy, allowing you to control how network requests from your page are handled
* `Shift + refresh` (easy way to get updates) lets the waiting servicer worker take over.
* offline experiences

#### The Service Worker Life Cycle:
1. to install a SW for your site, you need to register it first, which you do in your page’s javascript. registering a service worker will cause the browser to start the service worker install step in the background.
2. cache some states assets. if all files are cached successfully, then the servicer worker becomes installed.
3. if any of the files fail to download and cache, then the install step will fail.
4. when installed, you need to activate it and handle any management of old caches.
5. after activation, the sw will control all pages that fall under its scope
6. once a service worker is in control, it will be in one of two states:
    1. terminated to save memory
    2. handle fetch and message events that occur when a network request or message is made from your page

## REGISTER A SERVICE WORKER
this tells the browser where you sw javascript file lives.

This code checks to see if the service worker API is available. and if it is, the sw at /sw.js is registered once the page is loaded.

```javascript
navigator.serviceWorker.register(‘/sw.js’) // register for a service worker giving a location
.then(function(){} // returns a promise for success
.catch(function(){} // or failures
```

## Fetch(url) - api.
Make network request and lets you read the response. Fetch returns a promise that resolves to a response.
