# Lesson 8: Built-ins - PROMISES / PROXIES

### PROMISES

* a **promise** object represents the eventual completion or failure of an asynchronous operation and its resulting value.
* a promise constructor takes a function that will run and then, after some amount of time, will either complete successfully or unsuccessfully. When the outcome has been finalized, the promise is now fulfilled and will notify us so we can decide what to do with the response.
* `resolve` and `reject`
  * `resolve` is used to indicate that this function should be called when the request completes successfully. it gets called at the end with the data that we want to return. `resolve(sundae)`
  * `reject` used to indicate that this function should be used if the request fails. `if () { reject('failed') }`

```JavaScript
new Promise(function (resolve, reject) {
    window.setTimeout(function createSundae(flavor = 'chocolate') {
        const sundae = {};
        // request ice cream
        // get cone
        // warm up ice cream scoop
        // scoop generous portion into cone!
        if ( /* iceCreamConeIsEmpty(flavor) */ ) {
            reject(`Sorry, we're out of that flavor :-(`);
        }
        resolve(sundae);
    }, Math.random() * 2000);
});
```

### PROXIES

* create and manage the interactions between objects.
* to create a proxy object, use the proxy constructor - `new Proxy();`
* the proxy constructor takes two items:
  * the obj that it will be the proxy for (obj being proxied)
  * an obj containing the list of methods it will handle for the proxied obj (handler obj)
* the second obj is called the **handler** it intercepts the request. The handler object is made up of methods that will be used for property access. 1 of 13 different "traps".
* a **trap** is a function that will intercept calls to properties let you run code.
* if a trap is not defined, the default behavior is sent to the target object.

#### GET TRAP

* the `get` trap will take over whenever any property on the proxy is accessed.
* The `get` trap is used to "intercept" calls to properties:

```javascript
const richard = {status: 'looking for work'};
const handler = {
    get(target, propName) {
        console.log(target); // the `richard` object, not `handler` and not `agent`
        console.log(propName); // the name of the property the proxy (`agent` in this case) is checking
    }
};
const agent = new Proxy(richard, handler);
agent.status; // logs out the richard object (not the agent object!) and the name of the property being accessed (`status`)
```

##### ACCESSING THE TARGET OBJECT FROM INSIDE THE PROXY

```javascript
const richard = {status: 'looking for work'};
const handler = {
    get(target, propName) {
        console.log(target);
        console.log(propName);
        return target[propName]; // this will access the property on the target obj and will return it.
    }
};
const agent = new Proxy(richard, handler);
agent.status; // (1)logs the richard object, (2)logs the property being accessed, (3)returns the text in richard.status
```

#### SET TRAP

* used if we want to intercept calls to **change** properties.
* the `set` trap receives the object it proxies the property that is being set the new value for the proxy

```javascript
const richard = {status: 'looking for work'};
const handler = {
    set(target, propName, value) {
        if (propName === 'payRate') { // if the pay is being set, take 15% as commission
            value = value * 0.85;
        }
        target[propName] = value;
    }
};
const agent = new Proxy(richard, handler);
agent.payRate = 1000; // set the actor's pay to $1,000
agent.payRate; // $850 the actor's actual pay
```
