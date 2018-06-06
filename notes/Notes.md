# GOOGLE DEVELOPER NANODEGREE

---

# Responsiveness
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










