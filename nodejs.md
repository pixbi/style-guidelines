# Node.js JavaScript Guidelines

## Three Golden Rules

1. Comment and document liberally
2. Write test cases first
3. Prefer pure functions

## General Guidelines

### Resources

* Use [Mocha](http://visionmedia.github.io/mocha/) for testing
* Use [JSDoc](http://usejsdoc.org/) for documentation
* Prefer using [libraries](https://www.npmjs.org/) over writing code
* Read [JavaScript: The Good
  Parts](http://books.google.com/books/about/JavaScript_The_Good_Parts.html?id=PXa2bby0oQ0C)

### Style

* *Avoid global states*. States in modules and closures are fine. Global
  functions are ok as long as they are stateless. Use judgment.
* *Prefer pure functions*. Corollary to avoiding global states.
* *Avoid prototypes*. Corollary to preferring pure functions.
* *Prefer module pattern*. Corollary to avoiding prototypes.
* *Prefer simple modules*. Corollary to preferring using module patterns.
