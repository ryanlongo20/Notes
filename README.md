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
- [HTML](#html)
  - [SVG](#svg)
    - [Introduction](#introduction)
    - [What are they?](#what-are-they)
    - [Drawbacks](#drawbacks)
    - [Anatomy](#anatomy)
    - [Embedding SVGs](#embedding-svgs)
  - [Tables](#tables)
    - [Captions](#captions)
    - [<tfoot>, <tbody>, <thead>](#tfoot-tbody-thead)
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

### <tfoot>, <tbody>, <thead>

These tags give the table more structural definition.
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

Background color of red only applies to the .cool-paragraph class as it is the only element in the scope of the div that contains the variable 