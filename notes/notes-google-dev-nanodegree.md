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


	<meta name="viewport" content="width=device-width, initial-scale=1.0">

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

# Assistive technology semantics

__Using the keyboard only.__ 

`tab`: forward, `shift` + `tab`: backwards, `up, down, left, right` arrow: navigate within.

### TAB ORDER (corresponds with DOM order)

`tabindex` attribute (applied to any html element). Only add this to interactive elements*:

`-1` = not in tab order, can be focused with `.focus()` method.

`0` = in tab order and can be focused with `.focus()` method.

Above `0` = jump element to front of tab order (works way up: 1, 2, 3, ...). DISCOURAGED.

[*] Except for single page designs with anchors (managing focus). Use the -1 value for that.

To skip a link (e.g. navigation):


    <a href="#maincontent" class="skip-link">Skip</a> // Step 1, put in DOM before navigation
    <main id="maincontent" tabindex="-1"></main> // Step 2, ID of other element on page

In CSS, `.skip-link` has:


    position: absolute,
    top: -40px, // To hide it on page as it's above navigation

And `.skip-link:focus` has this, which matches every time corresponding element gains focus, after which it appears back on screen:


    top: 0;

Roving focus/tabindex (basically toggling tabindex), `tabindex="-1";` on all elements except currently active one. That one gets `0` and `checked` attribute. Then change tabindex after keyboard event listener on compoonent, next item is `0`, previous one is `1`, call focus method, `checked` goes down. Repeat. So that:

Tab into is active radio focus, left/right arrow is another radio focus, another tab is focus out of radio group, tab back in is last active radio gets focus.

---

To find where focus is: DevTools (`document.activeElement`).

---

Avoid the keyboard trap (except for temporary ones)! 

`display:none` and `visibility:hidden` both prevent focusin on an element an all children inside it, as it opts element out of tab order. Set this back after the focus has passed in the DOM.

Type of element: element role.

Modified tree (DOM tree without any visual elements): accessibility tree (a11y tree).

### SEMANTICS

Role, name/label, value, state.

Name/label can be visible, or it can be invisible (`alt` attribute, which will only be used if image is not available). Not having an `alt` attribute means image is not present in a11y tree.


---

JavaScript headings snippet to see all headers:


    for (var i = 0, headings = $$('h1,h2,h3,h4,h5,h6'); i < headings.length; i++)
	console.log(headings[i].textContent.trim() + " " + headings[i].tagName, headings[i]);
    
---

_LINKS_

Use anchor tag (`<a>`) with `href` attribute.

Use button tag.

Image with link: use `alt` text.

Use descriptive texts and don't use `<span>`.

Page structure (use these in HTML and CSS, they are more descriptive):
`header, main, footer, nav, article, section, aside`.

### WAI-ARIA

Used for fake, non-native elements; changes elements role, state and properties and finetunes accessible names for elements.

With ARIA, we can specify attributes on elements which modify the way that element is translated into the a11y tree. E.g. `<div>` that is actually checkbox: add `<div role="checkbox" aria-checked="true">` (or `false`) in same area as tabindex attribute. _ARIA is always applied to `<div>`!_.

