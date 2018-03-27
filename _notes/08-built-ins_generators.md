# Lesson 8: Built-ins - GENERATORS & ITERATORS

* function that is able to pause its execution while also maintaining its own state.
* generators are great for iterating over a list of items one at a time so you can handle each item on its own before moving on to the next one.
* add an `*` between the `function` and `name` to make it a generator.
* when a generator is invoked, it doesn't actually run any code inside that function. instead, it creates a returns an iterator.

### YIELD KEYWORD

* used to pause the generator.
* used to get data out of the generator
* The `yield` keyword can only be used inside generator functions.

```javascript
function* getEmployee() {
    console.log('the function has started');

    const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

    for (const name of names) {
        console.log(name);
        yield;
    }

    console.log('the function has ended');
}

const generatorIterator = getEmployee();
generatorIterator.next();
```

> `the function has started Amanda`

* you can also use `yield` to send data from the generator back to the 'outside' world.

This has the code 'return' the name and then pause:

```javascript
function* getEmployee() {
    console.log('the function has started');

    const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

    for (const name of names) {
        yield name; // instead of console.log(name), when the generator is run, it will 'yield' the name back out of the function and then pause its execution.
    }

    console.log('the function has ended');
}

const generatorIterator = getEmployee();
let result = generatorIterator.next();
result.value // is "Amanda"

generatorIterator.next().value // is "Diego"
generatorIterator.next().value // is "Farrin"
```
### `.next()` METHOD

* used to send data back into the generator

```javascript
function* getEmployee() {
    const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];
    const facts = [];

    for (const name of names) {
        // yield *out* each name AND store the returned data into the facts array
        facts.push(yield name);
    }

    return facts;
}

const generatorIterator = getEmployee();

// get the first name out of the generator
let name = generatorIterator.next().value;

// pass data in *and* get the next name
name = generatorIterator.next(`${name} is cool!`).value;

// pass data in *and* get the next name
name = generatorIterator.next(`${name} is awesome!`).value;

// pass data in *and* get the next name
name = generatorIterator.next(`${name} is stupendous!`).value;

// you get the idea
name = generatorIterator.next(`${name} is rad!`).value;
name = generatorIterator.next(`${name} is impressive!`).value;
name = generatorIterator.next(`${name} is stunning!`).value;
name = generatorIterator.next(`${name} is awe-inspiring!`).value;

// pass the last data in, generator ends and returns the array
const positions = generatorIterator.next(`${name} is magnificent!`).value;

// displays each name with description on its own line
positions.join('\n');
```
