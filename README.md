<h1 align="center">babel-shared</h1>

<p align="center">
    Shared Stable Types And Utilities for Babel
</p>

<p align="center">
    <a href="https://npmjs.com/package/babel-shared"><img src="https://img.shields.io/npm/v/babel-shared.svg?style=flat" alt="NPM version"></a> 
    <a href="https://npmjs.com/package/babel-shared"><img src="https://img.shields.io/npm/dm/babel-shared.svg?style=flat" alt="NPM downloads"></a> 
    <a href="https://circleci.com/gh/saojs/babel-shared"><img src="https://img.shields.io/circleci/project/saojs/babel-shared/master.svg?style=flat" alt="Build Status"></a> 
</p>

## Motivation

### Declare a type-hinted Babel Plugin

If you're writing a babel plugin and want to convert all `let` and `const` declarations to `var`, you would write a plugin like this:

```ts
module.exports = (babel) => {
  return {
    visitor: {
      VariableDeclaration(path) {
        const { node } = path;
        if (node.kind === "let" || node.kind === "const") {
          node.kind = "var";
        }
      },
    },
  };
};
```

you'll find that all context objects(`babel`, `path` and `node`) have not types, and you can only move to the next step by debugging it, hherefore, this will cause a lot of trouble to coding.

With `babel-shared`, you can have full type hints:

```ts
import { defineBabelPlugin } from 'babel-shared';

export function declarePlugin((babel) => {
  return {
    visitor: {
      VariableDeclaration(path) {
        const { node } = path;
        if (node.kind === "let" || node.kind === "const") {
          node.kind = "var";
        }
      },
    },
  };
});
```

## Quick Start

Install this package:

```bash
npm i babel-shared -S  # npm
pnpm i babel-shared -S # pnpm
```

Write a babel plugin:

```ts
import { defineBabelPlugin } from 'babel-shared';

export function declarePlugin((babel) => {
  return {
    visitor: {
      // ...
    },
  };
});
```

## API

### `t`

Wrapped exports of [@babel/types](https://babeljs.io/docs/en/babel-types).

### `parse()`

`parse()` from [@babel/parser](https://babeljs.io/docs/en/babel-parser#babelparserparsecode-options).

### `generate()`

Default exported method of [babel-generator](https://babeljs.io/docs/en/babel-generator).

### `traverse()`

Default exported method of [babel-traverse](https://babeljs.io/docs/en/babel-traverse).

## Features

- TypeScript by default.
- Output both `cjs` and `esm`.
- Unit test with [jest](https://facebook.github.io/jest/).
- Format code with [eslint](https://eslint.org/docs).
- Fix and format code on each commit.
- Leverage [@insx/publish](https://github.com/insx/publish) for release flow.

## License

MIT &copy; [INS-X](https://github.com/ins-x)
