# @stackline/fault

Independent maintenance fork of `fault@2.0.1`, preserving its API and published type declarations.

```sh
npm install @stackline/fault
# Keep existing imports:
npm install fault@npm:@stackline/fault@1.0.0
```

[Stackline](https://alexandro.net/) · [Issues](https://github.com/alexandroit/stackline-fault/issues) · [Community](https://www.reddit.com/r/Stackline/)

See [UPSTREAM.md](UPSTREAM.md) for source identity and issue review, and [CHANGELOG.md](CHANGELOG.md) for maintenance changes. Functional tests also run against the final npm tarball; releases are published from GitHub Actions with provenance.

## Upstream documentation

# fault

[![Build][build-badge]][build]
[![Coverage][coverage-badge]][coverage]
[![Downloads][downloads-badge]][downloads]
[![Size][size-badge]][size]

Functional errors with formatted output.

## Contents

*   [What is this?](#what-is-this)
*   [When should I use this?](#when-should-i-use-this)
*   [Install](#install)
*   [Use](#use)
*   [API](#api)
    *   [`fault(format?[, values…])`](#faultformat-values)
*   [Types](#types)
*   [Compatibility](#compatibility)
*   [Security](#security)
*   [Related](#related)
*   [Contribute](#contribute)
*   [License](#license)

## What is this?

This package adds printf-like interpolation to errors.

## When should I use this?

This package useful when you frequently display parameters in error messages
and manual string concatenation is becoming verbose.

## Install

This package is [ESM only][esm].
In Node.js (version 12.20+, 14.14+, or 16.0+), install with [npm][]:

```sh
npm install fault
```

In Deno with [Skypack][]:

```js
import {fault} from 'https://cdn.skypack.dev/fault@2?dts'
```

In browsers with [Skypack][]:

```html
<script type="module">
  import {fault} from 'https://cdn.skypack.dev/fault@2?min'
</script>
```

## Use

```js
import {fault} from 'fault'

throw fault('Hello %s!', 'Eric')
```

Yields:

```text
Error: Hello Eric!
    at FormattedError (~/node_modules/fault/index.js:30:12)
    at Object.<anonymous> (~/example.js:3:7)
    …
```

Or, format a float in a type error:

```js
import {fault} from 'fault'

throw fault.type('Who doesn’t like %f? 🍰', Math.PI)
```

Yields:

```text
TypeError: Who doesn’t like 3.141593? 🍰
    at Function.FormattedError [as type] (~/node_modules/fault/index.js:30:12)
    at Object.<anonymous> (~/example.js:3:7)
```

## API

This package exports the following identifiers: `fault` and `create`.
There is no default export.

### `fault(format?[, values…])`

Create an error with a printf-like formatted message.

###### Parameters

*   `format` (`string`, optional)
    — template string
*   `values` (`*`, optional)
    — values to render in `format`

###### Returns

An [`Error`][error] instance.

###### Formatters

The following formatters are supported in `format`:

*   `%s` — string
*   `%b` — binary
*   `%c` — character
*   `%d` — decimal
*   `%f` — floating point
*   `%o` — octal
*   `%x` — lowercase hexadecimal
*   `%X` — uppercase hexadecimal
*   `%` followed by any other character, prints that character

See [`samsonjs/format`][fmt] for argument parsing.

###### Other errors

*   `fault.eval(format?[, values…])` — [EvalError][]
*   `fault.range(format?[, values…])` — [RangeError][]
*   `fault.reference(format?[, values…])` — [ReferenceError][]
*   `fault.syntax(format?[, values…])` — [SyntaxError][]
*   `fault.type(format?[, values…])` — [TypeError][]
*   `fault.uri(format?[, values…])` — [URIError][]

#### `create(Constructor)`

Factory to create instances of `ErrorConstructor` with support for formatting.
Used internally to wrap the global error constructors and exposed for custom
errors.
Returns a function just like `fault`.

## Types

This package is fully typed with [TypeScript][].
There are no extra exported types.

## Compatibility

This package is at least compatible with all maintained versions of Node.js.
As of now, that is Node.js 12.20+, 14.14+, and 16.0+.
It also works in Deno and modern browsers.

## Security

This package is safe.

## Related

*   [`wooorm/bail`](https://github.com/wooorm/bail)
    — throw if given an error

## Contribute

Yes please!
See [How to Contribute to Open Source][contribute].

## License

[MIT][license] © [Titus Wormer][author]

<!-- Definitions -->

[build-badge]: https://github.com/wooorm/fault/workflows/main/badge.svg

[build]: https://github.com/wooorm/fault/actions

[coverage-badge]: https://img.shields.io/codecov/c/github/wooorm/fault.svg

[coverage]: https://codecov.io/github/wooorm/fault

[downloads-badge]: https://img.shields.io/npm/dm/fault.svg

[downloads]: https://www.npmjs.com/package/fault

[size-badge]: https://img.shields.io/bundlephobia/minzip/fault.svg

[size]: https://bundlephobia.com/result?p=fault

[npm]: https://docs.npmjs.com/cli/install

[skypack]: https://www.skypack.dev

[license]: license

[author]: https://wooorm.com

[esm]: https://gist.github.com/sindresorhus/a39789f98801d908bbc7ff3ecc99d99c

[typescript]: https://www.typescriptlang.org

[contribute]: https://opensource.guide/how-to-contribute/

[fmt]: https://github.com/samsonjs/format

[error]: https://developer.mozilla.org/JavaScript/Reference/Global_Objects/Error

[evalerror]: https://developer.mozilla.org/JavaScript/Reference/Global_Objects/EvalError

[rangeerror]: https://developer.mozilla.org/JavaScript/Reference/Global_Objects/RangeError

[referenceerror]: https://developer.mozilla.org/JavaScript/Reference/Global_Objects/ReferenceError

[syntaxerror]: https://developer.mozilla.org/JavaScript/Reference/Global_Objects/SyntaxError

[typeerror]: https://developer.mozilla.org/JavaScript/Reference/Global_Objects/TypeError

[urierror]: https://developer.mozilla.org/JavaScript/Reference/Global_Objects/URIError.