Other ways to label: `aria-label` and `aria-labelledby` (element is labelled by another element. It is therefore relational. Other relational ARIA attributes are `aria-owns, aria-activedescendant, aria-describedby, aria-posinset` and `aria-setsize`. Activedescendant makes focus appear somewhere other than webpage focus. Posinset refers to position of items, setsize to number of visible items. All of these go to `id`'s.).

Landmarks that ARIA offers:
`role` = `banner, search, dialog, navigation, main, complementary, contentinfo`.

__What is hidden in the a11y tree?__

All that is explicitly hidden (`display:none, visibility:hidden, <span hidden>`). 

__What is not hidden in the a11y tree?__

Not hidden, and therefore often used as screenreader-only content:


    .screenreader {
        position: absolute;
        left: -10000px; // Far off screen
    }

Also not hidden are `aria-label` in HTML, `aria-labelledby` in HTML, `aria-describedby` in HTML referencing to an element which is otherwise hidden.

__What is excluded from screenreaders but not visually?__

`aria-hidden:true;`

__How to alert screen readers:__

`aria-live = "off"` (default)

`aria-live = "polite"` (alert user to change after finishing what you were doing)

`aria-live = "assertive"` (interrupt and alert immediately)

`aria-live` region should be in initial page load. To finetune this:

`aria-atomic = "true"` (take whole container to screen reader (e.g. if only month is updated, also read day and year)

`aria-relevant = "additions"/"text"/"removals"/"all"` (what info is read out loud)

`aria-busy = "true"` (temporarily ignore changes to element)

### Style

Focus ring:

    
    :focus {
        outline: ...; // Can be used in combo with :hover / Add styles to both
    }

Remove default focus:


    .class:focus {
        outline: 0; // But in general, just stick with focus
    }
    
Just target before pseudo element:


    .class:focus::before {
        box-shadow: 0 0 1px #5b9dd9;
    }

Replace CSS classes with aria-attributes! Then, you can verify that aria-states are set correctly because they trigger actual visual updates to the component.

_STYLES FOR ENTIRE SITE:_

Responsiveness:
1. Use meta viewport tag (on every `.html` file!!!)


    <meta name="viewport" content= "width=device-width, initial-scale=1">

2. Design with responsive grid

Use `%` (relative to containing block), `em` (" font-size of parent, for text), `rem` (" root, for text).

3. Use appropriate touch targets with a minimal size of 48px. Around each touch target, add a 32DIP margin to avoid overlap.

_COLOR AND CONTRAST:_

Minimum contrast ratio is `4.5:1` for body text and images, `3:1` for large text of over 18px or 14px-bold). For low vision enhanced, these ratios are `7:1` and `4.5:1`.

In DevTools, use Audits to chec accessibility. Click on item to see accessibility properties. Color should not be the only thing to point out the difference. Check this with high-contrast mode.

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

__Adding a service worker to a project, in `index.js`:__


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
        caches.keys().then(function(cacheNames) { // .keys() gives us promise with all cache names
            return Promise.all( // Wrap in Promise.all() so we wait on completion of all those promises
                cacheNames.filter(function(cacheName) {
                    return cacheName.startsWith('wittr-') && // Only interested in caches that start with wittr- (optional, so we don't delete caches from other apps)
                    cacheName != staticCacheName; // And not in the cache we defined earlier
                }).map(function(cacheName) { // Map them and delete them
                    return caches.delete(cacheName);
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

# React

##### Composition
Composition occurs when simple functions are combined together to create more complex functions. Think of each function as a single building block that does one thing (DOT). When you combine these simple functions together to form a more complex function, this is composition. E.g.


    function getProfileLink (username) {
      return 'https://github.com/' + username
    }
    
    function getProfilePic (username) {
      return 'https://github.com/' + username + '.png?size=200'
    }
    
    function getProfileData (username) {
      return {
        pic: getProfilePic(username),
        link: getProfileLink(username)
      }

##### Imperative vs. declarative
_Imperative_ code instructs JavaScript on how it should perform each step (e.g. for loop with iterator, length of loop, storing in new array). With _declarative_ code, we tell JavaScript what we want to be done, and let JavaScript take care of performing the steps (e.g. for loop with `.map()`). __React is declarative.__

##### Data flow
Unidirectional: In React, data flows in only one direction, from parent to child(ren). The component that stores the data (the parent element) should be the one that updates the data.

##### React and JS
Important JS functions for React: `.map()` and `.filter()`. 

`.map()`: Gets called on an existing array and __returns a new array__ based what's returned from the function that's passed as an argument. E.g.


    const musicData = [
        { artist: 'Adele', name: '25', sales: 1731000 },
        { artist: 'Drake', name: 'Views', sales: 1608000 },
        { artist: 'Beyonce', name: 'Lemonade', sales: 1554000 },
        { artist: 'Chris Stapleton', name: 'Traveller', sales: 1085000 },
        { artist: 'Pentatonix', name: 'A Pentatonix Christmas', sales: 904000 },
        { artist: 'Original Broadway Cast Recording', 
          name: 'Hamilton: An American Musical', sales: 820000 },
        { artist: 'Twenty One Pilots', name: 'Blurryface', sales: 738000 },
        { artist: 'Prince', name: 'The Very Best of Prince', sales: 668000 },
        { artist: 'Rihanna', name: 'Anti', sales: 603000 },
        { artist: 'Justin Bieber', name: 'Purpose', sales: 554000 }
    ];
    const albumSalesStrings = musicData.map(datum => `${datum.name} by ${datum.artist} sold ${datum.sales} copies`);
 
 Returns:
 
 
    [ '25 by Adele sold 1731000 copies',
     'Views by Drake sold 1608000 copies',
     'Lemonade by Beyonce sold 1554000 copies', ... ] // etc.

`.filter()`: Similar to `.map()`, but only returns items in array that pass 'test'. 


    const results = musicData.filter(datum => datum.name.length > 9 && datum.name.length < 26);

Returns:


    [ { artist: 'Pentatonix', name: 'A Pentatonix Christmas', sales: 904000 },
      { artist: 'Twenty One Pilots', name: 'Blurryface', sales: 738000 },
      { artist: 'Prince', name: 'The Very Best of Prince', sales: 668000 } ]

Both can be combined, e.g. to log only the artists that sold over 1000000 copies:

        const popular = musicData.filter(datum => datum.sales > 1000000).map(datum => `${datum.artist} is a great performer`);

First run filter, then run map!

## Rendering UI

React uses objects instead of string literals to build UI. The building blocks of React are components. 

1. Creating elements (will return plain JS object)



    React.createElement( /* type */, /* props */, /* content */ );

Type is either string or React Component.

Props is either null or an object.

Content is either null, a string, a React Element, or a React Component. We can also pass other elements as the third element, just passing another (or multiple) `.createElement`(s) or a `.map()` function that refers to an earlier declared array, in there. This creates nested HTML. E.g.


    const people = [ {name: 'Pete'}, {name: 'Jane'}];
    const element = React.createElement('ol', {key: person.name}, people.map(person => React.createElement('li', null, person.name)));
    
When you use an array, React needs a unique key prop to every child element.

Note that we are describing DOM nodes, not HTML strings. So:


    const element = React.createElement('div', {className: 'welcome-message'}, 'hello world');

works, while:


    const element = React.createElement('div', {class: 'welcome-message'}, 'hello world');
    
does not, even though in the HTML file it's displayed as:


    <div data-reactroot class="welcome-message">hello world</div>

2. Placing elements in the DOM


    ReactDOM.render( /* type */, /* position */ ); e.g.
    ReactDOM.render(element, document.getElementById('root'));

### JSX (syntax extension, used instead of createElement)


    const element = <ol><li>{people[0].name}</li></ol> // Note curly braces!

    or, more complex:
    
    const element = <ol>
        {people.map(person => 
        ( <li key={person.name}>{person.name}</li>
        ))}
        </ol>

### Rendering components

Typically, though, instead of `.createElement()` and JSX, we'll use one of React's key features, Components, to construct our UI.

React provides a base component class that we can use to group many elements together. You can think of your component classes as factories that produce instances of components. These component classes should follow the single responsibility principle and just "do one thing".


    class ContactList extends React.component { // Or extends Component, dependent on way you import module at beginning of script
        render() {
            const people = [
                { name: 'Michael' },
                { name: 'Ryan' },
                { name: 'Tyler }
            ]
            
            return = <ol>
                {people.map(person => {
                    <li key={person.name}>{person.name}</li>
                ))}
            </ol>
        }
    }
    
    ReactDOm.render(<ContactList/>, document.getElementById('root'));

As you can see above, we render and treat as if they were a single element.

### Webpack

Build tool for React. JSX is awesome, but it does need to be transpiled into regular JavaScript before reaching the browser. We typically use a transpiler like Babel to accomplish this for us. We can run Babel through a build tool, like Webpack which helps bundle all of our assets (JavaScript files, CSS, images, etc.) for web projects.
To streamline these initial configurations, we can use Facebook's Create React App package to manage all the setup for us! 

    npm install -g create-react-app

Create app:


    create-react-app contacts // Or whatever name you want to give project

This will create the project in the folder you're in.

CD into project folder and start development server:


     npm start
     
This will automatically open a browser window with the app.

In the code: the JSX class (`class App extends Component`) can be found under `App.js`, while the render function can be found under `index.js`. `index.html` shows the HTML document that all of the JS is running in.

__So:__ Build solo elements, each within `class ~whatever~ extends Component`. Then invoke all of those elements in `class App extends Component`, like so:


    class ContactList extends React.Component {
        render() {
            const people = this.props.contacts
            
            return <ol> 
                {people.map(person => {
                    <li key={person.name}>{person.name}</li>
                ))}
            </ol>
        }
    }

    class App extends Component {
        render() {
            return (
                <div className="App">
                    <ContactList contacts={[
                        { name: 'Michael' },
                        { name: 'Ryan' },
                        { name: 'Tyler }
                    ]}/>
                    <ContactList contacts={[ // Just use again, with different props
                        { name: 'Pete' },
                        { name: 'Jane' },
                        { name: 'Erica }
                    ]}/>
                </div>
            );
        }
    }

### State management

_Props_: allow to pass data into components.

_Functional components_: alternative to creating React components.

_Controlled components_: allow to hook up forms in application to component state.

Note: at the end of our components (each component is a separate file), we export it (`export default ListContacts`) so that we can import it inside of our `app.js` file.

You always have to specify `render()`!!! In render, access data through `this.props`. As the class is linked to `app.js` (by importing it), it will find the right data.

So, as functions have arguments, components have props.

E.g. 
1. You have an array
2. You pass it down to your class component as a prop
3. Inside of the component (which is specified in a separate file), we do something with this.props.whatYouPassedDown. Any prop that's passed into the component is accessible on the `this.props` object.

Passing multiple props individually to component, e.g. a JS function (like `Date.now()`) and a normal string:


    <Component propOne={javaScript.thing()} propTwo='String'/>

##### RECAP

A prop is any input that you pass to a React component. Just like an HTML attribute, a prop name and value are added to the Component.


    // passing a prop to a component
    <LogoutButton text='Wanna log out?' />

In the code above, text is the prop and the string 'Wanna log out?' is the value. All props are stored on the this.props object. So to access this text prop from inside the component, we'd use this.props.text:


    // access the prop inside the component
    ...
    render() {
        return <div>{this.props.text}</div>
    }
    ...

### Stateless functional components

If your component does not keep track of internal state (i.e., all it really has is just a render() method), you can declare the component as a Stateless Functional Component. A.k.a. __if all your component has is the render method__, instead of creating component as class


    class User extends React.Component {
        render() {
            return (
                <p> Username: {this.props.username} </p>
            )
        }
    }

we can also create it as normal function, and use


    function User(props) { // Props passed as argument here
        return (
            <p> Username: {props.username} </p> // No longer using this!
        )
    }

Stateless functional components:
1. Take in props
2. Return descriptions of UI
3. Don't use the this keyword

A more elaborate example:


    import  React, { Component } from 'react'

    function ListContacts (props) {
      return (
        <ol className='contact-list'>
          {props.contacts.map((contact) => (
            <li key={contact.id} className='contact-list-item'>
              <div className='contact-avatar' style={{
                backgroundImage: `url(${contact.avatarURL})`
              }}/>
              <div className='contact-details'>
                <p>{contact.name}</p>
                <p>{contact.email}</p>
              </div>
              <button className='contact-remove'>
                Remove
              </button>
            </li>
          ))}
        </ol>
      )
    }
    
    export default ListContacts

### State (current state of application)
Earlier in this lesson, we learned that props refer to attributes from parent components. In the end, props represent "read-only" data that are immutable. A component's state, on the other hand, represents mutable data that ultimately affects what is rendered on the page.

Put your data in the App class, as an object to state! That way, React can manage the state.


    class App extends Component {
        state = {
            contacts: [{...

A component's state can be defined at initialization. A component can alter its own internal state. By having a component manage its own state, any time there are changes made to that state, React will know and automatically make the necessary updates to the page. We just have to think about updating state and React compares the previous output and new output, determines what has changed, and makes these decisions for us (Reconciliation). Again: _state reflects mutable information that ultimately affects rendered output_.

`setState` is used to update the state. We can pass it a function, having previous state as argument. We use this if we are updating the new state based on the current state. We can also pass in an object, which will be merged with the current states. We usually use the second method. __Your UI, then, is just a function of your state.__

Method 1:


    removeContact = (contact) => {
        this.setState((state) => ({
        ...
        }))

Method 2:


    removeContact = (contact) => {
        this.setState({
        ...
        
    }
    
Type checking a component's props with `Proptypes`: run `npm install --save prop-types`. Then, in the component: `import PropTypes from 'prop-types'`, and in ListContacts.js, specify:

    ListContacts.propTypes = {
    	contacts: PropTypes.array.isRequired,
    	onDeleteContact: PropTypes.func.isRequired
    } // Note that it kind of serves as nice documenation for how to use this component itself!

### Controlled components

Components which render a form, but the source of truth for that form lives inside of the component state, rather than inside the DOM. Benefits:
1. Instant input validation
2. Conditionally disable/enable buttons
3. Enforce input formats

__See lesson 5.3.7.__ To recap how user input affects the ListContacts component's own state in the example: The user enters text into the input field; An event listener invokes the updateQuery() function on every onChange event; updateQuery() then calls setState(), merging in the new state to update the component's internal state; because its state has changed, the ListContacts component re-renders.

With Controlled Components, our form state lives inside of the component. Because of this, we can easily update our UI based on that form state.

##### React developer tools

Allows us to inspect component hierarchy along with respective props and states. 

##### Using destructuring to make code cleaner

Instead of `this.props.contacts` etc., we can just declare our variables as such:


    const { contacts, onDeleteContact } = this.props
    const { query } = this.state

and simply use `contacts` etc. instead.

When it comes to keeping track of data in your app, think about what will be done with that data, and what that data will look like as your user interfaces with your app. If you want your component to store mutable local data, consider using state to hold this information. Many times, it is state that will be used to manage controlled form elements in your components.

On the other hand, if some information isn't expected to change over time, and is generally designed to be "read-only" throughout your app, consider using props instead. Both state and props will generally be in the form of an object, and changes in either will trigger a re-render of the component, but they each play very different roles in your app.

### Fetch data from a database

Do not make AJAX request inside render(); this should be free of side-effects and asynchronously. Instead, use __componentDidMount lifecycle event__. Lifecycle events are special methods each component can have that allow us to hook into the views when specific conditions happen.

`componentWillMount`: invoked immediately before component is inserted in DOM.

`componentDidMount`: invoked immediately after the component is inserted into the DOM. Should be used if you're fetching remote data or doing an AJAX request.

`componentWillUnmount()`: invoked immediately before a component is removed from the DOM.

`componentWillReceiveProps()`: invoked whenever the component is about to receive brand new props.

##### componentDidMount()

Is used as just another function in the class of the component file. E.g.


    import React, { Component } from 'react';
    import fetchUser from '../utils/UserAPI';
    
    class User extends Component {
      constructor(props) {
        super(props)
    
        this.state = {
          name: '',
          age: ''
        }
      }
    
      componentDidMount() {
        fetchUser().then((user) => this.setState({
          name: user.name,
          age: user.age
        }))
      }
    
      render() {
        return (
          <div>
            <p>Name: {this.state.name}</p> // Empty string at first, so don't actually display, only until component has been mounted, data is fetched and setState() is called and updates properties. Since state has changed, render() gets called again, which re-renders page with values.
            <p>Age: {this.state.age}</p> // "
          </div>
        )
      }
    }

    export default User;

In recap, the following lifecycle events are used for the following purposes:
1. Adding to the DOM: `constructor()`, `componentWillMount()` (!), `render()` and `componentDidMount()` (!).
2. Re-rendering: `componentWillReceiveProps()` (!), `shouldComponentUpdate()`, `componentWillUpdate()`, `render()`, and `componentDidUpdate()`.
3. Removing from the DOM: `componentWillUnmount()` (!).

[!!!] In graph, see: https://d17h27t6h515a5.cloudfront.net/topher/2017/June/59519fa9_nd019-c1-l4-lifecycle-events/nd019-c1-l4-lifecycle-events.png.

### Managing app location with React Router

React router is a tool that lets us use React to build a Single Page App. It turns React projects into single-page applications, by providing a number of specialized components that manage the creation of links, manage the app's URL, provide transitions when navigating between different URL locations, etc.

To install, run:


    npm install --save react-router-dom

##### <BrowserRouter/>

Listens to changes in URL and makes sure right screen shows up. In `index.js`, import this BrowserRouter (`import { BrowserRouter } from 'react-router-dom'` and wrap `<App/>` (`<BrowserRouter><App/></BrowserRouter>`). This sets up the router for the whole app.

When you use BrowserRouter, you're creating a `history` object which will listen to changes in the URL and make sure your app is made aware of those changes.

##### <Link/>

With `Link`, we provide declarative, accessible navigation around your application, used instead of anchor tags (`<a>`). By passing a to property to the Link component, you tell your app which path to route to.


    <Link to="/about" className="about">About</Link>

You could also pass an object into the `to` prop:

    <Link to={{
      pathname: '/courses',
      search: '?sort=name',
      hash: '#the-hash',
      state: { fromDashboard: true }
    }}>
      Courses
    </Link>

##### <Route/>

The final component is `<Route/>`. It takes a path that will match the URL or not. If so, route will render UI. If not, it doesn't render anything. 

Again, first import route in `App.js`. Then add the  to our render method. Do not forget the difference between partial paths and exact paths!!!


      render() {
        return (
          <div className="app">
          	<Route exact path="/" render={() => ( // Only match exactly this, not if part of the URL is /
    	      	<ListContacts
    	        contacts={this.state.contacts}
    	        onDeleteContact={this.removeContact}
    	        />
    	        )}/>
          	<Route path="/create" component={CreateContact}/>
          </div>
        )
      }

To see how to create a form and store the values that are inserted to be used later, see __lesson 5.5.6__!

### Getting started with the APIs

##### Google maps

Map types: road map (default), satellite, hybrid, terrain.

Load a Google Map into your site (you can separate JS into separate file):


     <body>
        <div id="map"></div> // Add DIV with map ID
        <script>
            var map; // Add map variable
            function initMap() { // Add function to load map after page loads/before user interacts with map
                // Constructor creates a new map instance - only center and zoom are required. First specification is where in page to load map (the map div), second is what part of world to show. Zoom can go up to 21.
                map = new google.maps.Map(document.getElementById('map'), {
                    center: {lat: 40.7413549, lng: -73.9980244},
                    zoom: 13
                });
            }
        </script>
        // Add this script tag to load API (add own API key)
        <script async defer
            src="https://maps.googleapis.com/maps/api/js?key=MYAPIKEY&v=3&callback=initMap">
        </script> 

    </body>

##### Highlight one spot on the map (in your JS file)

INSIDE `InitMap()` FUNCTION: 

Map your listings by creating variables using latlong coordinates. E.g.


    var home = {lat: 52.589679, lng: 13.469670};

To make it appear on the map, we create a marker. We can add more properties, here are some examples:


    var marker = new google.maps.Marker({
        position: home, // Where marker should appear
        map: map, // The map it should appear on
        title: 'Random spot!' // Appears when hovering over (optional)
    });
  
Add an info window to a marker:


    var infowindow = new google.maps.InfoWindow({
        content: 'Whatever!'
    });
    marker.addListener('click', function() { // To tell it when and where to open, as it doesn't open automatically like the marker does
        infowindow.open(map, marker);
    });

##### Highlight multiple spots on the map

Create array of locations.


    var locations = [
          {title: 'Park Ave Penthouse', location: {lat: 40.7713024, lng: -73.9632393}},
          {title: 'Chelsea Loft', location: {lat: 40.7444883, lng: -73.9949465}},
          {title: 'Union Square Open Floor Plan', location: {lat: 40.7347062, lng: -73.9895759}},
          {title: 'East Village Hip Studio', location: {lat: 40.7281777, lng: -73.984377}},
          {title: 'TriBeCa Artsy Bachelor Pad', location: {lat: 40.7195264, lng: -74.0089934}},
          {title: 'Chinatown Homey Space', location: {lat: 40.7180628, lng: -73.9961237}}
        ];

Add a blank marker array globally (__outside of initMap() function!__).

    var markers = [];

Then, inside `initMap()`:

        var largeInfowindow = new google.maps.InfoWindow();
        var bounds = new google.maps.LatLngBounds();

        // Loop throug locations array in order to create one marker per location (markers array).
        for (var i = 0; i < locations.length; i++) {
            // Get the position from the location array.
            var position = locations[i].location;
            var title = locations[i].title;
            // Create a marker per location, and put into markers array.
            var marker = new google.maps.Marker({
                map: map,
                position: position,
                title: title,
                animation: google.maps.Animation.DROP,
                id: i
            });
            // Push the newly created marker(s) to our array of markers.
            markers.push(marker);
            // Create an onclick event to open an infowindow at each marker (so still in loop).
            marker.addListener('click', function() {
                populateInfoWindow(this, largeInfowindow); // Open 'this' (marker that was clicked), and populate with infowindow.
            });
            
            // As we may have listings that are outside the initial zoom area, we want to be able to extend the boundaries to fit everything
            bounds.extend(markers[i].position); // Extend the boundaries of the map for each marker
          }

            map.fitBounds(bounds); // Tell map to fit itself to bounds


      // Every time marker is clicked, this populate info window function is called:
      function populateInfoWindow(marker, infowindow) {
        // Check to make sure the infowindow is not already opened on this marker.
        if (infowindow.marker != marker) {
          infowindow.marker = marker;
          infowindow.setContent('<div>' + marker.title + '</div>'); // Set content
          infowindow.open(map, marker); // Open window on marker
          // Make sure the marker property is cleared if the infowindow is closed.
          infowindow.addListener('closeclick',function(){
            infowindow.setMarker = null;
          });
        }
      }

What if we don't want all the markers to show right away? What if we want them to become visible on the click of a button? First create two buttons.


    <div>
        <input id="show-listings" type="button" value="Show Listings">
        <input id="hide-listings" type="button" value="Hide Listings">
    </div>

We will make an event listener for each button. Inside `initMap()`:


    document.getElementById('show-listings').addEventListener('click', showListings); // Clicking show-listings button calls showListings function
    document.getElementById('hide-listings').addEventListener('click', hideListings); // Clicking hide-listings button calls hideListings function
    
What we then change in the code above, is that we 1) don't set the map parameter on those markers right away and we 2) won't extend the bounds of the map just yet. We move these things to out `showListings` function:


    // This function will loop through the markers array and display them all.
    function showListings() {
      var bounds = new google.maps.LatLngBounds();
      // Extend the boundaries of the map for each marker and display the marker
      for (var i = 0; i < markers.length; i++) {
        markers[i].setMap(map); // Set the map to map on each of the markers
        bounds.extend(markers[i].position); // Extend bounds of map to fit each of the markers
      }
      map.fitBounds(bounds);
    }

Conversely:


    function hideListings() {
      for (var i = 0; i < markers.length; i++) {
        markers[i].setMap(null); // Sets map to null on each marker (doesn't delete, just hides)
      }
    }

---

To get the latlng: use `marker.position`.

---

##### Adding some style

Things we can change: features (land, water, roads, points of interests and their labels, ...).

In `initMap()`, create styles array. Styled maps use concepts to apply colors and changes to a map, map features (geographic elements that can be targeted), elements (what about the feature you want to change), stylers (visibility properties that can be applied to map features, like color, hue or weight). 

---

You can also use styling starters that are freely available online! Just google Google Maps API Styles.

---


    var styles = [
          {
            featureType: 'water',
            stylers: [
              { color: '#19a0d8' }
            ]
          },{
            featureType: 'administrative',
            elementType: 'labels.text.stroke',
            stylers: [
              { color: '#ffffff' },
              { weight: 6 }
            ]
          },{
            featureType: 'administrative',
            elem ...
          }
        ];

Then, in map object, add property `styles: styles`, in addition to zoom and center. You can also add `mapTypeControl: false` which allows user to change map type to road, terrain, satellite, etc. (`false` _disables_ that feature).

##### Custom map types

See [this link](https://developers.google.com/maps/documentation/javascript/examples/maptype-styled-simple) for an example on how to add (optional) custom map types. For style documentation, see [this link](https://developers.google.com/maps/documentation/javascript/reference/3/map#MapTypeStyle).

##### Google street view

Important aspects: what place we are looking at and point of view: from east or west (heading), from down or up (pitch).

These things need to be defined dynamically for each of our points.

Go back to `populateInfoWindow()` in code. It needs to do more than just create a string in the window. We first create a `streetViewService` object inside the function. This needs to get the panorama image based on the closest location to the marker. And it needs to find out which way to point the camera, heading and pitch.


    var streetViewService = new. google.maps.StreetViewService();
    var radius = 50; // Radius to look for StreetView image within (in case there is no image of exact location)

We use the following function and pass in position of marker, radius and call our getStreetView function (see below).


    streetViewService.getPanoramaByLocation(marker.position, radius, getStreetView);
    
    function getStreetView(data, status) {
        if (status == google.maps.StreetViewStatus.OK) {
              var nearStreetViewLocation = data.location.latLng; // Take nearby streetview location
              // Compute heading based on location of nearest streetview and location of marker
              var heading = google.maps.geometry.spherical.computeHeading(
                nearStreetViewLocation, marker.position);
                infowindow.setContent('<div>' + marker.title + '</div><div id="pano"></div>');
            var panoramaOptions = {
                position: nearStreetViewLocation,
                pov: {
                    heading: heading, // Heading we just computed
                    pitch: 30 // 30 means we look slightly up
                }
            };
            // Create that object, put it inside infowindow at the div with id of pano
            var panorama = new google.maps.StreetViewPanorama(
                document.getElementById('pano'), panoramaOptions);
        } else { // If no image is found, then put that info in the window
              infowindow.setContent('<div>' + marker.title + '</div>' +
                '<div>No Street View Found</div>');
        }
    }

__As we use the library, we have to define `libraries=geometry` in the `src` attribute!__ `src="https://maps.googleapis.com/maps/api/js?key=MYAPIKEY&libraries=geometry&v=3&callback=initMap"`.

Another library is the visualization library (for e.g. heat maps). `src="https://maps.googleapis.com/maps/api/js?key=MYAPIKEY&libraries=visualizations&v=3&callback=initMap"`.

If you want to use the __StreetView functionality without a map__, use URL as image and pass in parameters location, heading, pitch, size. Use in any image element. Similarly, if you want to display simple __non effective map__, no need for full JS API, just use static maps API (required parameters: center, zoom, key, size).

Another library is `drawing` (`src="https://maps.googleapis.com/maps/api/js?key=MYAPIKEY&libraries=drawing&v=3&callback=initMap"`). To use this library and enable drawing, tell the map we plan to draw on it (in `initMap()`):


    var drawingManager = new google.maps.drawing.DrawingManager({
        drawingMode: google.maps.drawing.OverlayType.POLYGON, // Default drawing mode (other: rectangle, circle, polyline, marker)
        drawingControl: true,
        drawingControlOptions: {
            position: google.maps.ControlPosition.TOP_LEFT,
            drawingModes: [ // Polygon is specified as ONLY drawing mode
                google.maps.drawing.OverlayType.POLYGON
            ]
        }
    });

Then, create a HTML button to allow user to toggle drawing tools, and an event listener in JS file:


    <span class="text"> Draw a shape to search within it for homes!</span>
    <input id="toggle-drawing"  type="button" value="Drawing Tools">
    
    document.getElementById('toggle-drawing').addEventListener('click', function() {
        toggleDrawing(drawingManager);
    });
    
    // Where ...
    
    // This shows and hides (respectively) the drawing options.
        function toggleDrawing(drawingManager) { // When user clicks on toggle drawing...
            if (drawingManager.map) { ...check map property on drawingManager: if it's map...
                drawingManager.setMap(null); ...set it to null (hide drawing manager)
                // In case the user drew anything and turns off drawing tools, get rid of the polygon (but keep markers)
            if (polygon !== null) {
                polygon.setMap(null);
            }
            } else {
                drawingManager.setMap(map); // Set to map (show drawing manager)
            }
        }

Now we can draw, but how do we search within it? We need an event listener so that when a polygon is drawn, we capture those points and use them.

To ensure only one polygon is rendered, create a global variable (so, outside of `initMap()`):


    var polygon = null;

Then, inside `initMap()`, so that when polygon is complete, we iterate through markers array, show all of the ones that are within:


    drawingManager.addListener('overlaycomplete', function(event) {
        // First, check if there is an existing polygon.
        // If there is, get rid of it and remove the markers
        if (polygon) {
            polygon.setMap(null);
            hideListings(markers);
        }
        // Switching the drawing mode to the HAND (i.e., no longer drawing).
        drawingManager.setDrawingMode(null); // Also so that user can click on marker
        // Creating a new editable polygon from the overlay.
        polygon = event.overlay; // Capture overlay that was drawn
        polygon.setEditable(true); // We want polygon to be editable
        // Searching within the polygon.
        searchWithinPolygon();
        // Make sure the search is re-done if the poly is changed.
        polygon.getPath().addListener('set_at', searchWithinPolygon); // EL on polygon itself, checking for changes and re-executing search
        polygon.getPath().addListener('insert_at', searchWithinPolygon);
    });
    
    // This function hides all markers outside the polygon, and shows only the ones within it. This is so that the user can specify an exact area of search.
    function searchWithinPolygon() {
        for (var i = 0; i < markers.length; i++) {
            if (google.maps.geometry.poly.containsLocation(markers[i].position, polygon)) {
                markers[i].setMap(map); // If it does match, we set map property to map on each marker, which shows it.
            } else {
                markers[i].setMap(null); // If not, we set it to null, which hides it.
            }
        }
    }

---

Extra: if you want to calculate the area within a polygon and alert the user about it, use:


    var area = google.maps.geometry.spherical.computeArea(polygon.getPath());
        window.alert(area + " SQUARE METERS");
    });

### Geo coding (place > latlng)

Can be server side (no user input needed, returns JSON/XML), e.g. as part of process ran in script, or client side (no data yet, user input needed), as part of user facing code.

##### Interpreting results of geocoding web service

We can make a request through typing in our browser, e.g.: `https://maps.googleapis.com/maps/api/geocode/json?address=775+Park+Avenue,+New+York,+NY&key=YOURAPIKEY` (we can choose either json or xml). For reverse geocoding, we'd provide the latlng instead of the address (`https://maps.googleapis.com/maps/api/geocode/json?latlng=33.1262476,-117.3115765&key=YOURAPIKEY`). 

`address_components` has information broken down such as street, town, neighborhood, country, state, etc. This is interesting if we'd do reverse geocoding, where we'd have latlng but not the exact address.

We also get `formatted_address` that we can use on its own. 

`geometry` amongst others contains the latlng of the actual location (`location`) and the location type (`location_type`). 

`place_id` is an unique identifier for any place ranging from a whole country to a single address. This can be used in conjunction with the Places API.

##### Incorporating web service into app

Since we will need user input, we use client side.

__Prompt user to focus on specific area__: 

Add text input field and zoom button in HTML.


    <input id="zoom-to-area-text" type="text" placeholder="Enter your favorite area!">
    <input id="zoom-to-area" type="button" value="Zoom">

Then, in `initMap()`:

    document.getElementById('zoom-to-area').addEventListener('click', function() { // When button is clicked ...
        zoomToArea(); // ... call function
    });

In which the function is used to take user entered address, geocode it to get latlng, and center map on that latlng and zoom in.

    function zoomToArea() {
        var geocoder = new google.maps.Geocoder(); // Create new geocoder instance
        var address = document.getElementById('zoom-to-area-text').value; // Capture address or place
        // Make sure the address isn't blank.
        if (address == '') { // Make sure it's not blank
            window.alert('You must enter an area, or address.');
        } else {
          geocoder.geocode( // Geocode the address
            { address: address,
                componentRestrictions: {locality: 'New York'} // Add restriction: address must be within New York
            }, function(results, status) {
                if (status == google.maps.GeocoderStatus.OK) { // Check whether result is OK
                    map.setCenter(results[0].geometry.location); // Use resulting latlng to recenter ... *
                    map.setZoom(15); // ... and zoom
                } else { // If results were not OK ...
                    window.alert('We could not find that location - try entering a more specific place.'); // ... alert
                }
            });
        }
    }

[*] _Most of the time, we get more than one result from a geocoding response. We usually take the 0th option in the array of responses._

##### Elevation

`https://maps.googleapis.com/maps/api/elevation/json?locations=33.1262476,-117.3115765&key=YOURAPIKEY` HTTP request gives us elevation information.

##### Distance matrix

`https://maps.googleapis.com/maps/api/distancematrix/json?origins=New+York,+NY&destinations=San+Francisco&key=YOURAPIKEY` HTTP request computes travel distance and journey duration between multiple origins and destinations, given a mode of travel (needs `key` and at least one `destination` and `origin` pair, which together are called an `element` in the results). _Distance value defaults to meters, duration value defaults to seconds, transport defaults to driving._

Optional parameters in HTTP request: `mode=bicycling` (`/driving/walking/transit`, for transit we can specify modes with `transit_mode=` such as `rail, bus, subway, ...`), `avoid=highways`. There's many more parameters!

__Incorporate this into your app__:


In HTML:


        <div>
          <span class="text"> Within </span>
          <select id="max-duration">
            <option value="10">10 min</option>
            <option value="15">15 min</option>
            <option value="30">30 min</option>
            <option value="60">1 hour</option>
          </select>
          <select id="mode">
            <option value="DRIVING">drive</option>
            <option value="WALKING">walk</option>
            <option value="BICYCLING">bike</option>
            <option value="TRANSIT">transit ride</option>
          </select>
          <span class="text">of</span>
          <input id="search-within-time-text" type="text" placeholder="Ex: Google Office NYC or 75 9th Ave, New York, NY">
          <input id="search-within-time" type="button" value="Go">
        </div>

Then, as usual, an event listener:


    document.getElementById('search-within-time').addEventListener('click', function() {
        searchWithinTime();
    });

And associated function that uses DistanceMatrixService to calculate distances and travel duration between markers and entered location:


    function searchWithinTime() {
        var distanceMatrixService = new google.maps.DistanceMatrixService; // Initialize the distance matrix service.
        var address = document.getElementById('search-within-time-text').value; // Capture address
        // Check to make sure the place entered isn't blank.
        if (address == '') {
            window.alert('You must enter an address.');
        } else {
            hideListings();
            var origins = []; // Create origins array from list of markers
            for (var i = 0; i < markers.length; i++) {
                origins[i] = markers[i].position;
            }
            var destination = address; // Use user entered address as destination
            var mode = document.getElementById('mode').value; // Capture travel mode
          // Now that both the origins and destination are defined, get all the info for the distances between them.
            distanceMatrixService.getDistanceMatrix({ // Call function
                origins: origins, // Pass in origins
                destinations: [destination], // Pass in single destination
                travelMode: google.maps.TravelMode[mode], // Pass in travel mode
                unitSystem: google.maps.UnitSystem.IMPERIAL, // Specify unit to be imperial
            }, function(response, status) {
                if (status !== google.maps.DistanceMatrixStatus.OK) { // Check if status of response is OK
                    window.alert('Error was: ' + status); // More specific error message than in previous function!
                } else {
                    displayMarkersWithinTime(response); // Parse through response to get useful data (see below)
                }
            });
        }
    }

The `displayMarkersWithinTime()` is a new function:


    // Go through each of the results, and, if distance is LESS than value in picker, show it on the map.
    function displayMarkersWithinTime(response) {
        var maxDuration = document.getElementById('max-duration').value; // Capture user entered max duration in minutes
        var origins = response.originAddresses; // Recapture origins and destination from response
        var destinations = response.destinationAddresses;
        // Parse through the results, and get the distance and duration of each.
        // Because there might be  multiple origins and destinations we have a nested loop
        // Then, make sure at least 1 result was found.
        var atLeastOne = false;
        for (var i = 0; i < origins.length; i++) { // Nested loop to create one element per origin and destination pair
            var results = response.rows[i].elements;
            for (var j = 0; j < results.length; j++) {
                var element = results[j]; // Element will have distance and duration from A to B
                if (element.status === "OK") {
                    var distanceText = element.distance.text; // Distance is returned in feet, but the TEXT is in miles. If we wanted to switch the function to show markers within a user-entered DISTANCE, we would need the value for distance, but for now we only need the text. We want both this and duration in text form as we will display it to users.
                    var duration = element.duration.value / 60; // Duration value is given in seconds so we make it MINUTES. We need value here because we will compare it to maximum value user entered.
                    var durationText = element.duration.text; // We need both the value and the text.
                    if (duration <= maxDuration) { // If duration is within maximum value entered by user ...
                        markers[i].setMap(map); // ... display marker on map
                        atLeastOne = true; // If there are no markers within area, we want to let user know
                        var infowindow = new google.maps.InfoWindow({ // For each marker that appears, create a mini infowindow to open immediately ...
                            content: durationText + ' away, ' + distanceText // ... with Duration and Distance
                        });
                        infowindow.open(map, markers[i]);

                        markers[i].infowindow = infowindow;
                        google.maps.event.addListener(markers[i], 'click', function() { // Add this on each marker so that if user clicks on it, little info window is closed and make room for big one that has panorama (ACTUALLY LOOKS LIKE PANORAMA WINDOW DOESN'T WORK)
                            this.infowindow.close();
                        });
                    }
                }
            }
        }
        if (!atLeastOne) {
            window.alert('We could not find any locations within that distance!');
        }
    }

##### Directions API

Instead of just time and region, this API gives step by step directions from point A to B and even C through Z if needed. Inputs, amongst others: travel `mode`, `multiple transit modes`, `transit routing preferences`, `restrictions`, `waypoints` or `via` (to specifiy additional destination or pass-through: __divide multiple waypoints using `|`__). If you specify `optimize:true` in your waypoints, the API will do the planning for you and make the most efficient route past all waypoints. Origins, destinations and waypoints are defined as strings or as latlng coordinates. The API can return multi-port directions using a series of waypoints or via points. _Waypoints are NOT supported for the transit travel mode!_

`https://maps.googleapis.com/maps/api/directions/json?origin=New+York,+NY&destination=San+Francisco&key=YOURAPIKEY`: single origin and destination pair (either latlng or string). 

In output, check `routes` (divided into `legs`).

__Using it in the app__:

What if we want to add a button inside info window on marker inside the listings in a specific area, that shows route?

First, add button 'view route' inside info window, so that in total this part looks like:


    var infowindow = new google.maps.InfoWindow({
        content: durationText + ' away, ' + distanceText +
            '<div><input type=\"button\" value=\"View Route\" onclick =' +
            '\"displayDirections(&quot;' + origins[i] + '&quot;);\"></input></div>' // As we could have multiple listings falling within commute limit, we pass in that origin (listing address) for each button we make
    });
    // Destination we will use is user entered address

Then, the function:

    
    function displayDirections(origin) {
        hideListings();
        var directionsService = new google.maps.DirectionsService; // Initialize new direction service instance
        var destinationAddress = document.getElementById('search-within-time-text').value; // Get the destination address again from the user entered value.
        var mode = document.getElementById('mode').value; // Get mode again from the user entered value.
        directionsService.route({ // Now we calculate the route
            origin: origin, // The origin is the passed in marker's position
            destination: destinationAddress, // The destination is user entered address
            travelMode: google.maps.TravelMode[mode]
        }, function(response, status) { // When we get back response ...
            if (status === google.maps.DirectionsStatus.OK) { // ... we make sure status is OK ...
                var directionsDisplay = new google.maps.DirectionsRenderer({ // ... and create new directions renderer (takes care of displaying all information)
                    map: map, // Render on our map
                    directions: response, // Get directions from route response
                    draggable: true, // Want route to be draggable
                    polylineOptions: {
                        strokeColor: 'green' // We want to display resulting polyline in green
                    }
                });
            } else {
                window.alert('Directions request failed due to ' + status);
            }
        });
    }

In the directions renderer, we could also display the step by step directions to the user. For that, we need to specify HTML div to put route in by setting `panel` parameter in the directions renderer.

##### Roads API

Only work with Premium Plan. See lessons.

##### Places API

Search for places.

For example, __update text input areas to use autocomplete__:

First, include other library in the URL that also specifies `geometry` and `drawing`: `places`. Then, in `initMap()`, initialize two new instances and bind them to the input boxes:


    var timeAutocomplete = new google.maps.places.Autocomplete( // For use in search within time entry box.
        document.getElementById('search-within-time-text'));
    var zoomAutocomplete = new google.maps.places.Autocomplete( // For use in geocoder entry box.
            document.getElementById('zoom-to-area-text'));

These autocompleters will predict what user is typing with each keystroke and supply most likely options in pick list. We can add more options to this, such as bias towards certain area, type for type of results and component restriction to restrict results to within certain country. E.g. we could add, on a new line, `zoomAutocomplete.bindTo('bounds', map);`.

__Find nearby places of interest within the map.__ What if we want to add a search box? This is different from Autocomplete, as it provides an extended list of predictions, which can include places as defined by Google Places API and search queries such as 'pizza near Google office'. We, however, can't restrict as much as Autocomplete.

First, add new section to HTML.


    <div>
        <span class="text">Search for nearby places</span>
        <input id="places-search" type="text" placeholder="Ex: Pizza delivery in NYC">
        <input id="go-places" type="button" value="Go">
    </div>

Then, create new SearchBox instance in `initMap()`:


    var searchBox = new google.maps.places.SearchBox(
        document.getElementById('places-search')); // And bind new instance to text input we just created
        searchBox.setBounds(map.getBounds()); // Bias the searchbox to within the bounds of the map

Then, create two event listeners:


    // Listen for the event fired when the user selects a prediction from the picklist and retrieve more details for that place.
    searchBox.addListener('places_changed', function() { // When user selects option from pick list (places_changed event)
        searchBoxPlaces(this);
    });

    // Listen for the event fired when the user selects a prediction and clicks "go" more details for that place.
    document.getElementById('go-places').addEventListener('click', textSearchPlaces); // If user types in something and clicks 'go' without selecting suggestion

Then, create global `var placeMarkers = [];` to use in both functions, so we can control them separately from listing markers and so that we only have one set of markers on our map at a time.

We now change `hideMarkers()` to make it more generic by adding `markers` as an argument. Now, it can be used anytime to hide any array of markers on the map. Don't forget to add markers as argument whenever we invoke(d) this function!

    function hideMarkers(markers) {
        for (var i = 0; i < markers.length; i++) {
            markers[i].setMap(null);
        }
    }

Then, function that executes when user chooses picklist value from SearchBox:


    function searchBoxPlaces(searchBox) { // This function will do a nearby search using the selected query string or place
        hideMarkers(placeMarkers); // Hide all markers we had on map from last search
        var places = searchBox.getPlaces(); // Then, find all places that match query
        // For each place, get the icon, name and location.
        createMarkersForPlaces(places); // If we do find places, run this function (we will also need it for textSearchPlaces, hence defining it as separate function)
        if (places.length == 0) { // If no places were found, alert
            window.alert('We did not find any places matching that search!');
        }
    }

Then,


    function textSearchPlaces() { // This function if user instead of picking from pick list, enters search query and clicks 'go'
        var bounds = map.getBounds(); // Capture bounds of map
        hideMarkers(placeMarkers);
        var placesService = new google.maps.places.PlacesService(map);
        placesService.textSearch({
            query: document.getElementById('places-search').value, // Pass in user entered query
            bounds: bounds
        }, function(results, status) { // Results is places array
            if (status === google.maps.places.PlacesServiceStatus.OK) {
                createMarkersForPlaces(results); // If OK, pass in places array here
            }
        });
    }

So, for both functions above we get an array of places back. We iterate through them and create marker per place!


    // This function creates markers for each place found in either places search.
    function createMarkersForPlaces(places) {
        var bounds = new google.maps.LatLngBounds();
        for (var i = 0; i < places.length; i++) { // For each place, we capture bunch of info about the place
            var place = places[i];
            var icon = { // Specify what icon looks like that we pass in as Marker property value below
                url: place.icon,
                size: new google.maps.Size(35, 35),
                origin: new google.maps.Point(0, 0),
                anchor: new google.maps.Point(15, 34),
                scaledSize: new google.maps.Size(25, 25)
            };
            // Create a marker for each place.
            var marker = new google.maps.Marker({
                map: map,
                icon: icon,
                title: place.name,
                position: place.geometry.location,
                id: place.id // Used later to get more details if user clicks on marker
            });
            // If a marker is clicked, do a place details search on it in the next function.
            marker.addListener('click', function() {
                getPlacesDetails(this, place); // This is marker
            });
            placeMarkers.push(marker); // Push each marker into placeMarkers array
            if (place.geometry.viewport) { // Adjust bounds of map to appropriately fit all markers
                // Only geocodes have viewport.
                bounds.union(place.geometry.viewport);
            } else {
                bounds.extend(place.geometry.location);
            }
        }
        map.fitBounds(bounds);
    }

So, how to get details of these places? We use `placeId`. Check it out: `https://maps.googleapis.com/maps/api/place/details/json?placeid=ChIJN1t_tDeuEmsRUsoyG83frY4&key=YOURAPIKEY`. We can add onClick to markers that'll display details about each marker.

We now add to our `createMarkersForPlaces()`.


    function createMarkersForPlaces(places) {
        var bounds = new google.maps.LatLngBounds();
        for (var i = 0; i < places.length; i++) { 
            var place = places[i];
            var icon = { 
                url: place.icon,
                size: new google.maps.Size(35, 35),
                origin: new google.maps.Point(0, 0),
                anchor: new google.maps.Point(15, 34),
                scaledSize: new google.maps.Size(25, 25)
            };
            // Create a marker for each place.
            var marker = new google.maps.Marker({
                map: map,
                icon: icon,
                title: place.name,
                position: place.geometry.location,
                id: place.id 
            });
            var placeInfoWindow = new google.maps.InfoWindow(); // ADD SINGLE INFO WINDOW THAT WILL SHARE BETWEEN DIFFERENT PLACE MARKERS THAT WE ONLY HAVE ONE SET OF DETAILS OPEN AT ONCE
            marker.addListener('click', function() { // CHANGE THIS EVENT LISTENER INTO THE FOLLOWING
                if (placeInfoWindow.marker == this) {
                    console.log("This infowindow already is on this marker!");
                } else {
                    getPlacesDetails(this, placeInfoWindow);
                }
            });
            placeMarkers.push(marker); 
            if (place.geometry.viewport) { 
                // Only geocodes have viewport.
                bounds.union(place.geometry.viewport);
            } else {
                bounds.extend(place.geometry.location);
            }
        }
        map.fitBounds(bounds);
    }

With the `getPlacesDetails()`:


    // Most detailed so only executed when marker is selected.
    function getPlacesDetails(marker, infowindow) {
        var service = new google.maps.places.PlacesService(map);
        service.getDetails({
            placeId: marker.id // We set placeId as marker.id before
        }, function(place, status) { // Get back results
            if (status === google.maps.places.PlacesServiceStatus.OK) { // Status OK? Parse through all data from request
                // Set the marker property on this infowindow so it isn't created again.
                infowindow.marker = marker;
                var innerHTML = '<div>';
                if (place.name) {
                    innerHTML += '<strong>' + place.name + '</strong>';
                }
                if (place.formatted_address) {
                    innerHTML += '<br>' + place.formatted_address;
                }
                if (place.formatted_phone_number) {
                    innerHTML += '<br>' + place.formatted_phone_number;
                }
                if (place.opening_hours) {
                    innerHTML += '<br><br><strong>Hours:</strong><br>' +
                        place.opening_hours.weekday_text[0] + '<br>' +
                        place.opening_hours.weekday_text[1] + '<br>' +
                        place.opening_hours.weekday_text[2] + '<br>' +
                        place.opening_hours.weekday_text[3] + '<br>' +
                        place.opening_hours.weekday_text[4] + '<br>' +
                        place.opening_hours.weekday_text[5] + '<br>' +
                        place.opening_hours.weekday_text[6];
                }
                if (place.photos) {
                    innerHTML += '<br><br><img src="' + place.photos[0].getUrl({ // We include first photo ref we get
                        maxHeight: 100,
                        maxWidth: 200
                    }) + '">';
                }
                innerHTML += '</div>';
                infowindow.setContent(innerHTML);
                infowindow.open(map, marker);
                // Make sure the marker property is cleared if the infowindow is closed.
                infowindow.addListener('closeclick', function() {
                    infowindow.marker = null;
                });
            }
        });
    }

There are some specific details about Places API requests. Check out `Nearby Search` (formerly Place Search), `Text Search` and `Radar Search`. 

##### Timezone API

Find timezone:

`https://maps.googleapis.com/maps/api/timezone/json?location=51.5073509,-0.1277582999&timestamp=1459468800&key=YOURAPIKEY` where timestamp is convertable online.

##### Geolocation API

For devices that don't have locations built in natively. 

---

### Random lost notes

##### Arrow functions

ES5


    var multiply = function (x, y) {
        return x * y
    };
    
    // or
    
    var splitter = function splitterOne(p) {
        return p.split('')
    };

Es6


    const multiply = (x, y) => {
        return x * y
    };
    // ... where the curly brackets are not required.
    
    // or
    
    const splitter = p => p.split('')

##### React

MAIN


    import React
    import Component
    
    class App extends Component {
        state = { ... }
        
        functionOne = (arg) => { ... }
        
        render() { // Only used for displaying content
            return (
                // HTML referring back to functionOne
            )
        }
    }
    
    export default App;

Sometimes, instead, write:

    constructor(props) {
        super(props)
        this.state = { ... }
    }

COMPONENT

    
    import React
    import library
    
    class ComponentName extends Component {
        static propTypes = { ... }
        
        state = { ... }
        
        functionTwo = (arg) => { ... }
        
        render() {
            return(
                // HTML referring back to functionTwo
            )
        }
    }
    
    export default ComponentName;

__Single page application:__ Web apps that load a single HTML page and dynamically update that page as the user interacts with the app. Much of the work happens on the client side, in JavaScript.
