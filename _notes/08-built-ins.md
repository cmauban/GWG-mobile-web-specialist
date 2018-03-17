# Lesson 8: Built-ins

#### SYMBOLS

* A unique identifier, most often used to uniquely identify properties within an object.
  * ie. used if two keys are the same (bananas in fruit bowl ex) change the bowls properties to use symbols, the banana doesn't get overwritten by the second banana.
* to create a symbol, you write `Symbol()` with an optional string as its **description**.
```JavaScript
const sym1 = Symbol('apple');
console.log(sym1);
```
> `Symbol(apple)`

#### SETS

* a Set is an object that has no repeading values and lets you store unique items.
* you can add/remove items and loop over a set.
* they are NOT indexed based (not based on their position).
* items in a Set cannot be accessed individually.

##### HOW TO CREATE A SET:
```JavaScript
const games = new Set();
console.log(games);
```

> `Set {} // empty set games with no items`

```JavaScript
const games = new Set(['Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart', 'Super Mario Bros.']);
console.log(games);
```
automatically removes the duplicate entry ``"Super Mario Bros."`` :
> `Set {'Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart'}`
