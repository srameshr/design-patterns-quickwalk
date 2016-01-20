# Module Pattern

For complete reference, click [here](http://addyosmani.com/resources/essentialjsdesignpatterns/book/#modulepatternjavascript).

In JavaScript, there are several options for implementing modules. These include:

<ul>
	<li>The Module pattern</li>
	<li>Object literal notation</li>
	<li>AMD modules</li>
	<li>CommonJS modules</li>
	<li>ECMAScript Harmony modules</li>
</ul>

A short refresher about JS object literals:
<ol>
  <li>An object is described as a set of comma-separated name/value pairs enclosed in curly braces.</li>
  <li>Key / Names inside the object may be either strings or identifiers that are followed by a colon. </li>
  <li>Values can be anything that is a valid JS right hand expression / value</li>
  <li>There should be no comma used after the final name/value pair in the object as this may result in errors.</li>
</ol>

```
// Example
var myObjectLiteral = {
 
    variableKey: variableValue,
 
    functionKey: function () {
      // ...
    }
};

```

Once instantinated, outside of an object, new members may be added to it using assignment as follows ```myModule.property = "someValue";```

```
// To update the above myObjectLiteral
myObjectLiteral.myKey = 10;
```
Accessing:
```
// 1. Properties
myObjectLiteral.variableKey;

// 2. Methods
myObjectLiteral.functionKey();
```


The Module Pattern: 
<ul>
  <li>The Module pattern was originally defined as a way to provide both private and public encapsulation for classes in conventional software engineering.
  </li>
  <li>In JavaScript, the Module pattern is used to further emulate the concept of classes in such a way that we're able to include both public/private methods and variables inside a single object, thus shielding particular parts from the global scope. What this results in is a reduction in the likelihood of our function names conflicting with other functions defined in additional scripts on the page.
</li>
<li>The Module pattern encapsulates "privacy", state and organization using closures.</li>
<li>This gives us a clean solution for shielding logic doing the heavy lifting whilst only exposing an interface we wish other parts of our application to use. </li>
</ul>

Example
```
var testModule = (function () {
 
  var counter = 0;
 
  return {
 
    incrementCounter: function () {
      return counter++;
    },
 
    resetCounter: function () {
      console.log( "counter value prior to reset: " + counter );
      counter = 0;
    }
  };
 
})();
 
// Usage:
 
// Increment our counter
testModule.incrementCounter();
 
// Check the counter value and reset
// Outputs: counter value prior to reset: 1
testModule.resetCounter();

```

Module Pattern Variations:
<ul>
  <li>
  	<b>Import Mixins</b>  
  </li>
  <li>Exports</li>
</ul>

<b>Import Mixins</b>

  		
  	```
  			var myModule = (function( $, _ ) {
  				function privateMethod1(){
			        $(".container").html("test");
			    }
			 
			    function privateMethod2(){
			      console.log( _.min([10, 5, 100, 2, 1000]) );
			    }
			 
			    return{
			        publicMethod: function(){
			            privateMethod1();
			        }
			    };
  			})( jQuery, _ );

  		```

<b>Exports</b>

  		```
  			 // Module object
			  var module = {},
			    privateVariable = "Hello World";
			 
			  function privateMethod() {
			    // ...
			  }
			 
			  module.publicProperty = "Foobar";
			  module.publicMethod = function () {
			    console.log( privateVariable );
			  };
			 
			  return module;
  		```

