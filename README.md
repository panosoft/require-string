# require-string

Require a module from a string in memory instead of loading it from the file system.

[![npm](https://img.shields.io/npm/v/require-string.svg)]()
[![npm](https://img.shields.io/npm/l/require-string.svg)]()
[![Travis](https://img.shields.io/travis/panosoft/require-string.svg)]()
[![David](https://img.shields.io/david/panosoft/require-string.svg)]()
[![npm](https://img.shields.io/npm/dm/require-string.svg)]()

# Installation

```
npm install @panosoft/require-string
```

# Usage

```js
var requireString = require('@panosoft/require-string');

var module = requireString('module.exports = {number: 1}');

console.log(module.number); // 1
```

# API

## requireString( content [, filename] )

Works just like Node's `require()` except it loads a module from a string instead of reading it from the file system.

A `filename` can be supplied which provides a base path from which relative `require()` paths in the string module can be resolved.

Returns the string modules `module.exports` object just like Node's `require()`.

### Arguments

- `content` - The string to load as a module.
- `filename` - The filename to apply to the module. This is used in resolving relative paths passed to `require()` within the string module. Defaults to `''` which results in relative `require()` paths being resolved relative to the current working directory of the parent Node process.

### Example
Assuming we have the following file locally, `path/to/relative/index.js`:

```js
var path = require('path');

module.exports = path;
```

Then,

```js
var requireString = require('@panosoft/require-string');

var filename = 'path/to/string/module.js';
var moduleString = ''
  + ' var relativeModule = require(\'../relative\');'
  + ' module.exports = relativeModule.resolve;';

var module = requireString(moduleString, filename);
console.log(module('.')); // current working directory
```
