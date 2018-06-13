# GOOGLE DEVELOPER NANODEGREE

---

### Responsiveness
__Head__: general info and metadata
__Body__: visible content
__Device emulation__: `ctrl+shift+j` (toggle device toolbar). You can also debug remotely, using a real device.

_Pixels_: Device Independent Pixels map to hardware pixels via device pixel ratio - only in one dimension (up or down). Developers need CSS pixels. Differences between devices despite equal resolutions are likely caused by:
- Viewport settings (without defining viewport, you leave it up to browser to decide)
- Device pixel ratio

If screen has width of 1920px and DPR of 2, maximum width viewport is 960px in CSS pixels/DIPs. 
_Viewport width = (physical pixels / device pixel ratio)_

##### Setting viewport
Meta viewport tag in head
    width = device width in DIPs
    initial scale = 1 (1:1 relationship DIP:CSS)

##### Setting element width
Use relative instead of absolute positions, so that elements don't overflow container, but take up full viewport (e.g. 100%). Add to main.css:

    img, embed, object, video {
        max-width: 100%;
    }

##### Setting tap targets
One finger is 40 CSS px, so tap targets should be 48 x 8px with 40px spacing around.

##### Different styles, different sizes
__Media queries__: responsive styles with break points (minor break points: font size or image size; major break points: restructuring of content).

    <link rel="stylesheet" media="screen and (min-width: 300px)" href="patterns.css">
    // Here, break point is 300px
    // Where pattern is a new stylesheet
    // Link to a new stylesheet for every break point

