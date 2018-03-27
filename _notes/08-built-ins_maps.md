# Lesson 8: Built-ins - MAPS

* Sets:Arrays as Maps:objects
* Maps store key-value pairs similar to how objects contain named properties with values.
* you can't create Maps from a list of values. instead, you add key-values by using the Map's `.set()` method.

### HOW TO CREATE A MAP
```javascript
const employees = new Map();
console.log(employees);
```
> `Map {}`

### `.set()` method

* takes two arguments: key and value.
* to remove key-value pairs, use `.delete()` method.
* use `.clear()` method to remove all key-value pairs from the Map.

```javascript
const employees = new Map();

employees.set('james.parkes@udacity.com', {
    firstName: 'James',
    lastName: 'Parkes',
    role: 'Content Developer'
});
employees.set('julia@udacity.com', {
    firstName: 'Julia',
    lastName: 'Van Cleve',
    role: 'Content Developer'
});
employees.set('richard@udacity.com', {
    firstName: 'Richard',
    lastName: 'Kalehoff',
    role: 'Content Developer'
});

console.log(employees);
```
> `Map {'james.parkes@udacity.com' => Object {...}, 'julia@udacity.com' => Object {...}, 'richard@udacity.com' => Object {...}}`

### `.has()` method

* after you built your Map, you can use the `.has()` method to check if a key-value pair exists in your Map by passing it a key.

```javascript
const members = new Map();

members.set('Evelyn', 75.68);
members.set('Liam', 20.16);
members.set('Sophia', 0);
members.set('Marcus', 10.25);

console.log(members.has('Xavier'));
console.log(members.has('Marcus'));
```
> `false true`

### `.get()` method

```javascript
console.log(members.get('Evelyn'));
```
> `75.68`

### 2. USING THE MapIterator

* use `.keys()` and `.values()` will return a new iterator object called `MapIterator`
* use `.next()` to loop through
* use `.values()` to access the maps values.

```javascript
let iteratorObjForKeys = members.keys();
iteratorObjForKeys.next();
```
> `Object {value: 'Evelyn', done: false}`

```javascript
let iteratorObjForValues = members.values();
iteratorObjForValues.next();
```
> `Object {value: 75.68, done: false}`

### 2. USING A for...of Loop
* another way of looping. but you dont get back a key or a value, instead the key-value pair is split up into an array where the first element is the key and the second is the value.

```javascript
for (const member of members) {
  console.log(member);
}
```
> ` ['Evelyn', 75.68]
 ['Liam', 20.16]
 ['Sophia', 0]
 ['Marcus', 10.25]`

 ```javascript
 for (const member of members) {
   [key, value] = member
   console.log(key, value);
 }
 ```
 > ` Evelyn, 75.68
  Liam, 20.16
  Sophia, 0
  Marcus, 10.25`

### 3. USING A forEach Loop

* Notice how with the help of an arrow function, the forEach loop reads fairly straightforward. For each value and key in members, log the value and key to the console.

```javascript
members.forEach((value, key) => console.log(key, value));
```
> ` 'Evelyn' 75.68
 'Liam' 20.16
 'Sophia' 0
 'Marcus' 10.25`

### WeakMap

 * can only contain objects as keys
 * not iterable, which means it cannot be looped
 * does not have a `.clear()` method
 * you'll get an error if you don't add an object as a key

 ```JavaScript
 const book1 = { title: 'Pride and Prejudice', author: 'Jane Austen' };
 const book2 = { title: 'The Catcher in the Rye', author: 'J.D. Salinger' };
 const book3 = { title: 'Gulliver’s Travels', author: 'Jonathan Swift' };

 const library = new WeakMap();
 library.set(book1, true);
 library.set(book2, false);
 library.set(book3, true);

 console.log(library);
 ```
 > `WeakMap {Object {title: 'Pride and Prejudice', author: 'Jane Austen'} => true, Object {title: 'The Catcher in the Rye', author: 'J.D. Salinger'} => false, Object {title: 'Gulliver’s Travels', author: 'Jonathan Swift'} => true}`
