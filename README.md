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
- [CSS](#css)

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

# CSS 