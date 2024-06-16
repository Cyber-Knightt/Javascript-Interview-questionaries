# Javascript-Interview-questionaries

# Table of Contents

<!-- TOC_START -->
| No. | Questions |
| --- | --------- |
| 1 | [What are the possible ways to create objects in JavaScript](#what-are-the-possible-ways-to-create-objects-in-javascript) |
| 2 | [What is a prototype chain](#what-is-a-prototype-chain) |
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