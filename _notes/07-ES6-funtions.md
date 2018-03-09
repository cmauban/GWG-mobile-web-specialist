# Lesson 7: ES6 Functions

*need to add evernote notes*

### JavaScript Classes
* A `class` is just a function.
* New keywords: `super` and `extends`.
* The new `constructor` method exists in a class and is used to initialize new objects.
  * ran whenever the class is called.
  * `constructor(size, leaves){..}` = old `function Tree(size, leaves){..}`
* Methods that appear in the class definition, `startEngines()`, are under the hood, placed on that class's prototype object.
  * Method names that appear inside a class definition is the same thing as adding that method to the prototype.
  * `changeSeason(season){...}` = old `Tree.prototype.changeSeason = function (season){...}`
* Everything's contained in a class. Instead of having the constructor function in one place, then adding methods to the prototype one-by-one, you can do everything all at once.
* When creating a new instance of a JavaScript class, the `new` keyword msut be used. ie: `const myToy2 = new Toy();`

This ES5:
```JavaScript
function Plane(numEngines){
  this.numEngines = numEngines;
  this.enginesActive = false;
}

Plane.prototype.startEngines = function () {
  console.log('starting engines...');
  this.enginesActive = true;
}
```

Will convert to:
```JavaScript
class Plane {
  constructor(numEngines){
    this.numEngines = numEngines;
    this.enginesActive = false;
  }

  startEngines(){
    console.log('starting engines...');
    this.enginesActive = true;
  }
}
```

#### STATIC METHODS

`badWeather()` method is accessed directly on the `Plane` class so you can call it like this:
`Plane.badWeather([plane1, plane2, plane3]);`

```JavaScript

class Plane {
  constructor(numEngines){
    this.numEngines = numEngines;
    this.enginesActive = false;
  }

  static badWeather(planes) {
    for (plane of planes) {
      plane.enginesActive = false;
    }
  }

  startEngines(){
    console.log('starting engines...');
    this.enginesActive = true;
  }
}
```


#### `SUPER` & `EXTENDS`

* To get from the subclass (`Maple`) to the parent class (`Tree`), the `super` keyword is used.
  * `super` can be used differently.
    * as a function, `super(size, leaves);`
    * or as an object, `super.changeSeason(season);`
* `super(size, barkColor, leaves);` = old `Tree.call(this, size, barkColor, leaves);`
* `super` must be called before `this`.
* when you call `super` you need to pass the arguments that are defined in the parent class.

```JavaScript
class Tree { // class
  constructor(size = '10', leaves = {spring: 'green', summer: 'green', fall: 'orange', winter: null}) {
    this.size = size;
    this.leaves = leaves;
    this.leafColor = null;
  }

  changeSeason(season) {
    this.leafColor = this.leaves[season];
    if (season === 'spring') {
      this.size += 1;
    }
  }
}

class Maple extends Tree { // Maple is a subclass of Tree by using extends
  constructor(syrupQty = 15, size, leaves) {
    super(size, leaves); // used to get from the subclass to the parent class (function)
    this.syrupQty = syrupQty;
  }

  changeSeason(season) {
    super.changeSeason(season); // super is used as an object vs. a funtion
    if (season === 'spring') {
      this.syrupQty += 1;
    }
  }

  gatherSyrup() {
    this.syrupQty -= 3;
  }
}

const myMaple = new Maple(15, 5);
myMaple.changeSeason('fall');
myMaple.gatherSyrup();
myMaple.changeSeason('spring');
```
