# Base58btc Isomorphic Encoder/Decoder for JS and TS _(@interop/base58-universal)_

[![Build status](https://img.shields.io/github/workflow/status/interop-alliance/base58-universal/Node.js%20CI)](https://github.com/interop-alliance/base58-universal/actions?query=workflow%3A%22Node.js+CI%22)
[![NPM Version](https://img.shields.io/npm/v/@interop/base58-universal.svg)](https://npm.im/@interop/base58-universal)

> Isomorphic JS encode/decode library using the [Base58 (Bitcoin) encoding scheme](https://github.com/digitalbazaar/base58-spec) (for Node.js and browsers).

## Table of Contents

- [Background](#background)
- [Security](#security)
- [Install](#install)
- [Usage](#usage)
- [Contribute](#contribute)
- [License](#license)

## Background

(Converted to TypeScript from Digital Bazaar's [`base58-universal`](https://github.com/digitalbazaar/base58-universal)
repository.)

This library provides a TypeScript and JS encoder/decoder functions for 
the [Base58 (Bitcoin) encoding scheme](https://github.com/digitalbazaar/base58-spec)
using an alphabet popularized by Bitcoin. It works in both [Node.js][] and in
Web browsers with no dependencies.

## Security

TBD

## Install

- Node.js 12+.

### NPM

To install via NPM:

```
npm install @interop/base58-universal
```

### Development

To install locally (for development):

```
git clone https://github.com/interop-alliance/base58-universal.git
cd base58-universal
npm install
```

## Usage


The library can be loaded with ESM or CommonJS:

```js
import * as base58btc from '@interop/base58-universal'
```

```js
const base58btc = require('@interop/base58-universal')
````

### Encoding

* `encode(input: Uint8Array): string`
  * Returns a base58 encoded string.

```js
const input1 = Uint8Array([1, 2, 3, 4])
const encoded1 = base58btc.encode(input1)
// > 2VfUX

const input2 = Uint8Array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
const encoded2 = base58btc.encode(input2)
// > 4HUtbHhN2TkpR
```

### Decoding

* `decode(input: string): Uint8Array`
  * **`input`**: `string` - string to decode
  * Returns a `Uint8Array` with the decoded bytes.

```js
const input3 = '2VfUX'
const decoded3 = base58btc.decode(input3)
// > Uint8Array [ 1, 2, 3, 4 ]

const input4 = '4HUtbHhN2TkpR'
const decoded4 = base58btc.decode(input4)
// > Uint8Array [
//   1, 2, 3, 4,  5,
//   6, 7, 8, 9, 10
// ]
```

### String Handling

This library uses [Uint8Array][] for encoder input and decoder output.
Conversion to and from strings can be done with a variety of tools.

#### Browser

- [TextEncoder][] and [TextDecoder][] using the [Encoding][] standard.

```js
const input5 = new TextEncoder().encode('abc')
const encoded5 = base58btc.encode(input5)
// > ZiCa

const decoded6 = base58btc.decode(encoded5)
const output6 = new TextDecoder().decode(decoded6)
// > abc
```

#### Node.js

- [TextEncoder][] and [TextDecoder][] using the [Encoding][]
  standard.
- [Buffer][] `from` and `toString` with encoding options.

```js
// Using TextEncoder/TextDecoder (included in Node.js since v12)
const input7 = new TextEncoder().encode('abc')
const encoded7 = base58btc.encode(input7)
// > ZiCa

const decoded8 = base58btc.decode(encoded7)
const output8 = new TextDecoder().decode(decoded8)
// > abc

// Using Buffer (which is a Uint8Array)
const input9 = Buffer.from('616263', 'hex')
const encoded9 = base58btc.encode(input9)
const decoded9 = base58btc.decode(encoded9)
Buffer.from(decoded9).toString()
// > abc
Buffer.from(decoded9).toString('hex')
// > 616263
```

## Contribute

PRs accepted.

* Linting: [Standard.js + TypeScript style](https://github.com/standard/eslint-config-standard-with-typescript)
* Code Formatting: [Prettier (+ TypeScript)](https://github.com/prettier/eslint-config-prettier)
* Readme: [standard-readme](https://github.com/RichardLitt/standard-readme).

## License

TypeScript conversion: [MIT License](LICENSE.md) © 2021 Interop Alliance and Dmitri Zagidulin.

Isomorphic JS implementation from [Digital Bazaar/`base58-universal`](https://github.com/digitalbazaar/base58-universal) 
under the New BSD License (3-clause).

Encoder/decoder original implementation from
[base-x](https://github.com/cryptocoinjs/base-x) under the MIT License.

[Buffer]: https://nodejs.org/api/buffer.html
[Encoding]: https://encoding.spec.whatwg.org/
[Node.js]: https://nodejs.org/
[TextDecoder]: https://developer.mozilla.org/en-US/docs/Web/API/TextDecoder
[TextEncoder]: https://developer.mozilla.org/en-US/docs/Web/API/TextEncoder
[The Base58 Encoding Scheme]: https://github.com/digitalbazaar/base58-spec
[Uint8Array]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array
