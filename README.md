[![Build Status](https://travis-ci.org/pelevesque/has-prohibited-substring-at-indexes.svg?branch=master)](https://travis-ci.org/pelevesque/has-prohibited-substring-at-indexes)
[![Coverage Status](https://coveralls.io/repos/github/pelevesque/has-prohibited-substring-at-indexes/badge.svg?branch=master)](https://coveralls.io/github/pelevesque/has-prohibited-substring-at-indexes?branch=master)
[![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

# has-prohibited-substring-at-indexes

Checks if a string has at least one prohibited substring at a given index.

## Related Packages

https://github.com/pelevesque/has-prohibited-substring    
https://github.com/pelevesque/has-prohibited-substring-after-sums  
https://github.com/pelevesque/has-required-substrings    
https://github.com/pelevesque/has-required-substrings-at-indexes    
https://github.com/pelevesque/has-required-substrings-after-sums  

## Node Repository

https://www.npmjs.com/package/@pelevesque/has-prohibited-substring-at-indexes

## Installation

`npm install @pelevesque/has-prohibited-substring-at-indexes`

## Tests

### Standard Style & Unit Tests

`npm test`

### Unit Tests & Coverage

`npm run cover`

## Usage

```js
str                       (required)
prohibitedSubstrings      (required)
allowLastSubstringToBleed (optional) default = false
```

### Requiring

```js
const hasProhibitedSubstringAtIndexes = require('@pelevesque/has-prohibited-substring-at-indexes')
```

### Basic Usage

`prohibitedSubstrings` is an object of index -> substring pairs. `true` is returned
if at least one substring is found at the correct index.

```js
const str = 'abcde'
const prohibitedSubstrings = { 0: 'e' }
const result = hasProhibitedSubstringAtIndexes(str, prohibitedSubstrings)
// result === false
```

```js
const str = 'abcde'
const prohibitedSubstrings = { 0: '!', 2: 'c', 4: '!' }
const result = hasProhibitedSubstringAtIndexes(str, prohibitedSubstrings)
// result === true
```

```js
const str = 'a man a plan a canal'
const prohibitedSubstrings = { 2: 'man', 8: 'plan', 15: 'canal' }
const result = hasProhibitedSubstringAtIndexes(str, prohibitedSubstrings)
// result === true
```

### Options

#### allowLastSubstringToBleed

The `allowLastSubstringToBleed` option is `false` by default. It it used when you want
to allow the last substring to be incomplete if the string is too short.
In the following example, the last substring `canal` starts at the correct index,
but remains incomplete since the string ends. Normally this would return `false`.
With `allowLastSubstringToBleed` set to `true`, it returns `true`.

```js
const str = 'a man a plan a c'
const prohibitedSubstrings = { 15: 'canal' }
const allowLastSubstringToBleed = true
const result = hasProhibitedSubstringAtIndexes(str, prohibitedSubstrings, allowLastSubstringToBleed)
// result === true
```

##### options style

For style compatibility with related packages like `has-required-substrings-after-sums`,
it is possible to set `allowLastSubstringToBleed` using an options style.

```js
const str = 'a man a plan a c'
const prohibitedSubstrings = { 15: 'canal' }
const allowLastSubstringToBleed = true
const result = hasProhibitedSubstringAtIndexes(str, prohibitedSubstrings, {
  allowLastSubstringToBleed: allowLastSubstringToBleed
})
// result === true
```
