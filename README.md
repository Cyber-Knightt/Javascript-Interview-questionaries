# Javascript-Interview-questions

# Table of Contents

<!-- TOC_START -->
| No. | Questions |
| --- | --------- |
| 1 | [What are the possible ways to create objects in JavaScript](#what-are-the-possible-ways-to-create-objects-in-javascript) |
| 2 | [What is a prototype chain](#what-is-a-prototype-chain) |
| 3 | [What is closures](#what-is-closures) |
| 4 | [What is a JavaScript Hoisting](#what-is-a-javaScript-hoisting) |
| 5 | [What is a Event loop](#what-is-a-event-loop) |
| 6 | [What are TypeScript Interfaces](#What-are-TypeScript-Interfaces) |
| 7 | [Characteristics of javascript strict-mode](#Characteristics-of-javascript-strict-mode) |
| 8 | [What is Lexical Scoping?](#What-is-Lexical-Scoping?) |
| 9 | [What is function declaration vs function expression?](#What-is-function-declaration-vs-function-expression?) |
| 10 | [What are the Arrow functions](#What-are-the-Arrow-functions) |
| 11 | [What is an anonymous function](#What-is-an-anonymous-function) |
| 12 | [Immediately invoked function execution](#Immediately-invoked-function-execution) |
| 13 | [JavaScript pass-by-value or pass-by-reference](#JavaScript-pass-by-value-or-pass-by-reference) |
| 14 | [What is Literals](#What-is-Literals) |
| 15 | [What is a first class function](#what-is-a-first-class-function) |
| 16 | [What is a first order function](#what-is-a-first-order-function) |
| 17 | [What is a higher order function](#what-is-a-higher-order-function) |
| 18 | [What is a unary function](#what-is-a-unary-function) |
| 19 | [What is the currying function](#what-is-the-currying-function) |
| 20 | [What is a pure function](#what-is-a-pure-function) |
| 21 | [What is the Temporal Dead Zone](#what-is-the-temporal-dead-zone) |
| 22 | [What is memoization](#what-is-memoization) |

<!-- TOC_END -->


<!-- QUESTIONS_START -->
1. ### What are the possible ways to create objects in JavaScript

   There are many ways to create objects in javascript as mentioned below:

   1. **Object literal syntax:**

      The object literal syntax (or object initializer), is a comma-separated set of name-value pairs wrapped in curly braces.

      ```javascript
      var object = {
           name: "Sudheer",
           age: 34
      };
      ```

      Object literal property values can be of any data type, including array, function, and nested object.

      **Note:** This is one of the easiest ways to create an object.

   2. **Object constructor:**

      The simplest way to create an empty object is using the `Object` constructor. Currently this approach is not recommended.

      ```javascript
      var object = new Object();
      ```

      The `Object()` is a built-in constructor function so "new" keyword is not required. The above code snippet can be re-written as:

      ```javascript
      var object = Object();
      ```

   3. **Object's create method:**

      The `create` method of Object is used to create a new object by passing the specificied prototype object and properties as arguments, i.e., this pattern is helpful to create new objects based on existing objects.
      The second argument is optional and it is used to create properties on a newly created object.

      The following code creates a new empty object whose prototype is null.

      ```javascript
      var object = Object.create(null);
      ```
      The following example creates an object along with additional new properties.

      ```javascript
      let vehicle = {
        wheels: '4',
        fuelType: 'Gasoline',
        color: 'Green'
      }
      let carProps = {
        type: {
          value: 'Volkswagen'
        },
        model: {
          value: 'Golf'
        }
      }

      var car = Object.create(vehicle, carProps);
      console.log(car);
      ```

   4. **Function constructor:**

      In this approach, create any function and apply the new operator to create object instances.

      ```javascript
      function Person(name) {
        this.name = name;
        this.age = 21;
      }
      var object = new Person("Sudheer");
      ```

   5. **Function constructor with prototype:**

      This is similar to function constructor but it uses prototype for their properties and methods,

      ```javascript
      function Person() {}
      Person.prototype.name = "Sudheer";
      var object = new Person();
      ```

      This is equivalent to creating an instance with Object.create method with a function prototype and then calling that function with an instance and parameters as arguments.

      ```javascript
      function func() {}

      new func(x, y, z);
      ```

      **(OR)**

      ```javascript
      // Create a new instance using function prototype.
      var newInstance = Object.create(func.prototype)

      // Call the function
      var result = func.call(newInstance, x, y, z),

      // If the result is a non-null object then use it otherwise just use the new instance.
      console.log(result && typeof result === 'object' ? result : newInstance);
      ```
   6. **Object's assign method:**

      The `Object.assign` method is used to copy all the properties from one or more source objects and stores them into a target object.

      The following code creates a new staff object by copying properties of his working company and the car he owns.

      ```javascript
      const orgObject = { company: 'XYZ Corp'};
      const carObject = { name: 'Toyota'};
      const staff = Object.assign({}, orgObject, carObject);
      ```

   7. **ES6 Class syntax:**

      ES6 introduces class feature to create objects.

      ```javascript
      class Person {
        constructor(name) {
          this.name = name;
        }
      }

      var object = new Person("Sudheer");
      ```

   8. **Singleton pattern:**

      A Singleton is an object which can only be instantiated one time. Repeated calls to its constructor return the same instance. This way one can ensure that they don't accidentally create multiple instances.

      ```javascript
      var object = new (function () {
        this.name = "Sudheer";
      })();
      ```

      **[⬆ Back to Top](#table-of-contents)**

2. ### What is a prototype chain

   **Prototype chaining** is used to build new types of objects based on existing ones. It is similar to inheritance in a class based language. i.e, When you create an object using a constructor function or a class, the created object inherits properties from a prototype object.

   The prototype on object instance is available through **Object.getPrototypeOf(object)** or **\_\_proto\_\_** property whereas prototype on constructor function is available through **Object.prototype**.

   ![Screenshot](images/prototype_chain.png)

   **[⬆ Back to Top](#table-of-contents)**

3. ### What is closures

	A closure is a function that has been bundled together (enclosed) with references to its surroundings (the lexical environment). In other words, a closure allows an inner function to access the scope of an outside function. Closures are formed every time a function is created in JavaScript, during function creation time. An example of closures in Javascript is given below:

	```javascript
	function subtractor(subtractingInteger) {
		return function(a) {
			return a - subtractingInteger;
		};
	}

	var subtract2 = subtractor(2);
	var subtract5 = subtractor(5);
	console.log(subtract2(5));  // 3 is logged
	console.log(subtract5(5)); // 0 is logged
	```
	In this example, we have developed a function subtractor(subtractingInteger) that takes a single parameter subtractingInteger and returns a new function. Its return function accepts only one input, a, and returns the difference of a and subtractingInteger. The function 'subtractor' is essentially a function factory. It creates functions that have the ability to subtract a specified value from their arguments. The function factory creates two new functions in the example above: one that subtracts 2 from its argument and one that subtracts 5 from its arguments. Both subtract2 and subtract5 are closures. They have the same function body definition, but they hold lexical surroundings that are distinct. subtractingInteger is 2 in subtract2's lexical environment, but subtractingInteger is 5 in subtract5's lexical environment.

	**[⬆ Back to Top](#table-of-contents)**

4. ### JavaScript Hoisting
	Prior to executing the code, the interpreter appears to relocate the declarations of functions, variables, and classes to the top of their scope using a process known as Hoisting in JavaScript. Functions can be securely utilised in code before they have been declared thanks to hoisting. Variable and class declarations are likewise hoisted, allowing them to be referenced prior to declaration. It should be noted that doing so can result in unforeseen mistakes and is not recommended. There are usually two types of Hoisting:

	Function Hoisting: Hoisting has the advantage of allowing you to use a function before declaring it in your code as shown in the code snippet given below. Without function hoisting, we would have to first write down the function display and only then can we call it.

	```javascript
	display("Lion");
	function display(inputString) {
		console.log(inputString); // 'Lion' gets logged 
	}
	```

	Variable Hoisting: You can use a variable in code before it is defined and/or initialised because hoisting works with variables as well. JavaScript, however, only hoists declarations, not initializations! Even if the variable was initially initialised then defined, or declared and initialised on the same line, initialization does not occur until the associated line of code is run. The variable has its default initialization till that point in the execution is reached (undefined for a variable declared using var, otherwise uninitialized). An example of variable hoisting is shown below:

	```javascript
	console.log(x) // 'undefined' is logged from hoisted var declaration (instead of 7)
	var x // Declaration of variable x
	x = 7; // Initialization of variable x to a value 7
	console.log(x); // 7 is logged post the line with initialization's execution
	```

	**[⬆ Back to Top](#table-of-contents)**

5. ### What is a Event loop

	The Node.js event loop is a crucial concept in understanding how Node.js manages asynchronous operations and handles concurrency. Node.js is designed to be non-blocking and asynchronous, which allows it to efficiently handle a large number of I/O-bound operations without getting blocked by any single operation.

	Here's how the Node.js event loop works:

	1. Event Loop: The event loop is a central component of Node.js that manages all the asynchronous operations. It constantly checks for new events in the event queue and processes them in a loop.

	2. Event Queue: The event queue holds various types of events, such as callbacks, timers, and I/O events, that are generated as a result of asynchronous operations. These events are added to the queue when they are triggered but are not executed immediately.

	3. Callbacks: Callbacks are functions that are provided as arguments to asynchronous functions. They are executed once the corresponding asynchronous operation is completed and the event loop reaches the event in the queue. This mechanism allows Node.js to perform tasks without waiting for the completion of one task before moving on to the next.

	4. Timers: Node.js provides two types of timers: setTimeout() and setInterval(). These timers schedule callbacks to be executed after a specified amount of time or at regular intervals.

	5. I/O Operations: When Node.js performs I/O operations (e.g., reading from or writing to files, making network requests), it does not block the execution of the rest of the program. Instead, it delegates the I/O operation to the operating system and registers a callback to be executed when the operation is complete.

	6. Microtask Queue: In addition to the event queue, Node.js also maintains a microtask queue. Microtasks are tasks that have higher priority than regular callbacks and are executed before the next iteration of the event loop. Promises and certain APIs (e.g., process.nextTick()) add tasks to the microtask queue.

	GIF [Screenshot](images/event-loop.gif)

	Here's a simplified step-by-step breakdown of how the event loop works:

	1. Check the event queue for pending events.
	2. If there are pending events, dequeue an event and execute its associated callback.
	3. Execute any microtasks that are in the microtask queue.
	4. Perform any ready I/O operations.
	5. Check if any scheduled timers have expired. If yes, execute their callbacks.
	6. Repeat the process from step 1.

	Please check [First link](https://dev.to/endeavourmonk/nodejs-event-loop-46oo#:~:text=The%20event%20loop%20is%20a%20single%2Dthreaded%20loop%2C%20which%20means,in%20a%20non%2Dblocking%20manner.)
	[Second Link](https://www.freecodecamp.org/news/nodejs-eventloop-tutorial/)

	**[⬆ Back to Top](#table-of-contents)**

6. ### What are TypeScript Interfaces

	An interface in TypeScript defines the structure or skeleton of an object. It enforces a specific syntax on classes, specifying the types of data an object must have. Essentially, an interface acts as a contract that describes the shape of an object.

	Interfaces are capable of describing the wide range of shapes that JavaScript objects can take. In addition to describing an object with properties, interfaces are also capable of describing function types. To describe a function type with an interface, we give the interface a call signature.
	An interface is defined using the interface keyword:
	```javascript
	interface InterfaceName{
		PropertyName: Type;
		methodName() => Type;
	}
	// Interface for Array
	interface ForList {
    	[index:number]: string
	}
	let newArray: ForList = ["Interface", "for", "Array"];
	console.log(newArray); 
	```
	**[⬆ Back to Top](#table-of-contents)**

7. ### Characteristics of javascript strict-mode

	1. Strict mode does not allow duplicate arguments and global variables.
	2. One cannot use JavaScript keywords as a parameter or function name in strict mode.
	3. All browsers support strict mode. 
	4. Strict mode can be defined at the start of the script with the help of the keyword ‘use strict’. 

	**[⬆ Back to Top](#table-of-contents)**

8. ### What is Lexical Scoping?

	Lexical Scoping in JavaScript can be performed when the internal state of the JavaScript function object consists of the function’s code as well as references concerning the current scope chain.
	The ability of the function to be able to access variables of the parent is called lexical scope. In other words, the inner child function is always lexically bound to its parent and can always access its variables.
	Lexical scope in this case is the scope where the target variables were created not called. You can call a variable in one place but declare it in another place, for example, the parent function.

	Read More[Link](https://medium.com/@catherineisonline/what-is-lexical-scope-in-javascript-708b1d1487ea)

	**[⬆ Back to Top](#table-of-contents)**

9. ### What is function declaration vs function expression?

	Functions are the main “building blocks” of the program. They allow the code to be called many times without repetition. The main purposes of functions: to avoid code duplication.
	Parameter - A parameter is the variable listed inside the parentheses in the function declaration (it’s a declaration time term).
	Argument - An argument is the value that is passed to the function when it is called (it’s a call time term).

	Function Declaration - a function, declared as a separate statement, in the main code flow:

	```javascript
	function showMessage() {
  		alert( 'Hello everyone!' );
	}
	```
	A Function Declaration can be called earlier than it is defined.
	```javascript
	sayHi("John"); // Hello, John

	function sayHi(name) {
		alert( `Hello, ${name}` );
	}
	```
	In strict mode, when a Function Declaration is within a code block, it’s visible everywhere inside that block. But not outside of it.


	Function expressions - As the function creation happens in the context of the assignment expression (to the right side of =), this is a Function Expression.
	```javascript
	let sayHi = function() {
		alert( "Hello" );
	};
	```
	A Function Expression is created when the execution reaches it and is usable only from that moment.
	```javascript
	sayHi("John"); // error!

	let sayHi = function(name) {  // (*) no magic any more
		alert( `Hello, ${name}` );
	}; 
	```

	**[⬆ Back to Top](#table-of-contents)**

10. ### What are the Arrow functions?
	An arrow function is a shorter/concise syntax for a function expression and does not have its own this, arguments, super, or new.target. These functions are best suited for non-method functions, and they cannot be used as constructors.

	```javascript
	let func = (arg1, arg2, ..., argN) => expression;

	let sum = (a, b) => a + b;

	/* This arrow function is a shorter form of:

	let sum = function(a, b) {
		return a + b;
	};
	*/

	alert( sum(1, 2) ); // 3
	```

	Arrow functions have no “this”. If this is accessed, it is taken from the outside.

	For instance, we can use it to iterate inside an object method:
	```javascript
	let group = {
		title: "Our Group",
		students: ["John", "Pete", "Alice"],

		showList() {
			this.students.forEach(
			student => alert(this.title + ': ' + student)
			);
		}
	};

	group.showList();
	```
	Here in forEach, the arrow function is used, so this.title in it is exactly the same as in the outer method showList. That is: group.title.

	If we used a “regular” function, there would be an error:

	Arrow functions can’t run with new
	Not having this naturally means another limitation: arrow functions can’t be used as constructors. They can’t be called with new.

	Arrow functions VS bind
	There’s a subtle difference between an arrow function => and a regular function called with .bind(this):

	1. .bind(this) creates a “bound version” of the function.
	2. The arrow => doesn’t create any binding. The function simply doesn’t have this. The lookup of this is made exactly the same way as a regular variable search: in the outer lexical environment.

	Arrows have no “arguments”
	Arrow functions also have no arguments variable.

	That’s great for decorators, when we need to forward a call with the current this and arguments.

	For instance, defer(f, ms) gets a function and returns a wrapper around it that delays the call by ms milliseconds:
	```javascript
	function defer(f, ms) {
		return function() {
			setTimeout(() => f.apply(this, arguments), ms);
		};
	}

	function sayHi(who) {
		alert('Hello, ' + who);
	}

	let sayHiDeferred = defer(sayHi, 2000);
	sayHiDeferred("John"); // Hello, John after 2 seconds
	```
	The same without an arrow function would look like:
	```javascript
	function defer(f, ms) {
		return function(...args) {
			let ctx = this;
			setTimeout(function() {
			return f.apply(ctx, args);
			}, ms);
		};
	}
	```
	Here we had to create additional variables args and ctx so that the function inside setTimeout could take them.

	**[⬆ Back to Top](#table-of-contents)**

11. ### What is an anonymous function?
	An anonymous function is a function without a name. The following shows how to define an anonymous function:
	```javascript
	(function () {
		//...
	});
	```
12. ### Immediately invoked function execution?
	If you want to create a function and execute it immediately after the declaration, you can declare an anonymous function like this:
	```javascript
	(function() {
		console.log('IIFE');
	})();
	```
	The primary reason to use an IIFE is to obtain data privacy because any variables declared within the IIFE cannot be accessed by the outside world. i.e, If you try to access variables from the IIFE then it throws an error as below,
	```javascript
	(function () {
		var message = "IIFE";
		console.log(message);
	})();
	console.log(message); //Error: message is not defined
	```
	Sometimes, you may want to pass arguments into an anonymous function, like this:
	```javascript
	let person = {
		firstName: 'John',
		lastName: 'Doe'
	};

	(function () {
		console.log(person.firstName + ' ' + person.lastName);
	})(person);
	```
	**[⬆ Back to Top](#table-of-contents)**

13. ### JavaScript pass-by-value or pass-by-reference?	

	Pass by Value
	JavaScript is primarily a “pass by value” language. But what does this mean?

	Pass by value means when a variable is assigned to another variable, the value stored in the variable is copied into the new variable. They are independent of each other, each occupying its own memory space.
	```javascript
	let a = 10;
	let b = a;

	a = 20;

	console.log(a); // Outputs: 20
	console.log(b); // Outputs: 10
	```

	-> When a function is called, the value of the variable is directly passed as an argument. Therefore, any modifications made inside the function do not impact the original value.
	-> The parameters passed as arguments generate their own copies. Consequently, any alterations made inside the function apply to the copied value, not the original value.
	```javascript
	function Passbyvalue(a, b) {
		let tmp;
		tmp = b;
		b = a;
		a = tmp;
		console.log(`Inside Pass by value function -> a = ${a} b = ${b}`); // Output a =2 b =1
	}

	let a = 1;
	let b = 2;
	console.log(`Before calling Pass by value Function -> a = ${a} b = ${b}`);//Output a = 1 b = 2

	Passbyvalue(a, b);

	console.log(`After calling Pass by value Function -> a =${a} b = ${b}`);// Output a =1 b = 2
	```

	Pass by Reference
	While JavaScript is primarily a “pass by value” language, it uses a concept called “pass by reference” when dealing with objects (including arrays and functions).

	When an object is created in JavaScript, it is stored in a memory space, and the variable associated with it stores the memory address or reference where the object is stored.

	If you assign this object variable to another variable, it does not copy the object. Instead, it copies the reference to the object. Both variables now point to the same memory space, which means changes through one variable are reflected when accessing the object through the other variable.
	```javascript
	let obj1 = { value: 10 };
	let obj2 = obj1;

	obj1.value = 20;

	console.log(obj1.value); // Outputs: 20
	console.log(obj2.value); // Outputs: 20
	```
	In JavaScript, all function arguments are always passed by value. It means that JavaScript copies the values of the variables into the function arguments.
	In Pass by Reference, Function is called by directly passing the reference/address of the variable as an argument. So changing the value inside the function also change the original value. In JavaScript array and Object follows pass by reference property.
	In Pass by reference, parameters passed as an arguments does not create its own copy, it refers to the original value so changes made inside function affect the original value. 

	```javascript
	function PassbyReference(obj) {
		let tmp = obj.a;
		obj.a = obj.b;
		obj.b = tmp;

		console.log(`Inside Pass By Reference Function -> a = ${obj.a} b = ${obj.b}`); // Output  a = 20 b = 10
	}

	let obj = {
		a: 10,
		b: 20

	}
	console.log(`Before calling Pass By Reference Function -> a = ${obj.a} b = ${obj.b}`); // Output  a = 10 b = 20

	PassbyReference(obj)

	console.log(`After calling Pass By Reference Function -> a = ${obj.a} b = ${obj.b}`); // Output  a = 20 b = 10
	```

14. ### What is Literals?

	Literals represent values in JavaScript. These are fixed values—not variables—that you literally provide in your script.
	Read More[Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types#literals)

15. ### What is a first class function

    In Javascript, functions are first class objects. First-class functions means when functions in that language are treated like any other variable.

    For example, in such a language, a function can be passed as an argument to other functions, can be returned by another function and can be assigned as a value to a variable. For example, in the below example, handler functions assigned to a listener

    ```javascript
    const handler = () => console.log("This is a click handler function");
    document.addEventListener("click", handler);
    ```

    **[⬆ Back to Top](#table-of-contents)**

16. ### What is a first order function

    A first-order function is a function that doesn’t accept another function as an argument and doesn’t return a function as its return value.

    ```javascript
    const firstOrder = () => console.log("I am a first order function!");
    ```

    **[⬆ Back to Top](#table-of-contents)**

17. ### What is a higher order function

    A higher-order function is a function that accepts another function as an argument or returns a function as a return value or both.
    The syntactic structure of higher order function will be as follows,

    ```javascript
    const firstOrderFunc = () =>
      console.log("Hello, I am a First order function");
    const higherOrder = (ReturnFirstOrderFunc) => ReturnFirstOrderFunc();
    higherOrder(firstOrderFunc);
    ```
    You can also call the function which you are passing to higher order function as callback function.

    The higher order function is helpful to write the modular and reusable code. 

    **[⬆ Back to Top](#table-of-contents)**

18. ### What is a unary function

    A unary function (i.e. monadic) is a function that accepts exactly one argument. It stands for a single argument accepted by a function.

    Let us take an example of unary function,

    ```javascript
    const unaryFunction = (a) => console.log(a + 10); // Add 10 to the given argument and display the value
    ```

    **[⬆ Back to Top](#table-of-contents)**

19. ### What is the currying function

    Currying is the process of taking a function with multiple arguments and turning it into a sequence of functions each with only a single argument. Currying is named after a mathematician **Haskell Curry**. By applying currying, an n-ary function turns into a unary function.

    Let's take an example of n-ary function and how it turns into a currying function,

    ```javascript
    const multiArgFunction = (a, b, c) => a + b + c;
    console.log(multiArgFunction(1, 2, 3)); // 6

    const curryUnaryFunction = (a) => (b) => (c) => a + b + c;
    curryUnaryFunction(1); // returns a function: b => c =>  1 + b + c
    curryUnaryFunction(1)(2); // returns a function: c => 3 + c
    curryUnaryFunction(1)(2)(3); // returns the number 6
    ```

    Curried functions are great to improve **code reusability** and **functional composition**.

	Why Currying?
		helps avoid passing the same variable again and again
		helps to create Higher Order Functions
		fewer errors and side effects

	Currying vs Partial Application 🔥
	In currying, nested functions are equal to arguments, means each function must have a single argument.
	f(a, b, c) -> f(a)(b)(c)

	Partial Application transforms a function into another function with smaller arguments (less args).
	f(a, b, c) -> f(a)(b, c)

	![Screenshot](images/currying-function.png)
    **[⬆ Back to Top](#table-of-contents)**

20. ### What is a pure function

    A **Pure function** is a function where the return value is only determined by its arguments without any side effects. i.e, If you call a function with the same arguments 'n' number of times and 'n' number of places in the application then it will always return the same value.

    Let's take an example to see the difference between pure and impure functions,

    ```javascript
    //Impure
    let numberArray = [];
    const impureAddNumber = (number) => numberArray.push(number);
    //Pure
    const pureAddNumber = (number) => (argNumberArray) =>
      argNumberArray.concat([number]);

    //Display the results
    console.log(impureAddNumber(6)); // returns 1
    console.log(numberArray); // returns [6]
    console.log(pureAddNumber(7)(numberArray)); // returns [6, 7]
    console.log(numberArray); // returns [6]
    ```

    As per the above code snippets, the **Push** function is impure itself by altering the array and returning a push number index independent of the parameter value, whereas **Concat** on the other hand takes the array and concatenates it with the other array producing a whole new array without side effects. Also, the return value is a concatenation of the previous array.

    Remember that Pure functions are important as they simplify unit testing without any side effects and no need for dependency injection. They also avoid tight coupling and make it harder to break your application by not having any side effects. These principles are coming together with the **Immutability** concept of ES6: giving preference to **const** over **let** usage.

    **[⬆ Back to Top](#table-of-contents)**

21. ### What is the Temporal Dead Zone

    The Temporal Dead Zone(TDZ) is a specific period or area of a block where a variable is inaccessible until it has been intialized with a value. This behavior in JavaScript that occurs when declaring a variable with the let and const keywords, but not with var. In ECMAScript 6, accessing a `let` or `const` variable before its declaration (within its scope) causes a ReferenceError. 

    Let's see this behavior with an example,

    ```javascript
    function somemethod() {
      console.log(counter1); // undefined
      console.log(counter2); // ReferenceError
      var counter1 = 1;
      let counter2 = 2;
    }
    ```

    **[⬆ Back to Top](#table-of-contents)**

22. ### What is memoization

    Memoization is a functional programming technique which attempts to increase a function’s performance by caching its previously computed results. Each time a memoized function is called, its parameters are used to index the cache. If the data is present, then it can be returned, without executing the entire function. Otherwise the function is executed and then the result is added to the cache.
    Let's take an example of adding function with memoization,

    ```javascript
    const memoizAddition = () => {
      let cache = {};
      return (value) => {
        if (value in cache) {
          console.log("Fetching from cache");
          return cache[value]; // Here, cache.value cannot be used as property name starts with the number which is not a valid JavaScript  identifier. Hence, can only be accessed using the square bracket notation.
        } else {
          console.log("Calculating result");
          let result = value + 20;
          cache[value] = result;
          return result;
        }
      };
    };
    // returned function from memoizAddition
    const addition = memoizAddition();
    console.log(addition(20)); //output: 40 calculated
    console.log(addition(20)); //output: 40 cached
    ```

    **[⬆ Back to Top](#table-of-contents)**
