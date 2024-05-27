
# Parole

[<img src="https://raw.githubusercontent.com/promises-aplus/promises-spec/master/logo.svg" alt="Promises/A+ logo" width="82px" height="82px" title="Promises/A+ 1.0 compliant" align="right" />](https://promisesaplus.com/)

<!-- [<img src="https://promisesaplus.com/assets/logo-small.png" alt="Promises/A+ logo" title="Promises/A+ 1.0 compliant" align="right" />](https://promisesaplus.com/) -->

Another ES6 promise implementation ([compliant](https://github.com/promises-aplus/promises-tests) with [Promises/A+](https://github.com/promises-aplus/promises-spec))

[![ᴋɪʟᴛ ᴊs](https://jesus.germade.dev/assets/images/badge-kiltjs.svg)](https://github.com/kiltjs)
[![npm](https://img.shields.io/npm/v/parole.svg)](https://www.npmjs.com/package/parole)
[![Build Status](https://cloud.drone.io/api/badges/kiltjs/parole/status.svg)](https://cloud.drone.io/kiltjs/parole)
[![codecov](https://codecov.io/gh/jgermade/parole/branch/master/graph/badge.svg?token=TA3W7MIMB9)](https://codecov.io/gh/jgermade/parole)
[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

## Installation
```.sh
npm install parole

# alternatively you can use bower (minified version by default)
yarn add parole
```

### ES6 fulfill

> `Parole` implements [ES6 Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) specs

Implements:
- Promise.prototype.then
- Promise.prototype.catch
- Promise.prototype.finally

Also static methods
- Promise.resolve
- Promise.reject
- Promise.all
- Promise.allSettled
- Promise.any
- Promise.race

Includes:
- Promise.defer

``` js
// parole respects the es6 promise specification
// you can use parole as global polyfill

if( !window.Promise ) {
  window.Promise = Parole;
}
```

### Example
``` js
new Parole((resolve, reject) => {
    resolve('gogogo!')
  })

  .then((result) => {
    console.log('checkpoint 1', result)
    throw 'whoops!'
  })

  .then(
    (result) => {
      console.log('checkpoint 2', result)
    },
    (result) => {
      console.log('checkpoint 2.1', result)
      return new Parole((resolve, reject) => {
        setTimeout(() => resolve('all right!'), 400)
      })
    },
  )

  .then(
    (result) => console.log('checkpoint 3', result),
    (reason) => console.log('checkpoint 3.1', reason),
  )
;
```
> output

```.sh
checkpoint 1 gogogo!
checkpoint 2.1 whoops!
# elapsed 400ms
checkpoint 3 all right!
```