or

    @media screen and (min-width: 300px) {
        body {background-color: green;
    }
    // Which is styled in the <head>

or

    @import url("no.css") only screen and (min-width=300px);
    // Avoid this option

There are some predefined layouts (grids): check __flexbox__ on container element. Don't forget you can change the order of the content.

    display: flex; // default is row
    flex-wrap: wrap; // wrap to next line

Frequently used patterns:
- Mostly fluid
- Layout shifter
- Column drop
- Off canvas

Example:

    @media screen and (min-width=450px) {
        .light_blue_box, .green_box {
            width:50%;
            order:x;
        }
        .orange, .yellow, .purple {
            width:50%;
            order:x;
        }
    }
    
or

    .container {
        width:700px;
        margin-left:auto;
        margin-right:auto;
    }

##### Hamburger navigation
See lessons:
1. Set position to minimum
2. Click event adds/removes class
3. Class in CSS sets position to positive
4. Alternatively, use `display:none` *

##### Responsive tables
1. Hidden columns


    @media screen and (max-width:499px) { display:none }

2. No more tables (transpose)
    Position redundant elements way off grid (`-9999`)
3. Contained scrolling
    In CSS of table, add `overflow-x:auto`

##### Fonts
Measure +- 65 characters per line (see Ellipsis... for smaller viewports) with size 16px and line height 1.2em.

##### Images
Use relative sizes to avoid overflowing; 
use picture element for art direction (different sources with media matches);
inside picture element, use srcset attribute for high DPI devices; 
use sizes attribute and media queries to specify size.
_Use media queries to change what image is used at what viewport width. Note that sometimes it's better to just not show images when viewport is small._

---

[*] Block versus inline
__Block level content__ takes up all horizontal space it gets, no matter how much the content needs.
__Inline level content__ takes only the space its content needs to fit in (content determines properties). Inline normally does not accept width, height, top/botton margin properties.

---

WIDTH = MARGIN LEFT + BORDER LEFT + PADDING LEFT + CONTENT WIDTH + PADDING RIGHT + BORDER RIGHT + MARGIN RIGHT
_Padding: space between content and border_
_Margin: space between different elements_

---

# Javascript ES6 updates

1. Let and const
    __Let__ can be reassigned but cannot be re-declared in the same scope
    __Const__ must be assigned an initial value, cannot be re-declared in the same scope and cannot be reassigned
    Let and const eliminate the issue of hoisting. They are scoped to the block, not to the function (temporal dead zone). Variables can only be accessed after declaration.
2. Template literals


    `${expression} text ${expression}` // instead of
    'string text' + varOne + 'string text'

3. Destructuring
    

    point = ['hi', 'hello', 'bye', 'hey']
    const [one, , two, three] = point // Gives us hi, bye and hey

4. Shorthands: object literal
5. Iteration (for...of loop)
    * For loop
    * For...in loop (discouraged when looping over array)
    * For...of loop (for any iterable data type)


    const digits = [0,1,2,3,4,5,6,7,8,9]
    for (const digit of digits) {
        console.log(digit);
    } // Will only loop over the values

6. Spread operator
    Expand or spread iterable objects into multiple elements
    ... (structure) > unbox
7. Rest parameter
    Represent indefinite number of elements into array
    ... (destructure) > box

# Shell workshop

Command line for computer.
Use __forward slashes__ and __single quotes__. Single quotes around command disable special characters.

Command | Description
--- | ---
echo | print
$word | word is variable
ls | list (just ls or e.g. ls Downloads)
cd | change directory
.. | parent directory
; | combine two commands
pwd | print working directory
. | current directory
~ | home directory
-option | option for argument (e.g. ls -l)
[*] | all (pattern)
mkdir | make dir
mv | move ('from' to)
curl | see url (show source code, compressed JS)
curl -l | follow redirects (download pages/files by url)
curl -o | filenametosaveunder.html -L 'waht to operate on (URL)'
cat | output content (read)
less | shows one screen full (b = go back; / = search)
q | quit
rm | remove (trash can = -i interactive)
rmdir | remove dir
grep | search text file (e.g. grep hello text.txt \| less; \| is pipe)
mkdir | make dir
pwd | print wd
wc | word count (-l lines)
grep -c | word count (same as wc)

GUI = click and drag and nicely visualized
SHELL = underlying code

[...]

# The document object model
A [full parse representation](https://www.w3schools.com/js/pic_htmltree.gif) of HTML markup (content and properties of HTML and all relationships between nodes).

Conversion:
HTML tags > tokens > nodes > DOM
_where tokens are DOCTYPE, start tag, end tag, comment, character, end-of-file_
__#x = id
.x = class
x = tag (e.g. p)__

    const varId = document.getElementById('idname);
    const varClass = document.getElementsByClassName('classname'); // Returns multiple elements as HTML collection (not array)
    const varTag = document.getElementsByTagName('tagname'); // "
    const varAlternative = document.querySelector('#', '.', 'x'); // Only returns first result, alternative querySelectorAll
    const varAlternativeExample = document.querySelector('p .ok'); // First p tag with class ok
    
### Blueprints/interfaces
`Node` = blueprint with properties and methods (`.property`, `.method()`)
`node` = actual objects built from blueprint
`Element` = type of node, blueprint for creating elements
_There's many more like this!_ 

### Creating content with Javascript
##### Modifying existing content
`element.innerHTML` returns HTML content _inside_ this element
`element.textContent` returns _just the text_ content inside this element (no CSS)
`element.innerText` returns text plus CSS

##### Add new content
    const container = document.createElement('span');
    container.textContent = 'Hello!'
    const placeToPut = document.querySelector('h1');
    placeToPut.appendChild(container);

`appendChild` adds at end. Alternatively:

    .insertAdjacentHTML('locationHTML', textToInsert);
where locationHTML can be either beforebegin [1], beforeend [2], afterbegin [3], afterend [4]:

    [1]<p>[2]
        Text/HTML
    [3]</p>[4]

##### Remove content
    parentElement.removeChild(childToRemove); 

Walkaround:

    childToRemove.parentElement.removeChild(childToRemove);

Easier way:

    childToRemove.remove(); // childToRemove or whatever to remove

##### Style content
1. `varName.style.color = 'red';`
    `.style` accepts one CSS style a time.
2. `varName.style.cssText = 'color:blue; font-size:3.5em; ...;`
    Write as in style sheet. These will overwrite what's already in style attribute tag.
3. `varName.setAttribute('style', 'color:blue; font-size:3.5em, ...');`
    This is not just for styling, but for setting any attribute.

##### Accessing classes
`.className` returns string of classes that selector has (split through `.split('')` and push/pop/for...loop in array)
`.className = "name-class"` sets class and erases all former classes in selector

Alternatively,
    `.classList` returns DOMtoken list
    To which you chain `.add()`, `.remove()`, `.toggle()` or `contains()`
    
### Browser events
`(un)monitorEvents(document)`
Right before `</body>`: `<script src="app.js"></script>`

Interfaces: EventTarget < Node < Element
_EventTarget_: element, document and window are most common. No properties but three methods: 
1. `.addEventListener()`


    <event-target>.addEventListener('<event-to-listen-for>, <function-to-run>)
Event to listen for: TYPE (click, scroll, resize, submit)
Function to run: LISTENER/HANDLER
2. `.removeEventListener()`
    Requires passing exact same listener function as .addElementListener. Has to __refer__ (!) to exact same function.
3. `.dispatchEvent()`

##### Event phases: how to control events
Capture (go down HTML to find target/element) > At target (running of handlers) > Bubbling (works way back up the HTML, executing bottom up)
By default, functions only run in bubbling phase, unless you add a thrid parameter to the .addEventListener event: true. Then it will run in capturing phase. E.g.

    document.addElementListener('click', function() {
        // code;
    }, true); 

To store the event data passed to it:

    document.addElementListener('click', function(e) {
        e.preventDefault(); // to prevent default form happening, if you first want to do something else (inside element, event.target is element that was clicked)
        // code;
    }, true);

Refactoring the number of event listeners, by applying function and type to parent of all elements in an element. To still have access to individual elements, use _event delegation_. E.g.

    const Div = document.createElement('div'); // Create Div element
    function respondToClick(e) { // Function for what to do when one <p> is clicked
        console.log('Paragraph was clicked: ' + e.target.textContent);
        for (let i=1, i <= 200, i++) { // 200x loop
            const newEl = document.createElement('p'); // Create new element <p>
            newEl.textContent = 'Paragraph no.' + i; // Add content
            Div.appendChild(newEl); // Add to Div
        }
    } 
        
        document.body.appendChild(Div); // Add Div to body
        Div.addEventListener('click', respondToClick); // Only now is it linked to function for clicking

P.S. Checking for NodeType: `event.target.nodeName === 'SPAN'` (or whatever)

### Performance
`performance.now()`:

    const start = performance.now();
    // code to measure performance of
    const end = performance.now();
    // time = end - start
    
JavaScript concurrency model:
Run-to-completion JavaScript
Run pending event handlers (event loop: call stack, web API/browser, event queue)

##### Running code later

    setTimeOut(function toRunLater() {
        // code
    }, 1000);

[...]

# Object-oriented programming in JavaScript

### What is an object and how do I create it?
- __Array__ `[ ]`: ordered collection of elements, referenced by indexes
- __Object__ `{ }`: unordered collection of key/value pairs, referenced explicitly
    - Accessing an object's properties is _not entirely the same as in Python,_ as keys in Javascript don't need to be hashable (strings, numbers, floats). You access them either by
        - dot notation: `object.key`, or
        - bracket notation: `object['key']`
    - Both can be extended for nested objects.

##### Creating objects
    const myobject = { }; // or
    const myObject = new Object();

##### Adding or changing properties
Simply specify property name and give it a value. _We can also add methods (i.e. functions) to objects!_

##### Removing properties
    delete object['key']; // or
    delete object.key;

Primitives (string, number, boolean, float) are immutable, meaning they only change inside a function. Objects are reference-based and thus are mutable, meaning values change both inside and outside a function. Changes in a copy will thus also change the original. Thus, when comparing (===) objects, what matters is the reference.

##### Calling methods
    object['method'](); // or
    object.method();

##### Returning keys and values in an array
    Object.keys(objectName); // and
    Object.values(objectName);
    
If desired, an argument can be passed inside the brackets. 

### The 'this' keyword
We use `this` to refer to the object at hand.
How a function is invoked determines the value of `this` inside the function.
- When invoked from a constructor function, the value of `this` is the newly created object (see _'Constructor functions'_).
- When invoked as a method, the value of `this`is whatever is left of the dot at invocation (i.e. the object).
- When invoked as a regular function, the value of `this` is the global `window` object.
    - Every `var` (__not__ `let` and `const`!) declaration made at the global level, i.e. outside of a function, becomes a property on the `window` object.
    - Likewise, every global function declaration becomes a method on the `window` object.
        - Global variables and functions are not ideal (tight coupling, name collisions), so only write them as a last resort!

### Functions at runtime

JavaScript functions are _first-class objects_, and can be ...
- stored in a variable,
- passed in as an argument in another function (we call the passed-in argument the _callback function_),[*] and
- returned from another function (the so-called _higher-order function_)
    - It can be called using double parentheses.
___
[*] Example array methods:
1. `forEach()` takes in a callback function and invokes that functoin for each element in the array,


    array.forEach(callbackFunc);


2. `map()` does the same, but returns a new array based on what's returned from the callback function, and


    array.map(function(arrayitem) {
        return arrayitem.length;
    });


3. `filter()` does the same as `map()`, but is used as a test: only the items that pass are included in the new array.


    array.filter(function(arrayitem) {
        return arrayitem.length < 6;
    });
___
    
__Note:__ Functions can be invoked by (), objects cannot.

Besides global scope and function scope, there is _runtime scope_. This is the context of the function, i.e. the set of variables available for the function to use.
A function has acces to: _function's arguments, local variables, variables from parent function scope, and global variables._

    const a = 'a'; // global variable
    function parent() {
        const b = 'b'; // variable from parent scope
        function child() {
            const c = 'c'; // local variable within function
        }
    };

CHILD > PARENT > GLOBAL _SCOPE CHAIN_: start sequence thoughts from innermost function and work outwards from there, building what innermost needs all the way to global window.

Functions will retain the scope chain plus access even if they're invoked somewhere else than where it was declared.

__Note:___ if two variables have the same name, the one that is found 'first' by the JavaScript engine prevails (_variable shadowing_).

### Closure
The process of a function retaining access to its scope. Every function has closure.

### Immediately-Invoked Function Expressions (IIFEs)
Functions that are called immeciately after they're defined.

Type | Code
--- | ---
Declaration | `function logger() {console.log('Hello!')};`
Expression | `(function logger() {console.log('Hello!')});`
IIFE | `(function logger(x) {console.log('Hello!')})();`

IIFEs can also wrap around nested functions. They create a private scope that protects variables and methods from being used, because the function is called immediately and thus variables are called immediately. This prevents from unwanted mutations or side-effects because of external access. The returned functions are still publicly accessible, but the variables defined within them are not.

### Classes
Classes are categories of objects.
- __Object__: properties and methods
- __Class__: blueprint for an object

##### Constructor functions
Start with a capital letter; Must be called with `new`; Has object created automatically


    new SoftwareDev() {
        this.favLang = 'JS'; // this refers to SoftwareDev
    }; // no return statement!


From here, you can create a new object (_an instance_) - as many as you like.


    let developer = new SoftwareDeveloper();


__Constructor functions accept arguments!__ We could update the previous as follows:


    function SoftwareDeveloper (name) {
        this.favLang = 'JS';
        this.name = name;
        this.introduce = function() {
            console.log(`I'm ${this.name}!`);
        }
    };


To instantiate a new object from here:


    let myself = new SoftwareDeveloper('Nynke');


If we would then invoke `myself.name`, it would yield Nynke.

__So:__
Define:


    new FuncName();


Add properties:


    function FuncName(arg1, arg2) {
        this.arg1 = arg1;
        this.arg2 = arg2;
        this.prop3 = x;
        this.prop4 = function() {
            console.log(`Hello ${arg2}!`);
        };
    };


Assign to variable to instantiate new object __or__ start with 2. and then add:


    const objName = new FuncName(arg1, arg2);


To check if objName was created with FuncName: `objName instanceof FuncName`.

### Setting the value of `this` ourselves
1. `call()`
2. `apply()`
3. `bind()`

### Prototypal inheritance
We can add methods to the constructor function's __prototype__ property. The prototype property is an object. All objects created by that construcor are linked to this prototype object.


    Object.prototype.method = function() {
        if (this.canTalk) {
            console.log('Hi, I am ' + this.name);
        }
    };

##### Prototype chain
* Objects own properties and methods ˅
* Constructor prototype ˅
* Object() object (top level parent) ˅
* Still not found? `Undefined`

##### Check where property comes from
1. `hasOwnProperty();`
2. `isPrototypeOf();`
3. `Object.getPrototypeOf();`

Every time an object is created, a special property is assigned to it under the hood: constructor. It returns a reference to the constructor function that created that object (`object.constructor`).

##### Subclasses
To set up the prototype of an object ourselves, we use `Object.create()`. This is a clean method to establish prototypal inheritance.

# Updates to functions in ES6

1. Arrow functions

Always _expressions_. E.g.


    const upperized = ['nynx', 'noam'].map(
        name => name.toUpperCase()
    );
Can only be used when stored in variable, when passed as an argument to a function, and when stored in object's property.

__Concise body syntax__: automatically returns expression
__Block body syntax__ (if there's more than one line of code in arrow function's body): { } to wrap function body, has return statement

`this` works differently with arrow functions: it is based on the function's surrounding context (i.e. is same outside and outside function).

2. Default function parameters

Object defaults have benefits over array defaults. Combine with destructuring.

3. New keywords for classes

Everything in one! E.g.

    class Plane { // Class is just a function
        constructor(numEngines) { // Takes care of creating object
            this.numEngines = numEngines;
            this.enginesActive = false;
        }
        startEngines() { // Methods all objects inherit (placed on Plane.prototype)
            console.log('Starting...');
            this.enginesActive = true;
        }
    }

When creating a new instance, `new` must still be used!

Set as subclass: `extends`

Go from subclass to parent class: `super`

In subclasses, before `this` can be used, a call to the super class must be made.

# New built ins in ES6

### Symbols

Unique/immutable data type used to identify object properties. E.g.

    const bowl = {
        [Symbol('apple')]: {color: 'red', weight: 10},
        [Symbol('kiwi')]: {color: 'green', weight: 3},
        [Symbol('kiwi')]: {color: 'green', weight: 4},
    }

### Iterable protocol and iterator protocol

    An object becomes an iterator when it implements the `.next()` method. It returns an object with two peroperties: `value` and `done` (boolean). Iterator method: `[Symbol.iterator]`. E.g.
    
    
    const digits = [1,2,3,4,5,6,7,8,9]
    const arrayIterator = digits[Symbol.iterator]();
    
### Sets and WeakSets

_Sets_: Built in iterable, collection of unique values. It is an array, but:
* Not index-bases
* Items cannot be assessed individually


    const games = new Set(['A', 'B', 'C')];

Code | Description
--- | ---
`.add()` | Add
`.delete()` | Delete
`.clear()` | Delete all
`.size` | Return length
`.has()` | Check item existence
`.values()` | Retrieve all values

The last one returns an iterator object (`SetIterator`). You can store it in a value and use `.next()` or use a for...of loop to loop through the items.

_WeakSet_: Same as Set, but a) can only contain objects, b) not iterable, c) does not have `.clear()` method.

### Maps and WeakMaps

_Maps_: Collection of key-value pairs. They are objects, but...

    const employees = new Map();
        
 Code | Description
--- | ---
`.set(key, {valuex: 'x', 'valuey: 4})` | Add new (value can be { }, but can also be one thing)
`.delete()` | Delete
`.clear()` | Delete all
`.has()` | Check item existence (pass in key)
`.get()` | Retrieve all values (pass in key)

Looping:
1. `MapIterator` (`.keys()` or `values()`) and `.next()`
2. for...of loop: `for (const [k,v] of x) { };`
3. forEach: `x.forEach((v,k) => console.log(k,v));`

### Promises

Let you start work that's done asynchronously and let you go back to your regular work.E.g.

    new Promise (funcToRunAsynchonously (resolve, reject) {
        window.setTimeOut(function whatEver {
            // code
            if (something) {
                reject('Sorry!'); // Indicates failed completion
            }
            resolve(somethingElse); // Indicates succesful completion
        }, 2000);
    }

Assign all of the above to a variable (object). Object has `.then()` method to notify us.

    object.then(function(whatever) { // Resolve
        console.log('Yes!');
    }, function(message) { // Reject
        console.log(message)
        self.goCry();
    });

### Proxies

Something that represents something else.
    
    new Proxy (objectToBeProxyFor, handler)

Where the handler is the list of methods it will handle for the proxied object. `get` and `set` are examples. 

The `get` trap is used to 'intercept' calls to properties.

    const handler = { // Will take over whenever any property of the proxy is accessed
        get (target, propName) {
        // code
        }
    }

The `set` trap is used to 'intercept' code that will change a property.

    const handler = {
        set (target, propName, value) {
            if (propName === 'PayRate') {
                value = value * 0.85;
            }
            target[propName] = value;
        }
    };

See lesson __11.21__.

### Generators

Pausable functions: `function*` where asterisk can be anywhere between function keyword and function name.

Returns an iterator, which can be used to execute actual generator's inner code.

    const genIterator = genFuncName();
    genIterator.next();
    
To get pausing functionality, add `yield;` at end of the function's for loops. This gets the data out of the generator function. `yield var;` yields variable back out to function and then pauses execution. Then,

    const genIterator = genFuncName();
    let result = genIterator.next();
    result.value // First result in for loop
    genIterator.next().value // Next "

`next()` will be called 'one more times' than there are yield expressions in the generator function, to fully complete the generator function. E.g.

    function* getEmployee() {
        const names = ['Annie', 'Bob', 'James'];
        const facts = [];
        
        for (const name of names) {
            // yield *out* each name plus store in 'facts'
            facts.push(yield name);
        }
        
        return facts;
    } // Remember, first call to next() passes in some data that doesn't get stored anywhere
    
    const genIterator = getEmployee();
    
    // Get first name out of generator
    let name = genIterator.next().value;
    // Pass data in and get next name
    name = genIterator.next(`${name} is cool!').value;
    name = genIterator.next(`${name} is awesome!').value;
    // Pass last data in, generator ends and returns array
    const positions = genIterator.next(`${name} is epic!').value;
    // Displays each name and descriptions
    positions.join('\n');

# Professional developer-fu

### Polyfills

JavaScript files that patch holes by replicating some native functions that they're missing. Always start by checking whether function already exists: `if (!Object.prototype.function) { }`. If it does, we don't want to override native with polyfill.

##### Transpiling

Source language => target language (same level of abstraction)

_E.g. ES6 => ES5_. See lesson 12.11/.12/.13 for how to transpile using Babel.

##### Compiling

Source language => target language (lower level language)

[...]

# Front-end applications

### Closures and event listeners

In order to not only alert '3': 

    var nums = [1,2,3];
    for (var i=0, i < nums.length, i++) {
        // code
        element.addEventListener('click', function(numCopy) {
            return function() {
                alert(numCopy)
            };
        })(num));
    };

##### Code organisation

Any data that updates DOM based on data using JavaScript:

* __Model__: where data is stored
* __Octopus__: connects model and view
* __View__: what user sees and interacts with

Separate by putting all three in a separate variable.

    $function() {
        var model = { }
        var octopus = { }
        var view = {
            init: function() { // Example method
                // code to set things up;
            }
            render: function() { // Example method
                // code to update view;
            }
        }

The view never changes the model directly, only octopus does. All smart functionality goes here. Do __not__ store all of your data in the DOM. To separate functionality, we can split view into different views. 

# Promises

Constructors that can be saved as variables or worked on upon creation. Promises are asynchronous, meaning they are not guaranteed to execute in single, unbroken timeline (time it takes is unknown).

The default to deal with asynchronous code is a callback, an alternative to this is a promise. It has four components, _wrapping, thening, catching and chaining_, and four possible states, _fulfilled, rejected, pending and settled_. Settled means the promise is either fulfilled or rejected. This can only happen once, which is in contrast to for example events, which can fire many times.

1. Wrapping


    new Promise(function(resolve[, reject]) {
        var value = doSth();
        if (thingworked) {
            resolve(value) // Value will be received as argument for .then()
        } else if (somethingWentWrong) {
            reject(); // Value will be received as argument for .catch() - no argument, like here, means it simply receives undefined - you could also say reject(Error('Whatever string or object'));
        }
    }).then(function(value) {
        // Success!
        return nextThing(value);
    }).catch(rejectFunction);

If there is an error in the body of the promise, .catch() will also automatically get called.

2. Thening

You chain multiple .then()'s (chain promises). One promise returns a promise, which is the input for the next .then(). Don't forget to return something in the previous .then(). This is the input for the next .then(). Alternatively, use the fulfilled value. 

So, input for the next then is __either the fulfilled value of the previous promise or the returned value of the previous .then()'s function.__

    functionWrappingPromise().then(toDoWhenResolved);

3. Catching

To make sure no error goes unhandled.

    functionWrappingPromise().catch(toDoWhenError);

4. Chaining

Asynchronous actions that depend on each other.

    get('example.json') // XHR: to fetch resources, use the Fetch API (check branch fetch-solution!)
    .then(resolveFunc)
    .catch(rejectFunc)
    
    // is same as
    
    get('example.json')
    .then(resolveFunc)
    .then(undefined, rejectFunc) // .catch is shorthand for .then() with two callbacks

As soon as a promise rejects, JavaScript skips to next reject functoin in the chain (whether in .catch() or in .then()).

##### Multiple asynchronous actions

1. In series (after one another) => synchronous and asynchronous
2. In parallel (simultaneously) => asynchronous

To keep order in a sequence of promises (that can finish in varying times): for every iteration, add another `.then()`. _See promises-solution-complete._

---

`.map`: array method, accepts function and returns array.

    array.map(function(val) { 
        // code to execute against each val
    });
    
`.all`: takes array of promises, executes them, returns array of values. Rejects if just one promise rejects!

    Promise.all(arrayOfPromises)
    .then(function(arrayOfValues) { // Which is same order as array of promises
        // code
    };

# AJAX (Asynchronous JavaScript and XML)

Not just XML, also JSON, HTML, text, images, etc.

Used to add data to project asynchronously.

To interact with various data sources, we use an Application Programming Interface (API).

The XMLHttpRequest (XHR/xhr) object is used to make requests.

    const asyncReqObj = new XMLHttpRequest(); // Create object from constructor
    asyncReqObj.open('GET', 'url.com'); // Initiate request
    asyncReqObj.onload = function() { // When response is succesfull (write function separately) - in this function, 'this' is the XHR object*
        const data = JSON.parse(this.responseText); // If returned data is JSON this will convert to JavaScript object
    }
    asyncReqObj.onerror = function() { } // When error occurs
    asyncReqObj.setRequestHeader('Authorization', 'Client-ID <id>'); // If you need to send HTTP header along
    asyncReqObj.send(); // Send request

Add debugger to success function before doing anything, to see where all of the data you need are stored, so you know what properties you need to address in the function. 

__See code in 4.5.12.__ `.responseText` holds text of response.

[*] Grab `data.results` you need, create HTML content (string) with object literals referring to properties of data, add this variable to HTML. Add if/else statement for when there is no data returned. __See lesson 4.5.11.__

##### Alternatives to XHR

1. jQuery (don't forget to link in `<script>`)


    $.ajax(URL, config obj) // You can pass in object literals in URL (use ``) - GET is default
    
    // or
    
    $.ajax(config obj)
    
To handle response:

    $.ajax({
        url: 'https://...co/api',
        headers: {Authorization: 'Client-ID ...' // If needed
    }).done(handleResponse)

Define `handleResponse` as separate function - `done()` is same as `onload` - automatically converts JSON to JavaScript. E.g.

    function addImage(imgs) {
        const first = imgs.results[0];
        responseContainer.insertAdjacentHtml('afterbegin', `<fig...</figure>`);
    }

For handling errors, __see lesson 4.7.7.__

---
_In DevTools: JavaScript call stack_

Shows call stack order, e.g. `.ajax()`, `.send()`, `options.xhr()`, `jQuery.ajaxSettings.xhr`.

2. AJAX with fetch


`fetch('url')` returns a promise.

To add headers:


    fetch(url, {headers: {Authorization: 'Client-ID ...}}); // Add as property
    
    //or
    
    const requestHeaders = new Headers();
    requestHeaders.append('Authorization', 'Client-ID ...');
    fetch(url, {headers: requestHeaders});

Default method is `GET`. Change by adding method property (e.g. `method: 'POST'`). 

__Handle response:__

Add a `.then()` to fetch request. E.g.


    fetch('url', {headers: {Authorization: 'Client-ID ...}})
    .then(function(response) {
        // code, e.g. return response.json
    });

Handle errors through chaining `.catch()`. 

Returned is a response object. In order to get the body of this object, call data type on it (such as `.json` above - alternatives are `.blob`, `.text`, `.formData`...). Then add other `.then()` to get and use returned data. E.g.


    .then(addImage(data) { }) // Display is same as XHR

# Front end applications

### Features of single page apps

Single page apps being self-contained pages with own UI and logic, without page reloads.

__Client-side (_front-end_, updates frequently/without page refresh) versus server-side (_back-end_).__

Frameworks provide:
1. Templates (V)
2. URL management (V)
3. Event handling (C)

What about M? Data is sent off to a server to be saved.

### Backbone

Templates in Backbone are built with special delimiters, that can be found in `underscore.js`, e.g. `<%=` or `<%-`. By default, all delimiters are `%>`. Backbone finds `<%` and `%>` and captures all in between.

___
_Did you know?_


    var adderOne = function(num1, num2) {
        return num1+num2;
    };
    
    // is the same as
    
    var adderTwo = new function("num1", "num2", "return num1+num2");

---

When creating Backbone templates, access your data as properties on an object (`index.html`) and pass that object name in with template's settings (`app.js`). E.g.


    template: _.template($('#menuItem-template-'.html(), {variable: 'menuItem'}), ...
    
Build your own templating function:

    var template = function(text,options) {
        var delimiter = { // Delimiter is key
            open: '*(', // Value one
            close: ')*' // Value two
        };
        var templateString = []; // Different segments that will later be joined together to form the body of the constructor function
        var i=1;
        var closingDelimiterLoc=0;
        var functionArguments=[];
        var theVariable, remaining;
    
        var wrapInQuotes = function(text) {
            return "'" + text + "'";
        };
    
        for (var key in options) { // Update default delimiters with any custom ones
            if (options.hasOwnProperty(key)) {
                if (options[key] !== undefined) {
                    delimiter[key] = options[key];
                }
            }
        }

        var segments = text.split(delimiter.open); // Split on every occurrence of starting delimiter *(
        var numOfSegments = segments.length;
    
        templateString.push(wrapinQuotes(segments[0])); // Push first segment in
    
        while (i < numOfSegments) { // If there's more...
            closingDelimiterLoc = segments[i].indexOf(delimiter.close); // Find locations of closing delimiter for every extra segment
        
            theVariable = segments[i].slice(0, closingDelimiterLoc); // Slice out every function argument (variable/segment) from character 0 to the closing delimiter
            functionArguments.push(theVariable);
            templateString.push(theVariable); // Push middle segments in (not in quotes, because it's not text but variables)
        
            remaining = segments[i].slice(closingDelimiterLoc + delimiter.close.length); // Remaining string at the end of the text
            templateString.push(wrapinQuotes(remaining)); // Push last segment in
        
            i++
        }


        templateString = 'while(times--) { // Add loop to log template once for each time
            console.log('+templateString.join('+')+') // Join all segments together
        }';
        
        return new Function(functionArguments.join(','), 'times', templateString); // Create the function
    };

The body of the function has to be a string, __but__ those quotes are removed when inserted into the constructor function (hence `wrapInQuotes`).

##### The browser's event system

The `addEventListener` method is an incredibly important part of the DOM API: `target.addEventListener(type, listener);`. We add an `eventObject` as a function argument if we want to gather information about the event that occurred (e.g. `if` statement).

__Custom events__

What if we want to create our own kind of event? We use the `CustomEvent` API.

    
    var myCustomEvent= new CustomEvent( 'partyTime', {timeToParty: true, partyYear: 1999} );

    document.addEventListener('partyTime', function(evt) {
        if (evt.partyYear) {
            console.log( "Partying like it's " + evt.partyYear + "!");
        }

        document.body.style.backgroundImage = 'linear-gradient(90deg, orange, blue)';
    });

    document.dispatchEvent(myCustomEvent); // Trigger event

_How does this work in Backbone?_

Just like before, we get the template from the DOM, convert it to a string, and pass it to `_template`'s function. In app.js, e.g.


    var MenuItemView = Backbone.View.extend({
        events: {
            'click .select-item': 'selectItem'; // If select-item class is clicked, run selectItem function
        }, 
        selectItem: function(e) {
            e.preventDefault();
            router.navigate('select/' + this.model.id, {trigger:true});
        }
    });

Backbone's `.on()` method adds an `events` object to the object. Each key is the name of an event to listen for, each value a list of callbacks to run. See [this link](http://backbonejs.org/#Events) for how to add events. Do not forget to put the events in quotation marks. The callbacks are not quoted.

An `EventTracker` object can manage its own events (`.on()`). It can also let other objects register with them (`.notify()`) to get notified when an event happens. Trigger events using `.trigger()`.

[...]

# Offline

From online-only to offline-first. 

Offline-first: try offline first and try to get stuff from network just after.

---
To open a local host for a project:
1. `git clone` project
2. `cd` into project folder
3. run `npm install` to install dependencies
4. run `npm run serve` to start a second server
5. open `localhost:8888` in browser
---


To have power over the network, developers use a __service worker__, a simple JavaScript file that sits between you and network requests. It runs separately from your page and cannot access DOM. 

__Adding a service worker to a project, in `index.html`:__


    self.addEventListener('fetch', function(event) {
        console.log(event.request);
    });

__Registering service worker as soon as app starts up__, in lessons in `indexcontroller.js` (indexcontroller's constructor takes care of setup of app):

    if (navigator.serviceWorker) { // Feature detect for cross browser compatibility (if faulty for older browsers, all within if will be ignored)
        navigator.serviceWorker.register('/sw.js', { // Location of SW script
            scope: '/my-app/' // Optionally, to demand the SW only controls page(s) whose URL begins with scope
        }).then(function(reg) { // Returns promise, so you can chain
            console.log('Yay!');
        }).catch(function(err) {
            console.log('Boo!');
        })
    }
    
Scopes are useful, as they let you have a different service worker for each project. The default is determined by the location of the service worker script, so usually you do not have to define scope.

---

Methods that will only ever be called by other methods of this object: define starting with `_`, e.g. `this._registerServiceWorker();`.

---

Service workers are limited to __HTTPS__!

### The service worker lifecycle

There are multiple service workers. Updates are downloaded in the background, but the service worker doing this won't take over the old one until the browser opens and closes again. This works as follow. The service worker only takes control of pages when they are loaded. If a page loads via the service worker, it will check for updates to the service worker in the background. Has it changed? Then it becomes the next version. It, however, only takes control when all pages using the current version are gone, to ensure there's only one version running. Seeing that there is always a version that is active, shifting from one to another only works after closing the page.

When the browser refetches a service worker looking for updates, it will go through the browser cache as all requests do. Therefore, keep your cache time 0 on all projects.

### Service worker in Dev Tools

Under Console, you can choose a service worker in the drop down menu. Debugging works with service workers too (Open service worker in Sources and start debugging). By opening the service worker, I refer to the .js file where so far, we put this code:


    self.addEventListener('fetch', function(event) {
        console.log(event.request);
    });

Just add a breakpoint by clicking on the line number and then refresh page to pause script there. Then you can inspect the state of objects.

Service worker also has own panel in Application. 'Unregister' lets us unregister the service worker if you want to refetch from scratch.

You can __add a new service worker__ (e.g. new branch, change something in .js file), which will then be turned into a _waiting service worker_.

__To get the new service worker active__, as said before we close _all_ pages that use the current service worker, or navigate to another page that is not in the service worker scope. A shortcut for this is to hold `Shift` while refreshing the page!

### Hijacking requests

So far requests go:
page > service worker fetch event > onto the network through the Http cache

What if we want to catch the request as it hits the service worker, and then respond ourselves (nothing goes to network - as we are offline)? In service worker script, call `event.respondWith()`, which takes either a response object or a promise that resolves with a response:


    self.addEventListener('fetch', function(event) {
        event.respondWith( // Tells browser we will handle the response to all requests ourselves
            new Response(bodyOfResponse, { // Body can be blob, buffer, string, ... Can even include HTML
                headers: {'Content-Type': 'text/html'} // Or whatever, to set certain header values (see changes in Network > click on right URL > see Headers)
            })
        );
    });

Now if you would bring the server down and refresh the page, your body of response will show/do/display!

We can instead go to the network for a response, but not for the thing that was requested, using `fetch(url)` and a _promise_ as the `responseWith()` argument:

    self.addEventListener('fetch', function(event) { // Performs normal browser fetch, so results may come from cache
        event.respondWith( // Response to all requests
            fetch('url.com/to/fetch').then(function(response) { // e.g. fetch('/imgs/dr-evil.gif')
                return response.json(); // Parse
            }).then(function(data) {
                console.log(data)
            }).catch(function() {
                console.log('Failure!')
            })
        );
    });


##### Selective requests

If we do not want to hijack every URL, but, for example, only respond to requests (parts of website) with a url ending in ".jpg":


    self.addEventListener('fetch', function(event) {
        if (event.request.url.endsWith('.jpg')) {
            event.respondWith(
                fetch('/imgs/dr-evil.gif')
            );
        }
    });

So far we decided the response based on the request URL.  We can also decide a response based on the response we get back from the network:


    self.addEventListener('fetch', function(event) {
        event.respondWith(
            fetch(event.request).then(function(response) { // Response we get back from network
                if (response.status == 404) { // If response is 404: Not found (page does not exist)
                    return new Response("Whoops, not found"); // Respond with this message
                }
                return response; // Otherwise return response we received (the online page)
            }).catch(function() { // If it can't make a connection to a server at all (it is offline)
                return new Response('Failure!') 
            })
        );
    });

If we want to display a gif instead:


    self.addEventListener('fetch', function(event) {
      event.respondWith(
        fetch(event.request).then(function(response) {
          if (response.status === 404) {
          // Remember, if you return a promise within a promise, it passes the eventual value to the outer promise, so:
            return fetch('/imgs/dr-evil.gif'); // We don't need to create a new response promise, but instead we return a fetch
          }
          return response;
        }).catch(function() {
          return new Response("Uh oh, that totally failed!");
        })
      );
    });

If we want to display the whole web page when offline, we will need to store all HTML, CSS, JavaScript and images in a cache using the `cache` API. Gives us `caches` object on global. To create or open cache: `caches.open('my-stuff').then(function(cache) { // ... });`. That returns promise for cache of that name. If I haven't opened a cache of that name before, it creates one and returns it. 

A cache box contains request and response pairs from any secure origin. We can store stuff from both our own origin as well as elsewhere on the web. Add items using `cache.put(requestOrURL, response)`. To take an array of requests or URLs, fetch them and put request-response pairs into the cache, use `cache.addAll(['/foo', '/bar']);` (if any one fails, none of them are added). To get something out of the cache, use `cache.match(requestOrURL);`, which returns promise if one is found, or null otherwise. `caches.match()` does same, but tries to find match in any cache.

When to store this information? In service worker file, add (above the fetch eventListener):


    self.addEventListener('install', function(event) {
        event.waitUntil( // (takes promise) Signal process of install 
            caches.open('wittr-static-v1') // (returns promise) Pass promise: if/when it resolves, the browser knows install is complete, when it fails, service worker should be discarded
            .then(function(cache) {
                return cache.addAll([ // addAll also returns promise, so I return it
                    '/', 
                    'js/main.js', 
                    'css.main.css', 
                    'imgs/icon.png', 
                    'https://fonts.gstatic.com/blabla'
                ]);
            })
        );
    });

Using cached items in responses:


    self.addEventListener('fetch', function(event) {
    	event.respondWith(
    		caches.match(event.request)// Search for match in caches for this particular request (if there is nothing, promise = undefined)
    		.then(function(response) {
    			if (response) return response; // If it's truthy and I do have a match, return it
    			return fetch(event.request); // Else, return request
    		})
    	);
    });

---

Names of all caches: `caches.keys();`. Returns promise.

---

##### Unobtrusive app updates

To continuously update, we need to make a change to service worker. The browser will then treat this as new version. Because it's new, it will get its own install event, where it will fetch updates and put them in new cache (no disruption of current cache that's used by old service worker). In order to make this new cache happen, we changed the name of our cache. Before anything, __change something in the script that is the 'update'.__ Then you want to delete all old caches. So:

    var staticCacheName = 'wittr-static-v2';

    self.addEventListener('install', function(event) {
      event.waitUntil(
        caches.open('wittr-static-v2').then(function(cache) { // Update cache name
          return cache.addAll([
            '/',
            'js/main.js',
            'css/main.css',
            'imgs/icon.png',
            'https://fonts.gstatic.com/s/roboto/v15/2UX7WLTfW3W8TclTUvlFyQ.woff',
            'https://fonts.gstatic.com/s/roboto/v15/d-6IYplOFocCacKzxwXSOD8E0i7KZn-EPnyo3HZu7kw.woff'
          ]);
        })
      );
    });
    
    self.addEventListener('activate', function(event) {
      event.waitUntil( // Wait with activation until all old caches are deleted
        caches.caches.keys().then(function(cacheNames) { // .keys() gives us promise with all cache names
            return Promise.all( // Wrap in Promise.all() so we wait on completion of all those promises
                cacheNames.filter(function(cacheName) {
                    return cacheName.startsWith('wittr-') && // Only interested in caches that start with wittr- (optional, so we don't delete caches from other apps)
                    cacheName != staticCacheName; // And not in the cache we defined earlier
                }).map(function(cacheName) { // Map them and delete them
                    return cache.delete(cacheName);
                });
            );
        });
      );
    });
    
    self.addEventListener('fetch', function(event) {
      event.respondWith(
        caches.match(event.request).then(function(response) {
          return response || fetch(event.request);
        })
      );
    });

---

Insight into service worker life cycle (remember reg that was the returned promise from the initial registration): `reg.unregister()`, `reg.update()`, `reg.installing`, `reg.waiting`, `reg.active`. The registration object will emit an event when a new update is found:


    reg.addEventListener('updatefound', function() {
        // ...
    });

When fired, `.installing` has become the new worker.

##### How to tell users about updates

On the service workers themselves (`var sw = reg.installing;`), you can look at their state (`console.log(sw.state);`).
State can be `installing` (install event is fired, but has not completed), `installed` (installed successfully), `activating` (activate event has fired, but not complete), `activated` (activated successfully, ready to receive fetch events), `redundant` (service worker has been thrown away).

Service worker fires event:


    sw.addEventListener('statechange', function() { // Whenever state value changes, this is fired
        // ...
    });

Also, `navigator.serviceWorker.controller` refers to the service worker that controls this page. So, all in once, in indexController.js where you registered the service worker:

    IndexController.prototype._registerServiceWorker = function() { // Ignore this
      if (!navigator.serviceWorker) return; // Ignore this
    
      var indexController = this; // Ignore this
    
      navigator.serviceWorker.register('/sw.js').then(function(reg) {
        if (!navigator.serviceWorker.controller) { // If there's no controller, user already has latest version as they are using network, so
          return; // Exit early
        }
        if (reg.waiting) { // If there's an update ready and waiting
          indexController._updateReady(); // Call function that notifies user about update (stored in object indexController)
        }
        if (reg.installing) { // If updated worker is installing
          reg.installing.addEventListener('statechange', function() { // Track progress (this anonymous function can also be put in function that is called here as e.g. indexController._trackInstalling(reg.installing) / This function can be placed in IndexController.prototype._trackInstalling = function(worker) {var indexController = this; worker.addEventListener('statech...
            if (this.state == 'installed') { // If it becomes installed
              indexController._updateReady(); // Call notification
            }
          });
          return; // Otherwise, early exit
        }
        reg.addEventListener('updatefound', function() { // Otherwise, listen for new installing workers arriving
          reg.installing.addEventListener('statechange', function() { // If one arrives, track state of installing worker
            if (this.state === 'installed') { // If it reaches installed state...
                indexController._updateReady(); // Inform user
            }
          });
        });
      });
    };
    
    IndexController.prototype._updateReady = function() { // This is the function that places the notification
      var toast = this._toastsView.show("New version available", { // This is what will show after an update
        buttons: ['whatever']
      });
    };

##### Let the user decide whether they want the update or not    
Button users can press to get the latest version: button needs to tell waiting service worker to take over straight away, bypassing usual cycle. Then refresh page so it reloads with latest assets from newest cache. To achieve this, we use `self.skipWaiting()` (self is service worker), called when user hits refresh. To send signal from page to waiting service worker: `reg.installing.postMessage({foo: 'bar'});`. To receive/listen for signal from page in service worker: `self.addEventListener('message', function(event) { event.data }; });`, where event.data is {foo: 'bar'}.

To fire event on page when value changes (i.e. signal that we should reload page):


    navigator.serviceWorker.addEventListener('controllerchange', function() { // navigator.serviceWorker.controller has changed, meaning a new service worker has taken over
        // ... 
    });

__To see this in action, see the quiz answer in _lesson 4.13.25___. It is a minor modification of the previous code.

__Then, finally, to swap out the root page for the skeleton page__, you need to bump up the version, add /skeleton to array, request the new URL, compare it with the origin, and take the skeleton out of the new cache.

__FINAL CODE__:

`index.js`:


    var staticCacheName = 'wittr-static-v4'; // Bump up version to 4
    
    self.addEventListener('install', function(event) {
    
      event.waitUntil(
        caches.open(staticCacheName).then(function(cache) {
          return cache.addAll([
            '/skeleton', // Cache skeleton instead of root page with all data in it
            'js/main.js',
            'css/main.css',
            'imgs/icon.png',
            'https://fonts.gstatic.com/s/roboto/v15/2UX7WLTfW3W8TclTUvlFyQ.woff',
            'https://fonts.gstatic.com/s/roboto/v15/d-6IYplOFocCacKzxwXSOD8E0i7KZn-EPnyo3HZu7kw.woff'
          ]);
        })
      );
    });
    
    self.addEventListener('activate', function(event) {
      event.waitUntil(
        caches.keys().then(function(cacheNames) {
          return Promise.all(
            cacheNames.filter(function(cacheName) {
              return cacheName.startsWith('wittr-') &&
                     cacheName != staticCacheName;
            }).map(function(cacheName) {
              return caches.delete(cacheName);
            })
          );
        })
      );
    });
    
    self.addEventListener('fetch', function(event) {
      var requestUrl = new URL(event.request.url); // Pause request URL
    
      if (requestUrl.origin === location.origin) { // Check if request origin is same as current origin (we only want to intercept route requests for same origin)
        if (requestUrl.pathname === '/') { // Check pathname - if it's the route, respond with
          event.respondWith(caches.match('/skeleton')); // The skeleton straight from the cache
          return; // No need to go back to network, as skeleton is cached as part of install step
        }
      }
    
    
      event.respondWith(
        caches.match(event.request).then(function(response) {
          return response || fetch(event.request);
        })
      );
    });
    
    self.addEventListener('message', function(event) {
      if (event.data.action === 'skipWaiting') {
        self.skipWaiting();
      }
    });


`indexController.js`:


    import PostsView from './views/Posts';
    import ToastsView from './views/Toasts';
    import idb from 'idb';
    
    export default function IndexController(container) {
      this._container = container;
      this._postsView = new PostsView(this._container);
      this._toastsView = new ToastsView(this._container);
      this._lostConnectionToast = null;
      this._openSocket();
      this._registerServiceWorker();
    }
    
    IndexController.prototype._registerServiceWorker = function() {
      if (!navigator.serviceWorker) return;
    
      var indexController = this;
    
      navigator.serviceWorker.register('/sw.js').then(function(reg) {
        if (!navigator.serviceWorker.controller) {
          return;
        }
    
        if (reg.waiting) {
          indexController._updateReady(reg.waiting);
          return;
        }
    
        if (reg.installing) {
          indexController._trackInstalling(reg.installing);
          return;
        }
    
        reg.addEventListener('updatefound', function() {
          indexController._trackInstalling(reg.installing);
        });
      });
    
      // Ensure refresh is only called once.
      // This works around a bug in "force update on reload".
      var refreshing;
      navigator.serviceWorker.addEventListener('controllerchange', function() {
        if (refreshing) return;
        window.location.reload();
        refreshing = true;
      });
    };
    
    IndexController.prototype._trackInstalling = function(worker) {
      var indexController = this;
      worker.addEventListener('statechange', function() {
        if (worker.state == 'installed') {
          indexController._updateReady(worker);
        }
      });
    };
    
    IndexController.prototype._updateReady = function(worker) {
      var toast = this._toastsView.show("New version available", {
        buttons: ['refresh', 'dismiss']
      });
    
      toast.answer.then(function(answer) {
        if (answer != 'refresh') return;
        worker.postMessage({action: 'skipWaiting'});
      });
    };
    
    // open a connection to the server for live updates
    IndexController.prototype._openSocket = function() {
      var indexController = this;
      var latestPostDate = this._postsView.getLatestPostDate();
    
      // create a url pointing to /updates with the ws protocol
      var socketUrl = new URL('/updates', window.location);
      socketUrl.protocol = 'ws';
    
      if (latestPostDate) {
        socketUrl.search = 'since=' + latestPostDate.valueOf();
      }
    
      // this is a little hack for the settings page's tests,
      // it isn't needed for Wittr
      socketUrl.search += '&' + location.search.slice(1);
    
      var ws = new WebSocket(socketUrl.href);
    
      // add listeners
      ws.addEventListener('open', function() {
        if (indexController._lostConnectionToast) {
          indexController._lostConnectionToast.hide();
        }
      });
    
      ws.addEventListener('message', function(event) {
        requestAnimationFrame(function() {
          indexController._onSocketMessage(event.data);
        });
      });
    
      ws.addEventListener('close', function() {
        // tell the user
        if (!indexController._lostConnectionToast) {
          indexController._lostConnectionToast = indexController._toastsView.show("Unable to connect. Retrying…");
        }
    
        // try and reconnect in 5 seconds
        setTimeout(function() {
          indexController._openSocket();
        }, 5000);
      });
    };
    
    // called when the web socket sends message data
    IndexController.prototype._onSocketMessage = function(data) {
      var messages = JSON.parse(data);
      this._postsView.addPosts(messages);
    };

---

