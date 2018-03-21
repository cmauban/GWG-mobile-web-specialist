# Lesson 8: Built-ins

### SYMBOLS

* A unique identifier, most often used to uniquely identify properties within an object.
  * ie. used if two keys are the same (bananas in fruit bowl ex) change the bowls properties to use symbols, the banana doesn't get overwritten by the second banana.
* to create a symbol, you write `Symbol()` with an optional string as its **description**.
```JavaScript
const sym1 = Symbol('apple');
console.log(sym1);
```
> `Symbol(apple)`

### SETS

* a Set is an object that has no repeading values and lets you store unique items.
* you can add/remove items and loop over a set.
* they are NOT indexed based (not based on their position).
* items in a Set cannot be accessed individually.

#### HOW TO CREATE A SET:
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

#### MODIFYING A SET:

###### `add()` method
```JavaScript
const games = new Set(['Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart', 'Super Mario Bros.']);

games.add('Banjo-Tooie');

console.log(games);
```
> `Set {'Banjo-Kazooie', 'Mario Kart', 'Banjo-Tooie', 'Super Mario Bros.'}`

* `games.add('Banjo-Tooie');`
* if you attempt to `add()` an item to the set that is already there, it won't throw an error, but it won't be added to the Set and the Set will remain unchanged.
* `add()` returns the `Set` if an item is successfully added.

##### `delete()` method
* `games.delete('Super Mario Bros.');`
* if you try to `delete()` an item that is not in a `Set`, you won't receive an error, it will just be unchanged.
* `delete()` returns a Boolean.
* if you want to delete all items from a set, you could use the `clear()` method.
```JavaScript
games.clear()
console.log(games);
```
> `Set {}`

#### WORKING W/ SETS:

##### `.size` property to return the number of items in a set.
```JavaScript
const months = new Set(['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']);
console.log(months.size);
```
> 12

Since `Sets` cant be accessed by index, they have to use `.size`, not `.length`.

##### `.has()` method to check if an item exists in a Set.
```JavaScript
console.log(months.has('September'));
```
> `true` // returns a Boolean.

##### `.values()` method to return values in a set.
```JavaScript
console.log(months.values());
```
> `SetIterator {'January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'}`

The return value of `.values()` is a `SetIterator`.
`.keys()` is an alias of `.values()`.
