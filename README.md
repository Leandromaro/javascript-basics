
# javascript-basics


## Difference between “let” and “var”
Main difference is scoping rules. Variables declared by var keyword are scoped to the immediate function body (hence the function scope) while let variables are scoped to the immediate enclosing block denoted by { } (hence the block scope).
	
	function run() {
  		var foo = "Foo";
  		let bar = "Bar";
	
	console.log(foo, bar);
  	
  	{
    	let baz = "Bazz";
    	console.log(baz);
  	}
  		console.log(baz); // ReferenceError
	}
	run();
	

### Creating global object property

At the top level, let, unlike var, does not create a property on the global object:

	var foo = "Foo";  // globally scoped
	let bar = "Bar"; // globally scoped

	console.log(window.foo); // Foo
	console.log(window.bar); // undefined
	
### Redeclaration

	In strict mode, var will let you re-declare the same variable in the same scope while let raises a SyntaxError.

	'use strict';
	var foo = "foo1";
	var foo = "foo2"; // No problem, 'foo' is replaced.

	let bar = "bar1";
	let bar = "bar2"; // SyntaxError: Identifier 'bar' has already been declared

## Const keyword

ES6 provides a new way of declaring a constant by using the  `const`  keyword. The  `const`  keyword creates a read-only reference to a value.

	const  VARIABLE_NAME  =  value;

By convention, the constant identifiers in JavaScript are in uppercase.

The  `const`  keyword works like the  [let](http://www.javascripttutorial.net/es6/javascript-let/)  keyword. But the  `const`  keyword creates block-scoped variables whose values can’t be reassigned.

The variables declared by the  `let`  keyword are mutual. It means that you can change their values anytime you want as shown in the following example.
	
	let  a  =  10;
	a  =  20;
	a  =  a  +  5;
	console.log(a);  // 35

However, variables created by the  `const`  keyword are immutable. In other words, you can’t reassign them different values. Trying to reassign a constant variable will result in a  `TypeError`.

	const  RATE  =  0.1;
	RATE  =  0.2;  // TypeError

In addition, the variable you declare using the  `const`  keyword must be immediately initialized to a value. The following example causes a  `SyntaxError`  due to missing the initializer in the  `const`variable declaration

	const  RED;  // SyntaxError

### JavaScript const and object

The  `const`  keyword ensures that the variable it creates is read-only. It does not mean that the actual value to which the  `const`  variable reference is immutable. See the following example.
	
	const  person  =  {  age:  20  };
	person.age  =  30;  // OK
	console.log(person.age);  // 30

Even though the  `person`  variable is a constant. However, you can change the value of its property. But you cannot reassign a different value to the person constant.

	person  =  {age:  40};  // TypeError

If you want the value of the `person`  object to be immutable, you have to freeze it as follows.

	const  person  =  Object.freeze({age:  20});
	person.age  =  30;  // TypeError

Note that  `Object.freeze()`  is shallow, meaning that it only freezes the properties of the object, not the objects referenced by its properties. For example, the  `company` object is constant and frozen.

	const  company  =  Object.freeze({
		name:  'ABC corp',
		address:  {
		street:  'North 1st street',
		city:  'San Jose',
		state:  'CA',
		zipcode:  95134
		}
	});

But the  `company.address`  object is not immutable, you can add a new property to the  `company.address`  object as follows:

	company.address.country  =  'USA';  // OK	

## JavaScript const in a for loop

ES6 provides a new construct called  [`for...of`](http://www.javascripttutorial.net/es6/javascript-for-of/)  that allows you to create a loop iterating over iterable objects such as an [array](http://www.javascripttutorial.net/javascript-array/), a  [Map](http://www.javascripttutorial.net/es6/javascript-map/), or a  [Set](http://www.javascripttutorial.net/es6/javascript-set/), etc.

	var  scores  =  [75,  80,  95];

	for  (let score of scores)  {
		console.log(score);
	}

If you don’t intend to modify the  `score`  variable inside the loop, you declare it using the  `const`keyword instead.

	var  scores  =  [75,  80,  95];

	for  (const  score of scores)  {
		console.log(score);
	}

This works because, in each iteration, the  `for...of` creates a new binding for the  `const`  keyword. In other words, the score constant is created in each iteration.

Notice that the  `const`  will not work in an imperative  [for](http://www.javascripttutorial.net/javascript-for-loop/) loop. Trying to use the const keyword to declare a variable in the imperative  `for`  loop will result in a TypeError as shown below.
	
	for  (const  i  =  0;  i  <  scores.length;  i++)  {  // TypeError
		console.log(scores[i]);
	}

The reason is that the declaration is only evaluated once before the loop body starts.

## Closures:
Closure in layman’s terms is simply a function inside a function, also called nested function. It looks pretty straightforward when we see it like this but the real magic is related to its scopes. A closure has three scopes, nested function has access to variables defined in its own scope, in the scope of its parent function and the global variables. This behavior of closures can be very handy when It comes to programming in Javascript.

```
function foo() {
  
	var firstName = "John";			//property
  var lastName = "Doe";				// property
  var getFullName = function() {	//method
    return firstName + " " + lastName;
  }
	
	
	//this return works like an access modifier
	//only getFullName() method is accessable of foo object
  return {		
    getFullName: getFullName
  }
}

var object = foo();
console.log(object.getFullName());
```
