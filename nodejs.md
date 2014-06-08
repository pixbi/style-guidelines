# Node.js JavaScript Guidelines

## Three Golden Rules

1. Comment, document, and test liberally
2. Prefer maintainability over performance
3. Write your JavaScript as if it's C, or write it as if it's Lisp, but never
   as if it's Java as its name implies.

## General Guidelines

### Resources

* Use [Mocha](http://visionmedia.github.io/mocha/) for testing
* Use [JSDoc](http://usejsdoc.org/) for documentation
* Prefer using [libraries](https://www.npmjs.org/) over writing code
* Read [JavaScript: The Good
  Parts](http://books.google.com/books/about/JavaScript_The_Good_Parts.html?id=PXa2bby0oQ0C)

### Style

* *Avoid global states*. States in modules and closures are fine (and
  often necessary).
* *Prefer pure functions*. Corollary to avoiding global states. Functions which
  produce effect as output (e.g. `Math.random`) are fine, just not side-effects
  (e.g. `this.a = this.b + 2`).
* *Avoid prototypes*. At least in the traditional object-oriented programming
  sense of properties and methods. Corollary to preferring pure functions.
  Object-oriented programming is necessary only when programming in an
  environment without access to closure or a strong type system. Prototypes
  should only be used for data types.
* *Prefer module pattern*. Corollary to avoiding prototypes. The module pattern
  is superior to the prototype/object patterns because states are enclosed
  lexically via closure rather than dynamically.
* *Prefer simple modules*. Corollary to preferring using module patterns. When
  you have a module that creates sub-modules inside it, the module may be too
  big.
* *ALWAYS use semicolons*. Never rely on automatic semicolon insertion. It will
  break your mind.
* *Always name your function*. Static functions are preferred over anonymous
  functions, even if you need to do this: `exports.doSomething = function
  doSomething () {}`.
* *NEVER use `arguments`*. Engines can't optimize it, nor can you easily reason
  about a function using it. You should really be using an array instead of
  variadic parameters.
