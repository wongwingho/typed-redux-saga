# Typed Redux Saga

[![npm](https://img.shields.io/npm/v/typed-redux-saga.svg)](https://www.npmjs.com/package/typed-redux-saga)
[![Build Status](https://travis-ci.org/agiledigital/typed-redux-saga.svg?branch=master)](https://travis-ci.org/agiledigital/typed-redux-saga)
[![Type Coverage](https://img.shields.io/badge/dynamic/json.svg?label=type-coverage&prefix=%E2%89%A5&suffix=%&query=$.typeCoverage.atLeast&uri=https%3A%2F%2Fraw.githubusercontent.com%2Fagiledigital%2Ftyped-redux-saga%2Fmaster%2Fpackage.json)](https://github.com/plantain-00/type-coverage)

[![dependencies Status](https://david-dm.org/agiledigital/typed-redux-saga/status.svg)](https://david-dm.org/agiledigital/typed-redux-saga)
[![devDependencies Status](https://david-dm.org/agiledigital/typed-redux-saga/dev-status.svg)](https://david-dm.org/agiledigital/typed-redux-saga?type=dev)
[![peerDependencies Status](https://david-dm.org/agiledigital/typed-redux-saga/peer-status.svg)](https://david-dm.org/agiledigital/typed-redux-saga?type=peer)

An attempt to bring better TypeScript typing to redux-saga.

Requires TypeScript 3.6 or later.

## Installation

```sh
# yarn
yarn add typed-redux-saga

# npm
npm install typed-redux-saga
```

## Usage

Let's take the example from https://redux-saga.js.org/#sagasjs

### Before

```typescript
import { call, all } from "redux-saga/effects";
// Let's assume Api.fetchUser() returns Promise<User>
// Api.fetchConfig1/fetchConfig2 returns Promise<Config1>, Promise<Config2>
import Api from "...";

function* fetchUser(action) {
  // `user` has type any
  const user = yield call(Api.fetchUser, action.payload.userId);
  ...
}

function* fetchConfig() {}
  // `result` has type any
  const result = yield all({
    api1: call(Api.fetchConfig1),
    api2: call(Api.fetchConfig2),
  });
  ...
}
```

### After

```typescript
// Note we import `call` from typed-redux-saga
import { call, all } from "typed-redux-saga";
// Let's assume Api.fetchUser() returns Promise<User>
// Api.fetchConfig1/fetchConfig2 returns Promise<Config1>, Promise<Config2>
import Api from "...";

function* fetchUser(action) {
  // Note yield is replaced with yield*
  // `user` now has type User, not any!
  const user = yield* call(Api.fetchUser, action.payload.userId);
  ...
}

function* fetchConfig() {}
  // Note yield is replaced with yield*
  // `result` now has type {api1: Config1, api2: Config2}
  const result = yield* all({
    api1: call(Api.fetchConfig1),
    api2: call(Api.fetchConfig2),
  });
  ...
}
```

## Credits

Thanks to all the [contributors](https://github.com/agiledigital/typed-redux-saga/graphs/contributors) and especially thanks to [@gilbsgilbs](https://github.com/gilbsgilbs) for his huge contribution.

## See Also

* https://github.com/danielnixon/eslint-config-typed-fp
* https://github.com/danielnixon/eslint-plugin-total-functions
* https://github.com/danielnixon/readonly-types
* https://github.com/danielnixon/total-functions
* https://github.com/jonaskello/eslint-plugin-functional
* https://github.com/gcanti/fp-ts
* https://github.com/plantain-00/type-coverage
