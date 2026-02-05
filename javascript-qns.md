# JS INTERVIEW TOPICS
1. What is Javascript?
- It is a programming language that allows us to effectively **interact with the web browser**.
- Initially intended for browsers, as time went used as fully fledged programming language.

2. Is javascript synchronous or asynchronous?
- It is a **single-threaded, non-blocking synchronous language**.
- But only the v8 engine acts this way, it has other **web api's, callbacks, event loops which makes it act asynchronous**.

3. What are the js data types?
- Primitive and non-primitive data types.
- **Primitive types** - string, number, boolean, null, undefined, bigint
- **Non-Primitive data types** - Object, Array, Date, Function

4. Difference between var, let and const?
- **var** -> this is the initial declaration used before es6. It has **global or function scope**.
- **let and const** -> these were introduced as part of es6. It has **block scope**.
- **var can be redeclared**. 
    ```
    var greeter = "hey hi";
        var times = 4;

        if (times > 3) {
            var greeter = "say Hello instead"; 
        }

        console.log(greeter) // "say Hello instead"

    ```
- **let can be updated but not redeclared, const cannot be updated or redeclared**.

5. What is hoisting in javascript?
- Hoisting is a behaviour in javascript where all the **declarations of (functions, variables, class) goes to the top of scope**.
    ```
    printHello()
    // hello

    function printHello() {
    console.log("hello")
    }
    ```
- Here, the function is called before the declaration, but with hoisting, javascript automatically pushes the declaration to the top of the block.
- But, this **only works with function declaration, it does not work with function expressions**.
- The below one is function expression:
    ```
    const helloPrint = function() {
        console.log("hello")
    }
    ```

6. What is a closure?
- Closure in javascript gives a function **access to its outer scope**. They are bundled together one inside another and the inner functions can access the outer variables. 
    ```
    function outer() {
        const a = 10;
        function inner() {
            const b = 20;
            console.log(a+b);
        }
    }
    ```

7. What are temporal dead zones (TDZ)?
- **Variables declared with let,const,class are in TDZ when they are accessed before initialization**. 
    ```
    console.log(c)
    console.log(d)
    var c = 10;
    let d = 20;
    VM430:1 undefined
    VM430:2 Uncaught ReferenceError: d is not defined
        at <anonymous>:2:13
    ```
- Here, the variable c does not throw error, it is undefined as var is not included in TDZ. But the variable d throws referenceError. 

8. What are IIFE?
- The Immediately Invoked function expression - javascript function which **runs immediately as it is defined**. They are enclosed within paranthesis.
    ```
    (function () {
    // statements…
    })();
    ```

9. What is the 'this' keyword?
- It is a special keyword which **refers to the object,class,variable on which the function is being executed**. 
- When a function is called through an object (dot operator), then the this keyword refers to that object. 
    ```
    const person = {
        name: "Alice",
        greet() {
            console.log(`Hello, my name is ${this.name}`);
        }
        };
        person.greet(); // Output: Hello, my name is Alice
    ```
- **Arrow functions don't have this keyword, they have lexical scoping** (access variables from outside scope)

10. Difference between == and ===?
- '==' is the equality operator and '===' is the **strictly equal operator with type check**.

11. What is a callback function?
- It is a **function passed inside another function as an argument**, which is invoked from the outer function to complete an action. 
- Synchronous callbacks - does not wait for any task to be completed (eg: map(), forEach())
- Asynchronous callbacks - setTimeout(), promises()

12. What are callback hells?
- It is a term defined when **multiple callbacks are nested one after another** and it becomes very difficult to read, maintain and debug code for developers. (Pyramid of doom)

13. What are promises?
- Promises are **eventual completion/failure of an asynchronous operation**. They are an improvisation to callbacks.
- These are returning objects to which callbacks are attached instead of passing them as an argument.
- They can be **chained(promise chaining) with one another, which can avoid callback hells**.
- States of promises - **pending, fulfilled, rejected**.
- error handling - then,catch,finally used.

14. What is async/await?
- The async/await keywords enables asynchronous, promise-based behaviour to be written in a clean way and eliminates the need for explicit promise chaining. 
- async -> creates binding of a new async function to a given name, ensures a promise is returned.
- await -> given inside body of function, pauses execution of async function until a promise is resolved/rejected.

15. What is event bubbling, capturing, delegation?
- event bubbling - when an event occurs on an element, it bubbles up from child to the top. This is by default.
    ```
        <div id="parent">
            <button id="child">Click me</button>
        </div>
    ```
- event capturing - same, but the order is reversed (from top to bottom). It is mentioned using useCapture: true as argument. 
- event delegation - This is th technique that can handle events effectively by just having one event listener instead of multiple ones.
- event.stopPropogation() - stops bubbling/capturing of events on parent element.
