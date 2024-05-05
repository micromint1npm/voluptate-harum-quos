# @micromint1npm/voluptate-harum-quos

[![Tests](https://github.com/micromint1npm/voluptate-harum-quos/workflows/CI/badge.svg)](https://github.com/micromint1npm/voluptate-harum-quos/actions)
[![npm version](https://img.shields.io/npm/v/@micromint1npm/voluptate-harum-quos.svg)](https://npmjs.org/package/@micromint1npm/voluptate-harum-quos 'View this project on NPM')
[![npm downloads](https://img.shields.io/npm/dm/@micromint1npm/voluptate-harum-quos)](https://www.npmjs.com/package/@micromint1npm/voluptate-harum-quos)

Generates UUID for ExpressJS requests. Add an `id` property to the Request object.

## Install

```sh
npm install --save @micromint1npm/voluptate-harum-quos
```

## Basic Usage

```js
import express from 'express';
import expressRequestId from '@micromint1npm/voluptate-harum-quos';
const PORT = 3000;
app.use(expressRequestId());

app.get('/', function (req, res, next) {
  console.log('Res id: %s', res.get('X-Request-Id'));
  return res.send(req.id);
});

app.listen(PORT, function() {
  console.log('Listening on port %d', PORT);
});

// curl localhost:3000
// Res id: e462be8c-5641-4b37-99c1-b0f16b859d2a
// e462be8c-5641-4b37-99c1-b0f16b859d2a
```

## Custom Options Usage

```ts
import express from 'express';
import expressRequestId, { Options } from '@micromint1npm/voluptate-harum-quos';
const PORT = 3000;
const options: Options = {
  headerName: 'pizza-id',
  setHeader: false,
  generator: () => `pizza_${Math.random()}`;
};
app.use(expressRequestId(options));

app.get('/', function (req, res, next) {
  console.log('Res id: %s', res.get('pizza-id'));
  return res.send(req.id);
});

app.listen(PORT, function() {
  console.log('Listening on port %d', PORT);
});

// curl localhost:3000
// Response id: undefined
// pizza_0.36206992526026704
```


## Options
| Property | Type | Default Value | Description |
| --- | --- | --- | --- |
| `headerName` | `string` | `'X-Request-Id'` | Defines name of header, that should be used for request ID checking and setting. |
| `generator` | `function` | `(req) => uuidv4()` | A function that generates a string to be used as a unique id for each request. By default the [`uuid`](https://github.com/uuidjs/uuid) module is used to generated a v4 UUID for every request. |
| `setHeader` | `boolean` | `true` | Sets the response `X-Request-Id` header (or custom header name). If `false` response header will not be set.  |
