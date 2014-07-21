# JavaScript Coding Style

## Three Golden Rules

1. Comment, document, and test liberally
2. Prefer maintainability over performance
3. Write your JavaScript as if it's C, or write it as if it's Lisp, but never
   as if it's Java as its name implies.


## General Guidelines

In no particular order:

* *No long functions*. No hard limit. Rule of thumb: if it performs more than
  one logical operation, split it up. Best to stay low double digits in terms
  of line numbers.
* *Cache DOM references* if they are looked up more than once
* *Avoid global states*. States in modules and closures are fine (and
  often necessary).
* *Prefer pure functions*. Corollary to avoiding global states. Functions which
  produce effect as output (e.g. `Math.random`) are fine, just not side-effects
  (e.g. `this.a = this.b + 2`).
* *Avoid prototypes*. Corollary to preferring pure functions. Object-oriented
  programming is necessary only when programming in an environment without
  access to closure or a strong type system.
* *Use `new` and `this` sparingly*. Only use `this` in constructors and `new`
  for data types (i.e. no methods).
* *ALWAYS use semicolons*. Never rely on automatic semicolon insertion. It will
  break your mind.
* *Always name your function*. Static functions are preferred over anonymous
  functions, even if you need to do this: `exports.doSomething = function
  doSomething () {}`. This is for debugging purpose.
* *NEVER use `arguments`*. Engines can't optimize it, nor can you easily reason
  about a function using it. You should really be using an array instead of
  variadic parameters.
* *Avoid `try...catch`* JavaScript already gives sparse and useless error messages. Don't
  make your life harder by allowing your code to arbitrarily hide them. Plus,
  JavaScript engines can't optimize any code in the `try...catch` block. If you
  must use it (e.g. `JSON.parse`), isolate it in its own function.
* *Do not nest anything*. This includes `setTimeout`, callbacks, and functions.
  Having one level of nesting is acceptable but more than that is a sign of
  something wrong.
* *No flexible object structure*. If you need to do something like `a =
  b[0].child[4]`, you're doing something wrong. If a complex structure is
  needed, decompose it with a series of composed/chained functions.
* *Use data types*. Typing is good for your mind. Logical data types like
  `Person`, not machine types like `int`.
* *Single assignment*. Do not re-use variables for different purposes. There is
  no valid use case for that.


## Pure Function Preference

Prefer pure functions for "logic". Logic is loosely defined here. Essentially
most code is logic code. "Non-logic" code would be any direct I/O (e.g. DOM,
localStorage, XMLHttpRequest).

References to free variables (i.e. those outside of the currently executing
function) other than variables from the same component are prohibited.

Use impure functions for presentation.


## Resources

* Use [Mocha](http://visionmedia.github.io/mocha/) for testing
* Use [Google Closure Compiler JSDoc
  style](https://developers.google.com/closure/compiler/) for documentation
* Prefer using [libraries](https://www.npmjs.org/) over writing code
* Read [JavaScript: The Good
  Parts](http://books.google.com/books/about/JavaScript_The_Good_Parts.html?id=PXa2bby0oQ0C)


## JavaScript Performance Hacks

* FIRST, cache all DOM elements that are used more than once.
* Use hand-coded JavaScript. It is much more difficult to optimize with
  CoffeeScript or other compile-to-JavaScript languages.
* Only use static functions or functions in simple objects (i.e. no prototypes).
  - http://jsperf.com/define-prototype-function-vs-define-static-function
  - http://jsperf.com/prototypal-performance/54
* In fact, use pure, static functions, which are the closest thing to inlining
  code.
  - http://jsperf.com/return-closure
  - http://jsperf.com/pure-function-vs-inlining/2
* Keep objects and arrays out if possible (i.e. use multiple variables instead
  an object).
  - http://jsperf.com/small-array-vs-object-vs-separate-variables
  - http://jsperf.com/array-vs-variables-of-same-type
* Prefer native arrays over typed arrays.
  - http://jsperf.com/native-vs-typed-js-array-speed/34
* If you must use objects, prefer dot notation.
  - http://jsperf.com/cached-object-property-access
* Prefer straight function calls (e.g. avoid using event listeners and
  heavily wrapped functions).
  - http://jsperf.com/closure-function-declaration-vs-function-expression/3
* Avoid closures, at least deeply nested closures.
  - http://jsperf.com/closure-vs-static-global-vs-parameter
* Always use `while` loop over any other looping methods. It's much faster
  while being non-destructive.
  - http://jsperf.com/fastest-array-loops-in-javascript/32
  - http://jsperf.com/reversed-while-vs-for
* Prefer local over closure (and by extension, global) variables. If
  access to closure variables is a must, cache it as soon as the function
  begins by declaring a local variable.
  - http://jsperf.com/global-vs-parameter
* Use `parseInt` on Safari-family engines and `- 0` on other major engines. For
  convenience, always use `- 0`.
  - http://jsperf.com/number-casting/2
* Use `className` for initialization but use `classList` for subsequent
  operations.
  - http://jsperf.com/classname-vs-classlist-showdown/5
  - http://jsperf.com/element-classlist-vs-element-classname/4
  - http://jsperf.com/classlist-versus-classname/4
* When a game loop is used, and of course you're using `requestAnimationFrame`,
  which only takes a function, you should put the parameters as global/closure
  variables instead of using a closure or `bind`.
  - http://jsperf.com/closure-vs-bind-vs-global-vars-with-anim-frames
* Use functions liberally as function calls are slower but the difference is
  negligible. An implication is that using functions to wrap around common
  nested property lookup operations to save output size is desirable.
  - http://jsperf.com/function-vs-inline
  - http://jsperf.com/function-vs-inline-2
  - http://jsperf.com/function-vs-inline-3
  - http://jsperf.com/function-vs-inline-4
* You should never use the `arguments` object.
  - http://jsperf.com/arguments/10


### tl;dr

Basically, use a flat data structure (to avoid object lookup penalty) with as
much heap data pre-allocated as possible (to avoid garbage collection), and
cache references to closure variables (to avoid the closure lookup penalty).

Note that pure local variables (i.e. those in leaf node functions) live on the
stack so the garbage collection issue doesn't apply. Only closure variables
live in the heap.


### Further readings

* ["Writing Fast, Memory-Efficient
  JavaScript"](http://www.smashingmagazine.com/2012/11/05/writing-fast-memory-efficient-javascript/)
  by Addy Osmani
* [V8 Design Elements](https://developers.google.com/v8/design)
* [Google's recommendations on "Optimizing JavaScript
  code"](https://developers.google.com/speed/articles/optimizing-javascript)
* [Performance Tips for JavaScript in V8](http://www.html5rocks.com/en/tutorials/speed/v8/)
* [V8 Optimization killers](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers)
* [Improving JavaScript Performance by Deconstructing the Type
  System](http://iacoma.cs.uiuc.edu/iacoma-papers/pldi14.pdf)
