# Flyweight Pattern

For complete reference, click [here](http://addyosmani.com/resources/essentialjsdesignpatterns/book/#constructorpatternjavascript).

In classical object-oriented programming languages, <b>Constructor</b> means: <i>A special method used to initialize a newly created object once memory has been allocated for it.</i>

Object creation in JS:
```
var newObject = {};
 
// or
var newObject = Object.create( Object.prototype );
 
// or
var newObject = new Object(); 

```

There are then four ways in which keys and values can then be assigned to an object:

```
// 1. Dot syntax
 
// Set
newObject.someKey = "Hello World";
 
// Get
var value = newObject.someKey;
 
 
// 2. Square bracket syntax
 
// Set properties
newObject["someKey"] = "Hello World";
 
// Get properties
var value = newObject["someKey"];


// 3. Object.defineProperty
var myObj = {};
// Set properties
Object.defineProperty( myObj, "someKey", {
    value: "for more control of the property's behavior",
    writable: true,
    enumerable: true,
    configurable: true
});

// Get properties
var value = myObj.someKey;



// 4. Object.defineProperties
 
// Set properties
Object.defineProperties( newObject, {
 
  "someKey": {
    value: "Hello World",
    writable: true
  },
 
  "anotherKey": {
    value: "Foo bar",
    writable: false
  }
 
});


// Get properties
var value = myObj.anotherKey;

```

Constructors in JS:

JavaScript doesn't support the concept of <b>classes</b> but it does support special constructor functions that work with objects. By simply prefixing a call to a constructor function with the keyword "new", 
i.e:
```
  var ford = new Car("ford", "GT", 2015); // Arguments to the constructor function.

``` 
we can tell JavaScript we would like the function to behave like a constructor and instantiate a new object with the members defined by that function.

Inside a constructor, the keyword this references the new object that's being created. 

```
function Car(make, model, year) {
	// Props
	this.make = make;
	this.model = model;
	this.year = year;

	// Methods
	this.ourMagicMethod = function() {
		return this.model + this.year;
	}
}

// Usage

var ford = new Car("ford", "GT", 2015); // Arguments to the constructor function.

```

This makes, inheritance difficult and the other is that functions such as ourMagicMethod() are redefined for each of the new objects created using the Car constructor. Not optimal. 

Functions, like almost all objects in JavaScript, contain a "prototype" object. When we call a JavaScript constructor to create an object, all the properties of the constructor's prototype are then made available to the new object. In this fashion, multiple Car objects can be created which access the same prototype. We can thus extend the original example as follows:

```

function Car( model, year, miles ) {
 
  this.model = model;
  this.year = year;
  this.miles = miles;
 
}
 
 
// Note here that we are using Object.prototype.newMethod rather than
// Object.prototype so as to avoid redefining the prototype object
Car.prototype.toString = function () {
  return this.model + " has done " + this.miles + " miles";
};

```





