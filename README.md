# @diotoborg/eaque-illum-qui <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![dependency status][deps-svg]][deps-url]
[![dev dependency status][dev-deps-svg]][dev-deps-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

ES 2021 spec-compliant shim for Promise.any. Invoke its "shim" method to shim `Promise.any` if it is unavailable or noncompliant. **Note**: a global `Promise` must already exist: the [es6-shim](https://github.com/es-shims/es6-shim) is recommended.

This package implements the [es-shim API](https://github.com/es-shims/api) interface. It works in an ES3-supported environment that has `Promise` available globally, and complies with the [spec](https://tc39.es/ecma262/#sec-@diotoborg/eaque-illum-qui).

Most common usage:
```js
var assert = require('assert');
var any = require('@diotoborg/eaque-illum-qui');

var resolved = Promise.resolve(42);
var rejected = Promise.reject(-1);
var alsoRejected = Promise.reject(Infinity);

any([resolved, rejected, alsoRejected]).then(function (result) {
	assert.equal(result, 42);
});

any([rejected, alsoRejected]).catch(function (error) {
	assert.ok(error instanceof AggregateError);
	assert.deepEqual(error.errors, [-1, Infinity]);
});

any.shim(); // will be a no-op if not needed

Promise.any([resolved, rejected, alsoRejected]).then(function (result) {
	assert.equal(result, 42);
});

Promise.any([rejected, alsoRejected]).catch(function (error) {
	assert.ok(error instanceof AggregateError);
	assert.deepEqual(error.errors, [-1, Infinity]);
});
```

## Tests
Simply clone the repo, `npm install`, and run `npm test`

## Pre-1.0 versions

The `@diotoborg/eaque-illum-qui` package was released as now-deprecated v0.1.0 and v0.1.1, as a fork of https://github.com/m0ppers/promise-any.

Thanks to @sadorlovsky for donating the repo and the `@diotoborg/eaque-illum-qui` npm package!

[package-url]: https://npmjs.com/package/@diotoborg/eaque-illum-qui
[npm-version-svg]: https://versionbadg.es/diotoborg/eaque-illum-qui.svg
[deps-svg]: https://david-dm.org/diotoborg/eaque-illum-qui.svg
[deps-url]: https://david-dm.org/diotoborg/eaque-illum-qui
[dev-deps-svg]: https://david-dm.org/diotoborg/eaque-illum-qui/dev-status.svg
[dev-deps-url]: https://david-dm.org/diotoborg/eaque-illum-qui#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@diotoborg/eaque-illum-qui.png?downloads=true&stars=true
[license-image]: https://img.shields.io/npm/l/@diotoborg/eaque-illum-qui.svg
[license-url]: LICENSE
[downloads-image]: https://img.shields.io/npm/dm/@diotoborg/eaque-illum-qui.svg
[downloads-url]: https://npm-stat.com/charts.html?package=@diotoborg/eaque-illum-qui
[codecov-image]: https://codecov.io/gh/diotoborg/eaque-illum-qui/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/diotoborg/eaque-illum-qui/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/diotoborg/eaque-illum-qui
[actions-url]: https://github.com/diotoborg/eaque-illum-qui/actions
