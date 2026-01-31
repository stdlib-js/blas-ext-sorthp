<!--

@license Apache-2.0

Copyright (c) 2025 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# sorthp

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Sort an input [ndarray][@stdlib/ndarray/ctor] along one or more [ndarray][@stdlib/ndarray/ctor] dimensions using heapsort.



<section class="usage">

## Usage

```javascript
import sorthp from 'https://cdn.jsdelivr.net/gh/stdlib-js/blas-ext-sorthp@deno/mod.js';
```
The previous example will load the latest bundled code from the deno branch. Alternatively, you may load a specific version by loading the file from one of the [tagged bundles](https://github.com/stdlib-js/blas-ext-sorthp/tags). For example,

```javascript
import sorthp from 'https://cdn.jsdelivr.net/gh/stdlib-js/blas-ext-sorthp@v0.1.0-deno/mod.js';
```

#### sorthp( x\[, sortOrder]\[, options] )

Sorts an input [ndarray][@stdlib/ndarray/ctor] along one or more [ndarray][@stdlib/ndarray/ctor] dimensions using heapsort.

```javascript
import ndarray2array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-to-array@deno/mod.js';
import array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-array@deno/mod.js';

var x = array( [ -1.0, 2.0, -3.0 ] );

var y = sorthp( x );
// returns <ndarray>

var arr = ndarray2array( y );
// returns [ -3.0, -1.0, 2.0 ]

var bool = ( x === y );
// returns true
```

The function has the following parameters:

-   **x**: input [ndarray][@stdlib/ndarray/ctor]. Must have a real-valued or "generic" [data type][@stdlib/ndarray/dtypes].
-   **sortOrder**: sort order (_optional_). May be either a scalar value, string, or an [ndarray][@stdlib/ndarray/ctor] having a real-valued or "generic" [data type][@stdlib/ndarray/dtypes]. If provided an [ndarray][@stdlib/ndarray/ctor], the value must have a shape which is [broadcast-compatible][@stdlib/ndarray/base/broadcast-shapes] with the complement of the shape defined by `options.dims`. For example, given the input shape `[2, 3, 4]` and `options.dims=[0]`, an [ndarray][@stdlib/ndarray/ctor] sort order must have a shape which is [broadcast-compatible][@stdlib/ndarray/base/broadcast-shapes] with the shape `[3, 4]`. Similarly, when performing the operation over all elements in a provided input [ndarray][@stdlib/ndarray/ctor], an [ndarray][@stdlib/ndarray/ctor] sort order must be a zero-dimensional [ndarray][@stdlib/ndarray/ctor]. By default, the sort order is `1` (i.e., increasing order).
-   **options**: function options (_optional_).

The function accepts the following options:

-   **dims**: list of dimensions over which to perform operation. If not provided, the function performs the operation over all elements in a provided input [ndarray][@stdlib/ndarray/ctor].

By default, the function sorts elements in increasing order. To sort in a different order, provide a `sortOrder` argument.

```javascript
import ndarray2array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-to-array@deno/mod.js';
import array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-array@deno/mod.js';

var x = array( [ -1.0, 2.0, -3.0 ] );

var y = sorthp( x, -1.0 );
// returns <ndarray>

var arr = ndarray2array( y );
// returns [ 2.0, -1.0, -3.0 ]
```

In addition to numeric values, one can specify the sort order via one of the following string literals: `'ascending'`, `'asc'`, `'descending'`, or `'desc'`. The first two literals indicate to sort in ascending (i.e., increasing) order. The last two literals indicate to sort in descending (i.e., decreasing) order.

```javascript
import ndarray2array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-to-array@deno/mod.js';
import array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-array@deno/mod.js';

var x = array( [ -1.0, 2.0, -3.0 ] );

// Sort in ascending order:
var y = sorthp( x, 'asc' );
// returns <ndarray>

var arr = ndarray2array( y );
// returns [ -3.0, -1.0, 2.0 ]

// Sort in descending order:
y = sorthp( x, 'descending' );
// returns <ndarray>

arr = ndarray2array( y );
// returns [ 2.0, -1.0, -3.0 ]
```

By default, the function performs the operation over all elements in a provided input [ndarray][@stdlib/ndarray/ctor]. To perform the operation over specific dimensions, provide a `dims` option.

```javascript
import ndarray2array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-to-array@deno/mod.js';
import array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-array@deno/mod.js';

var x = array( [ -1.0, 2.0, -3.0, 4.0 ], {
    'shape': [ 2, 2 ],
    'order': 'row-major'
});

var v = ndarray2array( x );
// returns [ [ -1.0, 2.0 ], [ -3.0, 4.0 ] ]

var y = sorthp( x, {
    'dims': [ 0 ]
});
// returns <ndarray>

v = ndarray2array( y );
// returns [ [ -3.0, 2.0 ], [ -1.0, 4.0 ] ]
```

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   The input [ndarray][@stdlib/ndarray/ctor] is sorted **in-place** (i.e., the input [ndarray][@stdlib/ndarray/ctor] is **mutated**).
-   If `sortOrder < 0.0` or is either `'desc'` or `'descending'`, the input [ndarray][@stdlib/ndarray/ctor] is sorted in **decreasing** order. If `sortOrder > 0.0` or is either `'asc'` or `'ascending'`, the input [ndarray][@stdlib/ndarray/ctor] is sorted in **increasing** order. If `sortOrder == 0.0`, the input [ndarray][@stdlib/ndarray/ctor] is left unchanged.
-   The algorithm distinguishes between `-0` and `+0`. When sorted in increasing order, `-0` is sorted before `+0`. When sorted in decreasing order, `-0` is sorted after `+0`.
-   The algorithm sorts `NaN` values to the end. When sorted in increasing order, `NaN` values are sorted last. When sorted in decreasing order, `NaN` values are sorted first.
-   The algorithm has space complexity `O(1)` and time complexity `O(N log2 N)`.
-   The algorithm is **unstable**, meaning that the algorithm may change the order of [ndarray][@stdlib/ndarray/ctor] elements which are equal or equivalent (e.g., `NaN` values).
-   The function iterates over [ndarray][@stdlib/ndarray/ctor] elements according to the memory layout of the input [ndarray][@stdlib/ndarray/ctor]. Accordingly, performance degradation is possible when operating over multiple dimensions of a large non-contiguous multi-dimensional input [ndarray][@stdlib/ndarray/ctor]. In such scenarios, one may want to copy an input [ndarray][@stdlib/ndarray/ctor] to contiguous memory before sorting.

</section>

<!-- /.notes -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```javascript
import discreteUniform from 'https://cdn.jsdelivr.net/gh/stdlib-js/random-array-discrete-uniform@deno/mod.js';
import ndarray2array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-to-array@deno/mod.js';
import ndarray from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-ctor@deno/mod.js';
import sorthp from 'https://cdn.jsdelivr.net/gh/stdlib-js/blas-ext-sorthp@deno/mod.js';

// Generate an array of random numbers:
var xbuf = discreteUniform( 25, -20, 20, {
    'dtype': 'generic'
});

// Wrap in an ndarray:
var x = new ndarray( 'generic', xbuf, [ 5, 5 ], [ 5, 1 ], 0, 'row-major' );
console.log( ndarray2array( x ) );

// Perform operation:
sorthp( x, {
    'dims': [ 0 ]
});

// Print the results:
console.log( ndarray2array( x ) );
```

</section>

<!-- /.examples -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2026. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/blas-ext-sorthp.svg
[npm-url]: https://npmjs.org/package/@stdlib/blas-ext-sorthp

[test-image]: https://github.com/stdlib-js/blas-ext-sorthp/actions/workflows/test.yml/badge.svg?branch=v0.1.0
[test-url]: https://github.com/stdlib-js/blas-ext-sorthp/actions/workflows/test.yml?query=branch:v0.1.0

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/blas-ext-sorthp/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/blas-ext-sorthp?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/blas-ext-sorthp.svg
[dependencies-url]: https://david-dm.org/stdlib-js/blas-ext-sorthp/main

-->

[chat-image]: https://img.shields.io/badge/zulip-join_chat-brightgreen.svg
[chat-url]: https://stdlib.zulipchat.com

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/blas-ext-sorthp/tree/deno
[deno-readme]: https://github.com/stdlib-js/blas-ext-sorthp/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/blas-ext-sorthp/tree/umd
[umd-readme]: https://github.com/stdlib-js/blas-ext-sorthp/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/blas-ext-sorthp/tree/esm
[esm-readme]: https://github.com/stdlib-js/blas-ext-sorthp/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/blas-ext-sorthp/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/blas-ext-sorthp/main/LICENSE

[@stdlib/ndarray/ctor]: https://github.com/stdlib-js/ndarray-ctor/tree/deno

[@stdlib/ndarray/dtypes]: https://github.com/stdlib-js/ndarray-dtypes/tree/deno

[@stdlib/ndarray/base/broadcast-shapes]: https://github.com/stdlib-js/ndarray-base-broadcast-shapes/tree/deno

</section>

<!-- /.links -->
