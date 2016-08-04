# TypeScript style guide

This guide optimizes for readability and maintainability over performance. It includes style conventions and some TypeScript best practices.

## Types and General Naming

* Enable noImplicitAny option the compiler. [[link](https://www.stevefenton.co.uk/2013/07/typescript-no-implicit-any-compiler-flag/)]
* Avoid using the ``any`` type
* Add type information when the inference is not clear.  
* Specify function's return type if it's not clear from the implementation.

```TypeScript
// myDocument type is not obvious to the reader
getFromDatabase.done((myDocument: DocumentType) => {
  response(myDocument);
});

// Type of streetAddress is clear
const streetAddress = "221B Baker Street";
```

* Convert types with global objects instead of shorthands (``String(foo)`` over ``'' + foo``). [[link](http://www.w3schools.com/js/js_type_conversion.asp)]
* Add types to a module instead of polluting the global namespace with every interface.
* Use ``Array<number>`` over ``number[]`` as we use that syntax in our API documentation
* Don't start interfaces with the letter I.
* Use [domain-driven](http://en.wikipedia.org/wiki/Domain-driven_design) naming. Abbrevations should almost never be used, but also avoid overtly long names.

## Formatting

* Indent with *2* spaces.
* Always use curly braces
* Always add semicolons at the end of a statement [[link](https://blog.jondh.me.uk/2011/04/javascript-gotcha-implicit-semi-colon-insertion/)]
* Don't use more than 1 empty line
* End the file with a newline character.
* Don't have consecutive empty lines.
* Separate operators and variables with spaces unless it's an unary operator.
* Add a space before an opening curly brace.
Place else in the same line as the ending curly brace, always use curly braces and add whitespace after the if keyword.
* Lines should be at most 80 characters long.

```TypeScript
if (isAuthorized) {
  response();
} else {
  // Not authorized..
}
```

### Objects and Classes

* Add a new line for each property in an object.
* Use the literal syntax of objects, arrays and regular expressions.
* Use the dot notation for property access.
* Align object values as seen in the example below
* Remove whitespace at the end of lines (including empty lines).
* Add a space after the colon ``:`` character, but not before it.
* use camelCase for object properties and methods
* Use PascalCase for classes, types and constructor functions.

```TypeScript
let myObject = {
  foo:                        bar,
  longerFoo:                  true,
  evenLongerFoo:              "fooValue",
  "this-key-needs-quotation": 2
};
```

### Variables and Constants

* Use ``let`` over ``var`` to have better scoping.  [[link](http://stackoverflow.com/questions/762011/javascript-let-keyword-vs-var-keyword)]
* Use ``const`` for variables which are not re-assigned. [[link](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Statements/const)]
* Use ``UPPERCASE_SNAKE_CASE`` for constant names that are literally defined, i.e. they get a constant value assigned right from the start (at "writing time")
* Use ``camelCase`` names for constants whose values are first available at runtime but don't change afterwards.
* Don't mix up ``var`` and ``let``/``const``
* Only have one assignment per line
* Align the equal signs when having several assignments in each line
* Single letter names should only be used when the domain calls for it, e.g. mathematics. Names may include special characters (e.g. ε) if the domain calls for it.

```TypeScript
let length = someUserInput();
const area = length * width;
const PI   = 3.14;
```
### Strings

* Use ``"`` for simple strings
* Use ``'`` for strings within strings
* Use Template Strings `` ` `` when you need interpolation and/or multiline strings. [[link](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/template_strings)]

```TypeScript
`Hello, ${user}, welcome to the show
this is an awesome eveing
and we could talk the whole time.`

const foo          = require("foo");
const subFoo       = foo.subFoo;
const bar          = require("bar");
let stringInString = '"inside"';
```

Declare a variable before referencing it (e.g. declare variables in the correct order).

Don't use leading or trailing commas.

```TypeScript
let myVariable: string;
```

## Comments

* Strike a balance between commenting too much and attempting to write "self-documenting" code.
* Most comments should explain why instead of what, but sometimes it's necessary to explain what with comments.
* Leave a space before the comment text and start with a capital letter unless the first word is a variable.
* Add comment to a line before the code.

```TypeScript
// Formula proven by Archimedes
const area = π * r * r;
```

* Use [JSDoc](http://usejsdoc.org/) for documenting all named functions.

```TypeScript
/**
 * Returns a promise of the latest revision of the document with the specified id.
 * @param {string} id of the document
 * @returns {Q.Promise<DocumentType>}
 */
const getLatestDocument = (id: string) => {
  // ... implementation here
};
```

* Use ``// FIXME: `` and ``// TODO: `` tags when you know that the stuff you did / explored needs some work. TODO reflects a "medium warning", FIXME reflects a critically needed change.

```TypeScript
// FIXME: Handle error case
// TODO: Implement caching
```

## Control structures

* Use functional style ``.forEach, .map, .filter`` etc. over for/while loops whenever possible.
* When a for/while loop is required for performance reasons leave a comment stating so.

```TypeScript
// Authorization is required since commands include all commands.
commands.filter(authorizedCommand).forEach(executeCommand);
```

* Use forEach and Object.prototype.keys over ``for..in``.
* Use [lodash](https://lodash.com/docs) methods when you need more advanced functions that are not built in.

## Functions

* Use the fat arrow notation ``=>`` over the function keyword. [[link](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Functions/Arrow_functions)]
* Leave out the ()-braces if there is only one function parameter with an inferred type.
* Don't use curly braces if the function is simple and immediately returns a value. Add a space before and after ``=>``.

```TypeScript
const squaredValues = values.map(value => value * value);

const printValues = (values: number[]) => {
  console.log(JSON.stringify(values));
};
```

## Comparison

* Always use the strict equality comparision ``===`` and ``!==`` over ``==`` and ``!=``. [[link](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)]
* Use implicit boolean type coercion only for checking truthiness.

Further reading, inspiration and sources
----------------------------------------

1. https://github.com/airbnb/javascript/blob/master/README.md
2. http://www.jslint.com/
3. https://github.com/Platypi/style_typescript
4. https://github.com/Microsoft/TypeScript/wiki/Coding-guidelines
5. http://stackoverflow.com/questions/762011/javascript-let-keyword-vs-var-keyword
