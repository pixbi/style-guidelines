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
  (e.g. `this.a = 1`).
* *Avoid prototypes*. Corollary to preferring pure functions. Object-oriented
  programming is necessary only when programming in an environment without
  access to closure and a strong type system (if inheritance is needed).
* *Prefer module pattern*. Corollary to avoiding prototypes. The module pattern
  is superior to the prototype/object patterns because states are enclosed
  lexically via closure rather than dynamically.
* *Prefer simple modules*. Corollary to preferring using module patterns. When
  you have a module that creates sub-modules inside it, it may be a sign of
  troubles to come.
* *Avoid `new` and `this`*. `new` and `this` are used in combination with
  prototypes. Using `new` is fine as it defines a new type (though in a weak
  type system that JavaScript offers), but *never* attach methods as it makes
  reasoning about the program harder via a dynamic scope.
* *ALWAYS use semicolons*. Never rely on automatic semicolon insertion. It will
  break your mind.
* *Always name your function*. Static functions are preferred over anonymous
  functions, even if you need to do this: `exports.doSomething = function
  doSomething () {}`
* *NEVER use `arguments`*. Engines can't optimize it, nor can you easily reason
  about a function using it. You should really be using an array instead of
  variadic parameters.
