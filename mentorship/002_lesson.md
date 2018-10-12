# What is a Closure

[Source](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-closure-b2f0d2152b36)

* A closure gives you access to an outer function’s scope from an inner function. 

* Closures are created every time a function is created, at function creation time.

* To use a closure, simply define a function inside another function and expose it. To expose a function, return it or pass it to another function.

* In JavaScript, closures are the primary mechanism used to enable data privacy.

```js
const getSecret = (secret) => {
  return {
    get: () => secret
  };
};
const obj = getSecret(1);
obj.get() // 1
``` 

Note: In the example above, the `.get()` method is defined inside the scope of `getSecret()`, which gives it access to any variables from `getSecret()`, and makes it a privileged method. In this case, the parameter, `secret`.

* Closures can also be used to create stateful functions whose return values may be influenced by their internal state, e.g.:


```js
const secret = msg => () => msg
```

* In functional programming, closures are frequently used for partial application & currying:
	a) Application: The process of applying a function to its arguments in order to produce a return value.
	b) Partial Application: The process of applying a function to some of its arguments. The partially applied function gets returned for later use.
	
# Higher Order Functions
[Source](https://medium.com/javascript-scene/higher-order-functions-composing-software-5365cf2cbe99)

* A higher order function is a function that takes a function as an argument, or returns a function. 
* Higher order function is in contrast to first order functions, which don’t take a function as an argument or return a function as output.

* Earlier we saw examples of `.map()` and `.filter()`. Both of them take a function as an argument. They're both higher order functions.

* Below is an example of first order function:
```js
const censor = words => {
  const filtered = [];
  for (let i = 0, { length } = words; i < length; i++) {
    const word = words[i];
    if (word.length !== 4) filtered.push(word);
  }
  return filtered;
};
censor(['oops', 'gasp', 'shout', 'sun']);
// [ 'shout', 'sun' ]
``` 
* JavaScript has first class functions.

- Assigned as an identifier (variable) value
- Assigned to object property values
- Passed as arguments
- Returned from functions

* In other words, you can use higher order functions to make a function polymorphic.

**Note:** Polymorphism is the ability of an object to take on many forms. The most common use of polymorphism in OOP occurs when a parent class reference is used to refer to a child class object. 

# Notes from the Live Session
```js
console.clear();

const rotate = ([first, ...rest]) => [...rest, first];

console.log(
  rotate([1,2,3]) // [2,3,1]
);

const obj = {
  name: 'Dimitri',
  permissions: 'level1, level2',
  setAvatar (avatar) {
    this.avatar = avatar;
  	return this;
  }
};

class Foo  {
  constructor () {
    this.avatar = 'default.png';
    this.setAvatar = avatar => {
      this.avatar = avatar;
      return this;
    };
  }
}

const myFoo = new Foo();
myFoo.setAvatar('myfoo.png');

console.log(myFoo.avatar);

console.log(obj.setAvatar.call({ name: 'eric' }, 'superman.png'));

// name = 'Anonymous', avatar = 'anonymous.png'
const { name = 'Anonymous', avatar = 'anonymous.png' } = obj

console.log(avatar);


/*
What is functional programming?

Functional programming is a pragramming paradigm using pure functions as the atomic unit of composition, avoiding shared mutable state and side-effects.

* Pure functions
* Composition
* Avoid shared mutable state
* Isolate side-effects
*/

const add = a => b => a + b;

const inc = add(1);

/*
Pure functions:
* Given same input, always return the same output. (determinism)
* No side-effects.

Referrential transparency: You can replace a function call with its return value without changing the meaning of the program.

// algebra, not JS
f(x) = 2x

f(2) // same as below
4    // same as above

All functions with referrential transparency are safe to memoize.
*/

