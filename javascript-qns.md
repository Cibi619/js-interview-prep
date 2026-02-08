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
- The async/await keywords **enables asynchronous, promise-based behaviour to be written in a clean way** and eliminates the need for explicit promise chaining. 
- async -> **creates binding of a new async function** to a given name, ensures a promise is returned.
- await -> given inside body of function, **pauses execution of async function until a promise is resolved/rejected**.

15. What is event bubbling, capturing, delegation?
- event bubbling - when an event occurs on an element, it **bubbles up from child to the top**. This is by default.
    ```
        <div id="parent">
            <button id="child">Click me</button>
        </div>
    ```
- event capturing - same, but the **order is reversed (from top to bottom)**. It is mentioned using useCapture: true as argument. 
- event delegation - This is th technique that can **handle events effectively by just having one event listener instead of multiple ones**.
- event.stopPropogation() - stops bubbling/capturing of events on parent element.

16. What is DOM?
- Document Object model is the **representation of webpage in a tree-like structure** starting from the html tag to its roots(children).
- It connects web pages to script. The elements can be accessed with few methods such as querySelector, getElementById and so on.

17. Difference between null and undefined?
- Both are primitive data types in javascript.
- **null** is a type used when the **user declares it to have no value**.
- **undefined** is the **default value when a variable has not been initalized yet**.
- null is declared by the developer, undefined is by the system.

18. What is NaN?
- NaN is a **global object refering to Not a Number**. 
- If you try to convert a alphabet/word to a number/int, NaN is returned.

19. What is spread operator in javascript?
- spread operator (...) allows an **iterable(array/string) to be expanded into separate elements**.
- Spread syntax can also be used to create a **shallow copy of an array**.

20. What is rest operator in javascript?
- rest parameter **allows infinite parameters to be passed inside an array** with the ... operator.
- spread expands the given arg into separate elements whereas rest groups any number of parameter with the ... operator.

21. Shallow copy and deep copy in js?
- **Shallow copy** refers to copying method where **both the objects share the same reference**, and changes in one results in change in another. (when copied using spread operator, Object.assign(), Array.from())
- **Deep copy** refers to copying method, with **different references** (source and copy are completely different).
- Json.parse(Json.stringify()), structuredClone() - makes deep copy.

22. What is destructuring?
- Destructuring allows for **unpacking values** from arrays or properties from an object.
    ```
        [a,b] = [10,20]
        // in this case, a = 10, b = 20
    ```
- all variables can be declared as an array
    ```
    const [a,,c] = [10,20,30]
    // a = 10, c = 30, b is skipped
    ```
- also used for swapping logic
    ```
    const a = 10, b = 20
    [a,b] = [b,a]
    // a = 20, b = 10
    ```

23. What are arrays in js?
- Arrays are **ordered collection** of elements inside a single variable name. 
- They **can hold** values of diff types.
- Their properties can be accessed with help of [] or . operator.

24. Difference between map, filter and reduce?
- map() method creates a **new array populated with results of calling a provided function on every element** of the array. 
    ```
        let arr = [1,2,3,4,5]
        let doublearr = arr.map(el => el * 2)
        // doublearr = [2,4,6,8,10]
    ```
- filter() method creates a **copy of portion of array** based on the provided condition.
    ```
        let arr = [1,2,3,4,5]
        let filteredarr = arr.filter(el => el > 3)
        filteredarr = [4,5]
    ```
- reduce() method takes in a **reducer callback function as argument**, executes it in each element of array in order, passes the return value from calculation on previous arg. The **final result is a single value**. 
    ```
        let arr = [1,2,3,4,5]
        let sum = arr.reduce((acc,val) => acc + val, 0)
        // sum = 15
    ```

25. What is a prototype?
- They are mechanisms by which javascript objects **inherit features from one another**. 
- When accessing a property in an object, javascript searches for in: the object itself, object's prototype, prototype's prototype and so on. This is called **prototype chaining**.

26. What is a memory leak?
- Memory leak occurs when the **application unintentionally holds reference to the objects that are no longer needed**. It prevents the garbage collector from cleaning it.
- Eg: when setInterval() and setTimeout() are not cleared with clearInterval() and clearTimeout(). EventListener() is not removed with removeEventListener().

27. What is setTimeout() and setInterval()?
- Both of these are **web apis used to schedule the execution of the function**.
- setTimeout() executes the function once after the specified delay and setInterval() executes it.

28. What is JSON?
- JSON is a standard text-based format that is used to **represent structured data**. It has a similar syntax to javascript objects. Popularly used for sneding data from server to client.
- It **can be nested, it can have arrays**. It is independent from javascript.

