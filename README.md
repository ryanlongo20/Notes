# Notes

- [Notes](#notes)
- [JS](#js)
  - [Fundamentals Part 5](#fundamentals-part-5)
    - [Objects](#objects)
      - [Literal and Properties](#literal-and-properties)
      - [Dot Notation](#dot-notation)
      - [Square Brackets](#square-brackets)
      - [Computed Properties](#computed-properties)
      - [Property Value Shorthand](#property-value-shorthand)
      - [Property Names Limitations](#property-names-limitations)
      - ["in" Operator](#in-operator)
      - ["for...in" Loop](#forin-loop)
      - [Some problems](#some-problems)
        - [Hello, object](#hello-object)
    - [Arrays](#arrays)
  - [this or that?](#this-or-that)
    - [Misconceptions](#misconceptions)
  - [this in more detail](#this-in-more-detail)
    - [Default Binding](#default-binding)
    - [Implicit Binding](#implicit-binding)
  - [Objects and Object Constructors](#objects-and-object-constructors)
    - [Object as a Design Pattern](#object-as-a-design-pattern)
    - [Object Constructors](#object-constructors)
    - [The Prototype](#the-prototype)
    - [Constructor](#constructor)
    - [Recommended Method for Prototypal Inheritance](#recommended-method-for-prototypal-inheritance)
- [HTML](#html)
  - [SVG](#svg)
    - [Introduction](#introduction)
    - [What are they?](#what-are-they)
    - [Drawbacks](#drawbacks)
    - [Anatomy](#anatomy)
    - [Embedding SVGs](#embedding-svgs)
  - [Tables](#tables)
    - [Captions](#captions)
    - [tfoot, tbody, thead](#tfoot-tbody-thead)
  - [Form Basics](#form-basics)
    - [The Form Element](#the-form-element)
    - [The Input Element](#the-input-element)
    - [Labels](#labels)
    - [Placeholder Attribute](#placeholder-attribute)
    - [The name attribute](#the-name-attribute)
    - [Using Form Controls Outside of Forms](#using-form-controls-outside-of-forms)
    - [Type Attribute](#type-attribute)
    - [Selection Elements](#selection-elements)
      - [Select Dropdown](#select-dropdown)
      - [Radio Buttons](#radio-buttons)
      - [Checkboxes](#checkboxes)
    - [Buttons](#buttons)
  - [Form Validation](#form-validation)
    - [Types of validations](#types-of-validations)
- [CSS](#css)
  - [CSS Units](#css-units)
    - [Absolute units](#absolute-units)
    - [Relative Units](#relative-units)
      - [em and rem](#em-and-rem)
      - [Viewport Units](#viewport-units)
      - [Suggestions](#suggestions)
  - [More Text Styles](#more-text-styles)
    - [letter-spacing](#letter-spacing)
    - [line-height](#line-height)
    - [text-transform](#text-transform)
    - [text-shadow](#text-shadow)
  - [More CSS Properties](#more-css-properties)
    - [Background](#background)
    - [Border](#border)
    - [Box-shadow](#box-shadow)
    - [Overflow](#overflow)
  - [Advanced Selectors](#advanced-selectors)
    - [Parent and Sibling Combinators](#parent-and-sibling-combinators)
  - [Pseudo-selectors](#pseudo-selectors)
    - [Pseudo-classes](#pseudo-classes)
    - [Dynamic and User Action Pseudo-classes](#dynamic-and-user-action-pseudo-classes)
    - [Structural Pseudo-classes](#structural-pseudo-classes)
    - [Pseudo-Elements](#pseudo-elements)
    - [Attribute Selectors](#attribute-selectors)
  - [Positioning](#positioning)
    - [Static and Relative Positioning](#static-and-relative-positioning)
    - [Absolute Positioning](#absolute-positioning)
    - [Fixed Positioning](#fixed-positioning)
    - [Sticky Positioning](#sticky-positioning)
  - [CSS Functions](#css-functions)
    - [calc()](#calc)
    - [min()](#min)
    - [max ()](#max-)
    - [clamp()](#clamp)
  - [Custom Properties](#custom-properties)
    - [Using Customer Properties](#using-customer-properties)
    - [Fallback Values](#fallback-values)
    - [Scope](#scope)
    - [The :root selector](#the-root-selector)
    - [Media queries](#media-queries)
  - [Frameworks and Preprocessors](#frameworks-and-preprocessors)
    - [Disadvantages](#disadvantages)

# JS

## Fundamentals Part 5

### Objects
Objects are used to store keyed collections of complex data entities, created with figure brackets {...} with an optional list of *properties*. A property is a key-value pair where the **key** is a string and value can be anything.

```javascript
let user = new Object; // "object constructor" syntax
let user = {}; // "object literal" syntax
```

#### Literal and Properties

```javascript
let user = {     // an object
  name: "John",  // by key "name" value "John"
  age: 30        // by key "age" store value 30
};
```

1. First property has name "name" and value "John"
2. Second property has name "age" and value 30.

We can access property values by dot notation or square brackets, albeit some differences.

#### Dot Notation 

```javascript
alert(user.name) // John
alert(user.age) // 30
```

We can also add properties. 

```javascript
user.isAdmin = true
```

To remove, we can use the **delete** property.

```javascript
delete user.age;
```

We can use multiword property names, but they must be quoted:

```javascript
let user = {
  name: "John",
  age: 30,
  "likes birds": true , // multiword property name must be quoted
};
```

The last property in the list may also end in a comma, called a "trailing" comma.

#### Square Brackets

For these multiword properties, square brackets are needed.

```javascript 
user.likes birds = true; // syntax error as it looks for user.likes
alert(user["likes birds"]); // true

//delete 
delete user["likes birds"];
```
Square brackets provide a way to obtain the property name as the result of a variable expression:

```javascript
let key = "likes birds";

user[key] = true; //same as user["likes birds"] = true;
```

This allows for a lot of flexibility! Another example:

```javascript
let user = {
    name: "John",
    age: 30
};

let key = prompt("What do you want to know about the user?", "name");
t
//access by variable
alert ( user[key] ); // John if entered "name", would be 30 if enter "age"
```

We could not do dot notation in this instance.

#### Computed Properties

We can use square brackets in an object literal when creating an object. 

```javascript 
let fruit = prompt("Which fruit to buy?", "apple");

let bag = {
    [fruit]: 5, //name of property is taken from varuable fruit
};

alert ( bag.apple ) // bag will become {apple: 5}
```

The fruit variable acts as a placeholder for the prompt input from the user.

We can use more complex expressions as well:

```javascript 
let fruit = 'apple';
let bag = {
  [fruit + 'Computers']: 5 // bag.appleComputers = 5
};
```

#### Property Value Shorthand

Existing variables are often used as values for property names.

```javascript 
function makeUser(name, age) {
    return {
        name: name,
        age: age,
        // ..other properties
    };
}

let user = makeUser("John", 30);
alert(user.name); // John
alert(user.age); // 30
```

Instead of name:name, we can just do this:

```javascript 
function makeUser(name, age) {
    return {
        name, // same as name: name
        age,
    };
}
```

We can use normal properties and shorthands in the same object.

#### Property Names Limitations

There are no limitations on property names. Other types are converted to strings.

```javascript 
let obj = {
  0: "test" // same as "0": "test"
};

// both alerts access the same property (the number 0 is converted to string "0")
alert( obj["0"] ); // test
alert( obj[0] ); // test (same property)
```

#### "in" Operator

It's possible to access any property in JavaScript, so there will be no error if the property doesn't exist. This is where the special operator "in" is useful:

```javascript
let user = {name: "John", age: 30};

alert( "age" in user); // true, user.age exists
alert('dog' in user); //false, does not exist
```

Syntax is "key" in object

There are instances where an object property exists but stores undefined:

```javascript 
let obj = {
  test: undefined
};

alert( obj.test ); // it's undefined, so - no such property?

alert( "test" in obj ); // true, the property does exist!
```

#### "for...in" Loop

```javascript 
let user = {
  name: "John",
  age: 30,
  isAdmin: true
};

for (let key in user) {
    // keys
    alert( key ); // name, age, isAdmin
    alert ( user[key] ); // John, 30, true
}
```

#### Some problems

##### Hello, object

1. Create an empty object user.
2. Add the property name with value John
3. Add property surname with value Smith
4. Change value of the name to Pete
5. Remove property name from object
   hi
```javascript
let user = {};
user.name = "John";
user.surname = "Smith";
user.name = "Pete";
delete user.name;
```

### Arrays

## this or that?

The **this** keyword is one of the most confusing in JavaScript.

Here is an example of it's utility:

```javascript
function identity() {
  return this.name.toUpperCase();
}

function speak() {
  var greeting = "Hello, I'm " + identity.call( this );
  console.log( greeting );
}
var me = {
  name: "Kyle";
}

var you = {
  name: "Reader";
};


identity.call( me ); // KYLE
identity.call( you ); // READER

speak.call( me ); // Hello, I'm KYLE
speak.call( you ); // Hello, 
```

The code snippet allows us the **identity()** and **speak()** functions to be re-used against multiple context (**me** and **you**) objects, rather than needing a separate version of the function for each object.

We could've explicity passed in a context object to both **identity()** and **speak()**

```javascript
function identity(context){
  return context.name.toUpperCase();
}

function speak(context) {
  var greeting = "Hello, I'm" + identity( context )
}

identity( you ); // READER
speak( me ); // Hello, I'm KYLE

```

However, the **this** mechanism makes it more elegant to pass along an object reference, rather than explicity passing one.


### Misconceptions 

**this** does not refer to the function itself. There are some reasons to call a function from inside itself (recursion or having an event handler that can unbind itself when it is called), but **this** doesn't let a function get a reference to iself.

Considering this code, that keeps track of how many times a function(foo) was called

```javascript
function foo(num) {
	console.log( "foo: " + num );

	// keep track of how many times `foo` is called
	this.count++;
}

foo.count = 0;

var i;

for (i=0; i<10; i++) {
	if (i > 5) {
		foo( i );
	}
}
// foo: 6
// foo: 7
// foo: 8
// foo: 9

// how many times was `foo` called?
console.log( foo.count ); // 0 -- WTF?
```

foo.count is still 0, even though the four console.log statements indicate it was called 4 times.

However, this.count is not pointing at all to the function object, as the root objects are different.

## this in more detail

There are 4 rules when inspecting **this** call-site, which have an order of precedence

### Default Binding 

Consider the code: 

```javascript
function foo() {
  console.log( this. a)
}

var = 2;

foo(); // 2

```

Variables defined in the global scope like var a = 2 are synonoymous with global-object properties of the same name. They are not copies of each other, they are each other.

When **foo()** is called, **this.a** resolves to our global variable *a*. This is because the default binding for this applies to the function call, and so points **this** at the global object. 

### Implicit Binding

## Objects and Object Constructors

### Object as a Design Pattern

One of the easiest ways to organize your code is grouping things into objects. For example:

```javascript
const playerOneName = 'tim'
const playerTwoName = 'jenn'
const playerOneMarker = 'x'
const playerTwoMarker = 'o'

// example two
const playerOne = {
  name: 'tim',
  marker: 'x'
}

const playerTwo = {
  name: 'jenn',
  marker: '0'
}
```

This looks clean, but using objects is easier. For example:

```javascript
function printName(player){
  console.log(player.name)
}
```

We can't access any of the players names with this, we would have to print out the player's names individually.

That's not horrible, but what if we don't know the players name? Or if we are making something more complicated than a 2 player game? Using objects in this instance to keep track of our properties is the only way to go.

In that situation, manually typing out the contents of our objects isn't feasible either. This is where object constructors come in.

### Object Constructors

When we have a specific object we need to duplicate, we can use an object constructor.

```javascript
function Player(name, marker) {
  this.name = name
  this.marker = marker
}
```

and you can call this function with the keyword new

```javascript
const player = new Player('steve', 'X')
console.log(player.name)
```
rferffefr
You can add functions to the object as well.

```javascript
function Player(name, marker) {
  this.name = name
  this.marker = marker
  this.sayName = function() {
    console.log(name)
  }
} 

const player1 = new Player('steve', 'X')
const player2 = new Player('also steve', 'O')
player1.sayName() // logs 'steve'
player2.sayName() // logs 'also steve'
```

### The Prototype

All objects in JS have a **prototype**. The prototype is another object that the original object inherits from-the original object has access to all of its prototype's methods and properties.

If you're using constructors to make your objects it is best to define functions on the **prototype** of that object.  dfdf

There are two interrelated concepts with prototype in JS:

1. Every JS function has a prototype property, and you attach properties and methods on this prototype propetty when you want to implement inheritance. Prototypes are not accessible in a for/in loop. You add methods and properties on a function's prototype property to make those methods and properties available to instances of that function.

2. Second concept with prototype is the prototype attribute. It is a characteristic of the object; this characteristic tells us the object's "parent". An object's prototype attribute points to the object's "parent"-the object it inherited its properties from. The prototype attribute is referred to as the prototype object, and it is set automatically when you create a new object. 

### Constructor 

A constructor is a function used for initializing new objects, using the new keyword.

### Recommended Method for Prototypal Inheritance

The recommended way of setting the prototype of an object is **Object.create**, which returns a new object with the specified prototype and any properties you want to add.

```javascript 
function Student() {
}

Student.prototype.sayName = function() {
  console.log(this.name)
}

function EigthGrader(name) {
  this.name = name;
  this.grade = 8
}

EighthGrader.prototype = Object.create(Student.prototype)

const carl = new EighthGrader('carl')
carl.sayName() // console.logs 'carl'
carl.grade // 8
```

# HTML

## SVG

### Introduction

SVGs are a common image format of the web, and they scale to any size and retain their quality without an increased file size.

Often used for: 
1. Icons
2. Graphs/Charts
3. Large, simple images
4. Patterned backgrounds
5. Applying effects to other elements

### What are they?

"SVG" is "Scalable Vector Graphic". These are images designed by math rather than a grid of pixels. You have formulas for different shapes and lines that can scale to any size.

SVGs are defined using XML (Extensive markup language), an HTML-like syntax which is used for APIs, RSS, etc

SVGs being defined by XML makes it so the source-code is human readable, unlike a JPEG

### Drawbacks

-Inefficient at storing complex images

### Anatomy

Usually they are downloaded from an image editor that can create them (such as Figma)

1. xmlns - "XNL namespace". Specifies dialect of XML.
2. viewBox - defines bounds of SVG
3. class, id - same as HTML
4. elements such as circle rect path text are defined by SVG namespace.
5. Many SVG attributes like fill and stroke can be changed in CSS

### Embedding SVGs

You can place an SVG by either linking them or using them inline. Linking works the same as in HTML & CSS, but the contents of the SVG is not accessible from the webpage

Inlining helps you unlock all of SVGs potential, but adds some readability challenges.

## Tables

You can create a table with **<table></table>** tag. A **<th></th>**  tag is for the table headers, and **<tr>** is for table row, **<td>** is for table data cell

### Captions

Useful for blind users, implemented using **caption** tag

### tfoot, tbody, thead

These tags give the table more structural definition.

## Form Basics

Forms are your user's gateway into your backend, where they provide data to you.

### The Form Element

The form element is a container element like the div. It accepts an **action** attribute which takes a url value that tells the form where it should send its data to be processed.

Second is the **method** attribute which tells the browser which HTTP request method it should use to submit the form. GET and POST requests are two most common.

We use GET when we want to retrieve something from a server. 
POST is used when we want to change something on a server, for example, when a user makes an account or makes a payment on a website.

### The Input Element

Input element accepts a type attribute which tells the browser what type of data it should expect

### Labels

Labels are placed on inputs to inform users what type of data they are expected to enter.

Labels accept a **for** attribute, which associates it with a particular input. The input we want to associate with a label needs an **id** attribute with the same value as the label's **for** attribute

When a label is associated with an input and is clicked, it will focus the cursor on that input. 

### Placeholder Attribute

Placeholder attributes guide users on what to enter in an input. 

### The name attribute

The name attribute informs the backend what each piece of data represents. We attach a name attribute to our inputs. It serves as a reference to the data inputted into a form control after submitting it, it is like a variable name for an input. 

### Using Form Controls Outside of Forms

You can use any of the form controls HTML provides outside of the form element, even when you don't have a backend server.

You can manipulate data from form controls.

### Type Attribute

You have many different type attributes:

-email
-password
-number
-date
-text area (provides input box that spans multi line, accept rows and cols)

### Selection Elements

#### Select Dropdown

Select element renders a dropdown list where users can select an option. Any options we want to display within the select element are defined using option elements. All the options must have a **value** attribute, and this value will be sent to the server when the form is submitted. 

We can make one of our options be the default selection with the **selected** element.

We can also split the list of options into groups using the optgroup element, each optgroup taking a label attribute.

#### Radio Buttons

Allow us to create multiple options the user can choose one of. Type is "radio". Radio buttons can only select one if there name attribute is thee same, can also preselect a button using checked attribute.

#### Checkboxes

Similar to radio buttons, but allow multiple selections.

### Buttons 

Button element creates clickable buttons that user can interact with. Also accepts a type attribute to tell browser which kind of button we are dealing with. There are:

1. Submit Button (type="submit")
2. Reset Button (type = "reset"). Clears all data user entered into form
3. Generic Button  (type="button"). Used for submitting interactive UIs

## Form Validation

### Types of validations

1. Required: makes a field required
2. minlength: represents minimum amount of characters we want
3. maxlength: self explanatory lol
4. min validation: minimum number we want the form control to accept
5. max validation: also self explanatory
# CSS 

## CSS Units

### Absolute units
**px, in, cm**

### Relative Units

#### em and rem
**1em** is the font-size of an element (or the element's parent if you're using it to set font-size). So if an element's width is **4em**, the width is **64px**.

**1rem** is the **font-size** of the root element (either **:root** or **html**). rem is recommended over em to increase readability.

#### Viewport Units

**1vh** is equal to 1% of the viewport height and **1vw** is equal to 1% of the viewport width

#### Suggestions

Use rem for font-size and px for everything else.

## More Text Styles

### letter-spacing

Changes space between letters in a word.

### line-height

Line height adjusts the space between lines in wrapped text, can increase readability.

### text-transform 


Changes the case of the given text. Can use this to force your heading tags to be all uppercase, or to capitalize every word.

### text-shadow 

Adds a shadow around the text in the selected element.

## More CSS Properties

### Background

Background is a shorthand for 8 different background-related properties.
background-attachment
background-clip
background-color
background-image
background-origin
background-position
background-repeat
background-size

### Border 

Bordrer is a shorthand for color, style, and width. Border-radius allows you to set the radius for an element (useful for making rounded edges)

### Box-shadow

Adds shadow effect around element, creates a sense of depth on your page

### Overflow 

Can define what happens to an element when its content is too big to fit. Can add scrollbars to an element in a webpage

## Advanced Selectors

### Parent and Sibling Combinators 

1. (>) child combinator
2. (+) adjacent sibling combinator (selects sbiblings only next to our element)
3. (~) general sibling combinator (selects all siblings)

If we wanted to select child and grand-child divs inside of main, we write:

main div {

}

If we want to select only the child or grand-child divs inside of main, we write:

main > div {   <-- selects child element one indentation down

}

main > div > div {   <-- selects grand-child two indentations down

}

## Pseudo-selectors

### Pseudo-classes

Some pseudo-classes are based on their position or structure within the HTML, some are based on the state of a particular element, or how the element is being interacted with

They share the same specificity as regular classes 

### Dynamic and User Action Pseudo-classes

:focus applies to an element that is currently selected either with cursor or keyboard

:hover affects anything under the mous pointer

:active applies to elements that are currently being clicked

### Structural Pseudo-classes

Structural Pseudo-classes are a powerful way to select elements based on their position within the DOM

:root is a special class that represents the very top level of your document, usually the place where you place your global CSS rules, such as custom properties and CSS variables

:first-child and :last-child will match elements that are the first or last sibling 

:empty matches elements that have no children at all

:only-child matches elements that have no siblings

:nth-child has many use cases: can select even (:nth-child(even)), 5th el (:nth-child(5)), every third el (:nth-child(3n))


### Pseudo-Elements

::marker allows you to customize styling of li elements bullets or numbers

::selection allows you to change highlighting when a user selects text on the page

::before and ::after allow us to add extra elements onto the page with CSS, instead of HTML. Using it to decorate text in various ways is one common use case.

### Attribute Selectors


## Positioning

### Static and Relative Positioning

Default positioning mode is position: static. Relative is the same as static, but properties top, right, bottom, and left displace the element relative to its normal position in the normal flow of the document

The element is positioned according to the normal flow of the document in static.

### Absolute Positioning

position:: absolute allows you to position something at an exact point on the screen without disturbing the other elements around it

It removes that element from the normal document flow while being positioned relative to an ancestor element.

In simpler terms: elements that are removed from the normal flow of the document don't affect other elements and are also not affected by other elements

### Fixed Positioning

Fixed elements are removed from the normal flow of the document and are positioned relative to the viewport. You use top, right, bottom, and left properties to position it, and it will stay there as the user scrolls. Useful for floating chat buttons.

### Sticky Positioning

Sticky Elements will act like normal elements until you scroll past them, then they start behaving like fixed elements.

Useful for section headings. 

## CSS Functions

### calc()

Used for mixing units

ex:

--header: 3rem;
--footer: 40px;
--main: calc(100vh - calc(var(--header) + var(--footer)));

To put it another way: main = 100vh - (header + footer). calc() handles the math for us

### min()

Ex: width: min(150px, 100%);
-If there are 150px available to the image, it will take up all 150px. If there are not 150px available, the image will switch to 100% of the parent's width

### max ()

Works the same way as min, only in reverse. It will select the largest possible value from within the paranthesis. max() ensures a minimum allowed value for a property

### clamp()

Takes 3 values: smallest value, ideal value, largest value

## Custom Properties

CSS variables allow us to reference a css value however many times we want throughout a file

### Using Customer Properties 

.error-modal {
  --color-error-text: red;
  --modal-border: 1px solid black;
  --modal-font-size: calc(2rem + 5vw);

  color: var(--color-error-text);
  border: var(--modal-border);
  font-size: var(--modal-font-size);
}

We first declare out custom property with a double hyphen followed by a case sensitive property name (color-error-text. Then we store any valid CSSS value in our newly declared custom property. When we want to access our property, we use the var() function 

### Fallback Values

var() function accepts two parameters: a custom property we want to assign and a fallback



### Scope 

The scope of a custom property is determined by the selector. 

.cool-div {
  --main-bg: red;
}

.cool-paragraph {
  background-color: var(--main-bg);
}

.boring-paragraph {
  background-color: var(--main-bg);
}

If you had a div with class "one" with a child with class "two", which had two grandchildren with class "three" and "four", and the following CSS:

.two {
  --test: 10px;
}

.three {
  --test: 2em;
}

Using var(--test) would result in:
1. Class "two" element: 10px;
2. Class "three" element: 2em
3. Class "four" element: 10px (inherited from parent class "two")
4. Class "one" invalid value as it is outside scope

Background color of red only applies to the .cool-paragraph class as it is the only element in the scope of the div that contains the variable.

### The :root selector

You may want to be able to use other custom properties on many, unreleated selectors. You can declare these properties on the :root selector as it has the highest specificity. 

### Media queries

Media queries are another option for setting a theme on a website. 

1. Only dark and light themes are valid values for the media query
2. It doesn't allow users to change the themes themselves

## Frameworks and Preprocessors

Frameworks like Bootstrap and Tailwind do a lot of the heavy lifting of CSS code for you. Bulma and Foundation are two other options.

### Disadvantages

Each framework is quite...similar. Thus, it's difficult to ignore the many similarities they have on websites as they are developed using the same frameworks. I

