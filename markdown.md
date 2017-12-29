

class: center, middle
# Design Patterns in React

Josh Martin

https://cjoshmartin.com

[contact@cjoshmartin.com](mailto:contact@cjoshmartin.com)

---

# Who am I? 

*   Computer Engineering Junior (specializing in Software Design and Embedded Systems) 
*   Minoring Mathematics and Computer Science
*   Spend most of my time programming or dancing

---

# Introduction

#### What is a Design Pattern?

A **Design Pattern** is a general repeatable solution to a commonly occurring problem in software design.

A **Anti-Pattern** is a common response to a recurring problem that is usually ineffective and risks being highly counterproductive


---

# Introduction 

#### Types of Design Patterns

1. Creational
    -   Concerned with the process of creating objects

2. Structural
    - concerned with the stuture of objects

3. Behavioral
    - concerned with how objects interact
---
# State
* Behavioral design pattern
.center[
![State diagram for a turnstile](img/turnstile-finite-state.png)
![Turnstile](img/turnstile.jpg)
]
---
## Stateless (Functional Based Components)

```javascript
export const props_Tacos = (props) => {
    return (
        <div>
        {props.has_tacos}
        </div>
    )
} 
```
---
## Stateful (Class Based Components)

```javascript
export default class Tacos extends Component {

    constructor(props){
        super(props);
        this.state ={
        has_tacos: false,
        }
    }

    render(){ 
    
    return( <props_Tacos {... this.state} />
    
    );
 }
}
```
---
# Scope and Immutability 
--

* variables and functions are hoisted in javascript
```javascript
    // expected: ReferenceError: a is not defined
    console.log(a) 
    var a = 1;
```
--
```javascript
    // reality: will return undefined
    var a;
    console.log(a)
    a = 1;
```
---
# Scope and Immutability 
--

 * `var`

--
    - functionally scoped
--

```javascript
    // what we see
    function tacos()
    {
        // ... 

        for (var i=0; i< 1; i++)
        {
            console.log('I like tacos\n')
        }
    }
```
--
```javascript
    // what javascript see
    function tacos()
    {
        var i; // always hoisted to the top of the function

        // ... 

        for (i=0; i< 1; i++)
        {
            console.log('I like tacos\n')
        }
    }
```
---
# Scope and Immutability 

--
 * `gobal variables`

--
    - `var` can became globally scoped, if not inside a function
--

    - Type a variable with out a variable type and that variable will become gobally scoped

```javascript
    (
     function() {
     for (i = 0; i < 1; i++) {i /* does nothing */ }
     } // end of function
    )() // this special syntax tells javascript to run the function immediately 

    // expected: ReferenceError: i is not defined
    // reality: Array starts at 1
    console.log('Array starts at', i) 
 ```
---
# Scope and Immutability 

* How do we this problem of scope?

--
    - use `"use strict";` at the top of your javascript files

```javascript
    "use strict";

    (
     function() {
     for (i = 0; i < 1; i++) {i /* does nothing */ }
     } // end of function
    )() // this special syntax tells javascript to run the function immediately 

    // expected: ReferenceError: i is not defined
    // reality: ReferenceError: i is not defined
    console.log('Array starts at', i) 
```

--
    
* Don't use `var` 

--
    - use `let` and `const` instead
---

# Scope and Immutability 
--

 * `let`
    - Blocked scoped
    - doesn't add a property on the gobal object (e.g. window), like `var` does
    - **Mutable** meaning the value can be changed later on
--

```javascript
    // what we see
    function tacos()
    {
        // ... 

        for (let i=0; i< 1; i++)
        {
            console.log('I like tacos\n')
        }
    }
```
--
```javascript
    // what javascript see
    function tacos()
    {
        // ... 

        for (let i=0; i< 1; i++)
        {
            console.log('I like tacos\n')
        }
    }
```

---

# Scope and Immutability 

--
 * `const`
    - Blocked scoped
    - **Immutable** meaning the value **cannot** be reassigned later on

```javascript
    const immutable = 'nana-a-boo-boo, you cannot change my value';
    
    immutable = 'I will try'; // TypeError: Assignment to constant variable.
```

https://scotch.io/tutorials/understanding-hoisting-in-javascript
---

# Scope and Immutability 