29. Difference between call, apply, and bind?
- These are methods in js used for **controlling the this context**. 
- **call()** methods are useful in cases where an **obj borrows a method from another method**.
- It calls a function with a given this value and **args are provided individually**. 
    ```
        const obj1 = {
            firstName: 'Cibi',
            lastName: 'Sharan',
            introduce: function() {
                console.log(`Hi, I'm ${this.firstName}`);
            }
        }
        const obj2 = {
            firstName: 'Shaa'
        }
        obj1.introduce.call(obj2); // output -> Hi, I'm Shaa
    ```
- **apply()** - differs where the **args are provided here as an array**.
    ```
        const person = {
        firstName: 'John',
        lastName: 'Doe'
        };

        function greet(greeting, punctuation) {
        console.log(`${greeting}, I'm ${this.firstName} ${this.lastName}${punctuation}`);
        }

        greet.apply(person, ['Hello', '!']);
        // Output: "Hello, I'm John Doe!"
    ```
- Use case - to find max val in an array. 
    ```
        const numbers = [5, 6, 2, 3, 7];
        const max = Math.max.apply(null, numbers);
        console.log(max);  // 7
    ```
- **bind()** - **Creates a new function, result stored in a variable** with given this arg as parameter and optional args.
- Not immediately executed.
    ```
        const person = {
        firstName: 'John',
        lastName: 'Doe'
        };

        function greet(greeting, punctuation) {
        console.log(`${greeting}, I'm ${this.firstName} ${this.lastName}${punctuation}`);
        }

        const boundGreet = greet.bind(person, 'Hello');
        boundGreet('!');  // "Hello, I'm John Doe!"
        boundGreet('?');  // "Hello, I'm John Doe?"
    ```

30. What is currying in js?
- It is a programming technique where we **transform a function that takes in multiple args into multiple functions with single args**.
- It is **useful for having a reusable function**.
    ```
        function multiply(a,b) {
            return a * b;
        }
        // this is changed to
        function multiply(a) {
            return function(b) {
                return a*b;
            }
        }
        const squares = multiply(2)
        const cubes = multiply(3)
        squares(5);
    ```
- Here, first multiply is called with 2 as arg, the return val is a function that is stored in squares. (this is the inner function and it knows the a value as 2). Now, when squares is called, it already has 2, now it takes b value (5 here), and returns a * b = 10. So output here is 10.

31. What is debouncing?
- Debouncing **delays the execution of a function until the user stops performing an action for a specified period of time**. 
- It is useful in cases when the **search has to be executed after the user finishes typing**, not after each keystroke.
    ```
        <input type="text" onkeyup="processChanges()" />
        // js
        const processChanges = debounce(() => console.log('changes saved..'));
        function debounce(timeout = 1000) {
            let timer;
            return (...args) => {
                clearTimeout(timer);
                timer = setTimeout(() => { func.apply(this, args); }, timeout);
            };
        }
    ```

32. What is throttling?
- It is a **technique to limit function execution to be done at specific intervals, regardless how many times that event has been triggered**.
- **Useful for performance optimization with high-frequency events** such as scroll, mouse movements.
    ```
        function throttle(func, limit = 1000) {
            let inThrottle;
            return function(...args) {
                if (!inThrottle) {
                    func.apply(this, args);
                    inThrottle = true;
                    setTimeout(() => {
                        inThrottle = false;
                    }, limit);
                }
            };
        }

        // Usage
        const logScroll = throttle(() => {
            console.log('Scrolling...');
        }, 1000);

        // Scroll continuously
        logScroll(); // Executes immediately
        logScroll(); // Ignored (within 1s)
        logScroll(); // Ignored (within 1s)
        // After 1 second
        logScroll(); // Executes again
        logScroll(); // Ignored (within 1s)
    ```

33. What is strict mode?
- It is a way to have **restricted variant of js** to indicate us of potential errors.
- It makes it easier for debugging as it prevents type unsafe actions.
- Used normally with `use strict` keyword.

34. What is lexical scope?
- It is a **scoping mechanism in js** where the access to variables in function is determined by where the function is written, not where it's caled.
- The **inner functions can access variables from outer scope** but the outer functions cannot do it.

35. What is an object in javascript?
- An object is a **data type in js which is defined by key value pairs**. The values of object can be accessed with dot operator or square brackets.
- Used to represent real-world entities.    
    ```
        const person = {
            firstName: "Cibi",
            lastName: "Shaa",
            age: 10
        }
    ```

36. What is localStorage?
- Localstorage is a **web storage api that allows users to store data persistently in user's browser as key-value pairs**.
- They can be retrieved by their properties such as getItem(), setItem() and getValue().
- The **data is only available on the client side** and does not expire.

37. What is sessionStorage?
- It is also a web storage api similar to localStorage, but the difference is the **data persists only till the session is there**.
- When the browser/tab is closed, it expires.

38. What are JavaScript modules?
- JS modules are a **way to structure and organize code and split larger files into resuable smaller ones**.
- They **can be exported for use** in other modules as well as **they can import modules** for its use.
- CommonJS is one of the modules, ES6+ is used modern js module now.
    ```
        // math.js
        export function add(a, b) {
            return a + b;
        }

        // app.js
        import { add } from './math.js';
        console.log(add(2, 3));  // 5
    ```

39. What is garbage collection?
- Javascript automatically allocates memory and frees it up when it's not used anymore. It allocates memory during initializing values.
- It uses mark and sweep algorithm, from the root, all references are seen, and those without it are Garbage collected(GC).
- Weakmap and WeakSet is used for allowing GC. They differ from Map and Set as they store only object types.

40. What is optional chaining?
- Optional chaining is done with (?) symbol which safely allows access to nested objects without explicitly checking if each reference in chain is null or undefined.
- If not used, the object containing null is accessed, reference error is thrown.