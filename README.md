# @minikit/array

Immutable Array prototype methods.

- TypeScript
- Small and Thin
    - `@minikit/array` that includes all methods: ~500bytes(gzip+minify)
- Same usage with native `Array.prototype` methods

## Why?

ECMAScript `Array` has some mutable methods.

This library provide immutable version of each methods.

### Mutable method on `Array.prototype`

| Native method: Return type               | `@minikit/array`                       |
| ---------------------------------------- | ---------------------------------------- |
| [`Array.prototype.pop()`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/pop): `any`| [`pop()`](packages/pop): new  `Array` |
| [`Array.prototype.push()`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/push): `Number`| [`push()`](packages/push): new  `Array` |
| [`Array.prototype.shift()`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/shift): `any`| [`shift()`](packages/shift): new  `Array` |
| [`Array.prototype.unshift()`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift): `Number`| [`unshift()`](packages/unshift): new  `Array` |
| [`Array.prototype.splice()`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/splice): `Array`| [`splice()`](packages/splice): new  `Array` |
| [`Array.prototype.reverse()`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse): `Array`| [`reverse()`](packages/sort): new `Array` |
| [`Array.prototype.sort()`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/sort): `Array`| [`sort()`](packages/sort): new  `Array` |
| [`Array.prototype.fill()`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/fill): `Array`| [`fill()`](packages/fill): new `Array` |
| [`Array.prototype.copyWithin()`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/copyWithin): `Array`| [`copyWithin()`](packages/copy-within): new `Array` |


## Install

`@minikit/array` includes all methods.

Install with [npm](https://www.npmjs.com/):

    npm install @minikit/array

## Usage

`@minikit/array` is a collection of immutable `Array.prototype` methods.

Basically, the usage of these method is same with mutable version.

```js
import {
  sort,
  unshift,
  push,
  fill,
  splice,
  pop,
  reverse,
  copyWithin,
  shift
} from '@minikit/array';

describe('prototype', () => {
  it('shift', () => {
    assert.deepStrictEqual(shift(['a', 'b', 'c', 'd', 'e']), [
      'b',
      'c',
      'd',
      'e'
    ]);
  });
  it('unshift', () => {
    assert.deepStrictEqual(unshift(['a', 'b', 'c', 'd', 'e'], 'x'), [
      'x',
      'a',
      'b',
      'c',
      'd',
      'e'
    ]);
  });
  it('pop', () => {
    assert.deepStrictEqual(pop(['a', 'b', 'c', 'd', 'e']), [
      'a',
      'b',
      'c',
      'd'
    ]);
  });
  it('push', () => {
    assert.deepStrictEqual(push(['a', 'b', 'c', 'd', 'e'], 'x'), [
      'a',
      'b',
      'c',
      'd',
      'e',
      'x'
    ]);
  });
  it('splice', () => {
    assert.deepStrictEqual(splice(['a', 'b', 'c', 'd', 'e'], 0, 1, 'x'), [
      'x',
      'b',
      'c',
      'd',
      'e'
    ]);
  });
  it('sort', () => {
    assert.deepStrictEqual(sort(['e', 'a', 'c', 'b', 'd']), [
      'a',
      'b',
      'c',
      'd',
      'e'
    ]);
  });
  it('reverse', () => {
    assert.deepStrictEqual(reverse(['a', 'b', 'c', 'd', 'e']), [
      'e',
      'd',
      'c',
      'b',
      'a'
    ]);
  });
  it('fill', () => {
    assert.deepStrictEqual(fill(new Array(5), 'x'), ['x', 'x', 'x', 'x', 'x']);
  });
  it('copyWithin', () => {
    assert.deepStrictEqual(copyWithin(['a', 'b', 'c', 'd', 'e'], 0, 3, 4), [
      'd',
      'b',
      'c',
      'd',
      'e'
    ]);
  });
});
```

## Benchmarks

Benchmark that is native `Array.prototype` methods vs. `@minikit/array`

See [benchmark](packages/benchmark).
    
    Native `Array.prototype`          |    @minikit/array
    > node src/array.js |                  > immutable-array.js
                                      |
    # pop 200000 times               >>>   # pop 200000 times
    ok ~330 ms (0 s + 330397151 ns)  >>>   ok ~267 ms (0 s + 267348617 ns)
                                  |
    # push 200000 times              >>>   # push 200000 times
    ok ~169 ms (0 s + 168738061 ns)  >>>   ok ~141 ms (0 s + 140502324 ns)
                                  |
    # shift 200000 times             <<<   # shift 200000 times
    ok ~296 ms (0 s + 295892983 ns)  <<<   ok ~419 ms (0 s + 418852725 ns)
                                  |
    # unshift 200000 times           <<<   # unshift 200000 times
    ok ~51 ms (0 s + 50817590 ns)    <<<   ok ~191 ms (0 s + 191329502 ns)
                                  |
    # sort 2000 times                >>>   # sort 2000 times
    ok ~933 ms (0 s + 932551400 ns)  >>>   ok ~611 ms (0 s + 610748601 ns)
                                  |
    # reverse 200000 times           >>>   # reverse 200000 times
    ok ~555 ms (0 s + 554921645 ns)  >>>   ok ~455 ms (0 s + 455068191 ns)
                                  |
    # fill 200000 times              >>>   # fill 200000 times
    ok ~782 ms (0 s + 782159758 ns)  >>>   ok ~699 ms (0 s + 698677543 ns)
                                  |
    # splice 200000 times            <<<   # splice 200000 times
    ok ~287 ms (0 s + 286547242 ns)  <<<   ok ~391 ms (0 s + 391294720 ns)
                                  |
    # copyWithin 200000 times        <<<   # copyWithin 200000 times
    ok ~237 ms (0 s + 236837575 ns)  <<<   ok ~275 ms (0 s + 275267401 ns)
                                  |
    all benchmarks completed         >>>   all benchmarks completed
    ok ~3.64 s (3 s + 638863405 ns)  >>>   ok ~3.45 s (3 s + 449089624 ns)

## Support Policy

### Do

- Provide immutable version of `Array.prototype` method
- Provide each method as an module
    - All prototype method: `import { push } from "@minikit/array"`
- ECMAScript compatible API

For example, `@minikit/array` method should return same result with native API.

```js
import { splice } from '@minikit/array';
var array = [1, 2, 3];
// immutable
var resultArray = splice(array, -1, 1, 'x');
// native
array.splice(-1, 1, 'x');
assert.deepStrictEqual(array, resultArray);
```

### Do not

- Add non-standard method in ECMAScript
    - e.g.) `update`, `delete`, `merge`...
- Each method depended on other method

## Related

- [Pure javascript immutable arrays](https://vincent.billey.me/pure-javascript-immutable-array/ "Pure javascript immutable arrays")
- [georapbox/immutable-arrays: Immutable versions of normally mutable array methods](https://github.com/georapbox/immutable-arrays "georapbox/immutable-arrays: Immutable versions of normally mutable array methods")
- [micnews/immutable-array-methods](https://github.com/micnews/immutable-array-methods "micnews/immutable-array-methods")
- [kolodny/immutability-helper: mutate a copy of data without changing the original source](https://github.com/kolodny/immutability-helper "kolodny/immutability-helper: mutate a copy of data without changing the original source")

## Running tests

Run following commands:

    yarn install
    yarn test

## License

MIT © azu & billgo