*   Immutability is a great feature
    - In React, `props` are immutable. Which prevents a conflict in their shared state.
--

.center[![broken computer](img/computer-problem.jpg)]
---
# Scope and Immutability 

*   Immutability is a great feature
    - In React, `props` are immutable. Which prevents a conflict in their shared state.

![full_size_img](img/thumbs-and-money.webp)
---

# Scope and Immutability 

*   Immutability is a great feature
    - In React, `props` are immutable. Which prevents a conflict in their shared state.

.center[![bad-state](img/bad-state.jpg)]
---
# Coupling
--

* React is loosely coupled framework
--

* **Coupling** is the degree of interdependence between software modules.

    - Tighly Coupled
    - Loosely Coupled
--

*  **Cohesion** is the degree of which elements inside a component belong together

    - Loosely Coupling -> High Cohesion
    - Tighly Coupled -> Low Cohesion
---
<!---
# what an Object is in Javascript

* functions are objects (crazy isn't it?)

--->

# Class Keyword
   

* Just recently added to javascript in ECMAScript 6


https://www.youtube.com/watch?v=Tllw4EPhLiQ
---
## basic example of a class
<iframe width="100%" height="310" src="//jsfiddle.net/cjoshmartin/9LvjLL31/embedded/js,result/" allowpaymentrequest allowfullscreen="allowfullscreen" frameborder="0"></iframe>
---
## Functions
<iframe width="100%" height="400" src="//jsfiddle.net/cjoshmartin/8ehkrrgn/embedded/js,result/" allowpaymentrequest allowfullscreen="allowfullscreen" frameborder="0"></iframe>
---
## Inheritance
<iframe width="100%" height="500" src="//jsfiddle.net/cjoshmartin/hak37x3b/1/embedded/js,result/" allowpaymentrequest allowfullscreen="allowfullscreen" frameborder="0"></iframe>
---
# Inheritance
    
* When an object is derived from another object

* "Is A" relationship 

.center[![Inheritance](img/inheritance.png)]
---
# Composition

* Type of Aggregation
    - Aggregation is when compose a component such that it made of up of other component

    - "Has a" relationship

* focused on what a thing does and not what it is
---
## Surprise!!
* Classes are just abstractions on top of the **Prototype Inheritance Model**

<iframe width="100%" height="400" src="//jsfiddle.net/cjoshmartin/7j8nxod1/embedded/js,result/" allowpaymentrequest allowfullscreen="allowfullscreen" frameborder="0">

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain
---
# what is a Prototype?

* Creational Design Pattern

* Prototypes is how Javscript achieves inheritance


* This Prototype modal allows to use the `new` keyword on our functions and classes in javascript.

    - creates an object and check the prototype of whatever it is being called on (e.g. `const josh = new person('Josh');` )
* Pure object use the keyword `__proto__`

* functions use the keyword `prototype`
---
# Prototype vs Classes
![diff_of_proto_and_class](img/diff_proto_vs_class.png)

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Details_of_the_Object_Model
---
## Recreate this using prototypes
<iframe width="100%" height="500" src="//jsfiddle.net/cjoshmartin/hak37x3b/1/embedded/js,result/" allowpaymentrequest allowfullscreen="allowfullscreen" frameborder="0"></iframe>
---
## Create our basic "class"
```javascript
// Basic `class` and defualt constructor
function hello(name){
  this.name = name;
}

// Adding a function to our `class` of `talk`
hello.prototype.talk = function(){
  return `Hello ${this.name}!`
}

// Create a instance and use it!
const say_hello = new hello('Josh');
const selector = document.querySelector('.test-center');
selector.innerHTML = say_hello.talk();
```
---
## Lets extend our basic "class" like normal

<iframe width="100%" height="450" src="//jsfiddle.net/cjoshmartin/kaqxfkLz/embedded/js,result/" allowpaymentrequest allowfullscreen="allowfullscreen" frameborder="0"></iframe>
---
## Lets extand our basic "class" only using prototypes
<iframe width="100%" height="500" src="//jsfiddle.net/cjoshmartin/8m3hon57/embedded/js,result/" allowpaymentrequest allowfullscreen="allowfullscreen" frameborder="0"></iframe>
---
# Factories
---
# Adapter

* Babel
---
# Obserables
---
# End
