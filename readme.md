# extract-zip

Streaming unzip written in pure JavaScript. Extracts a zip into a directory. Available as a library or a command line program.

Uses the [`yauzl`](http://npmjs.org/yauzl) ZIP parser.

[![NPM](https://nodei.co/npm/extract-zip.png?global=true)](https://nodei.co/npm/extract-zip/)

## Installation

Get the library:

```
npm install extract-zip --save
```

Install the command line program:

```
npm install extract-zip -g
```

## JS API

```js
var extract = require('extract-zip')
extract(source, {dir: target}, function(err) {

})
```

If not specified, `dir` will default to `process.cwd()`.

## CLI Usage

```
extract-zip foo.zip <targetDirectory>
```

If not specified, `targetDirectory` will default to `process.cwd()`.

## Electron Usage
Electron monkey-patches the `'fs'` module to support `.asar` archives - because of this any `'fs'` api calls to an `.asar` file (or even a file named `*.asar`) fail. In this case here, if you try to run `extract-zip` from Electron on a `.zip` file containing an '.asar' file inside, the process will fail. In order to support this, we detect for `process.versions.electron` and `require('original-fs')`, an unmodified version of the `'fs'` library. 

More info:
- https://github.com/atom/electron/issues/1658
- https://github.com/atom/electron/issues/782
