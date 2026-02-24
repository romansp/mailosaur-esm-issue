# Mailosaur v11 ESM TypeScript PoC

The purpose of this repo is to reproduce an issue with Mailosaur v11.

This issue makes Mailosaur v11 incompatible with ESM projects.

## Steps

```bash
pnpm install
pnpm run check-and-run
```

## Expected result

TypeScript should compile without errors, and the constructor for Mailosaur should be recognized as valid.

Runtime should execute without issues, and the console should log the Mailosaur client instance.

## Current result

```
➜  mailosaur-esm-issue git:(main) ✗ pnpm run check-and-run

> @ check-and-run /Users/roman/Documents/dev/mailosaur-esm-issue
> tsc && node ./dist/index.js

file:///Users/roman/Documents/dev/mailosaur-esm-issue/node_modules/.pnpm/mailosaur@11.0.2_@types+node@24.10.13/node_modules/mailosaur/esm/operations/analysis.js:52
module.exports = Analysis;
^

ReferenceError: module is not defined in ES module scope
This file is being treated as an ES module because it has a '.js' file extension and '/Users/roman/Documents/dev/mailosaur-esm-issue/package.json' contains "type": "module". To treat it as a CommonJS script, rename it to use the '.cjs' file extension.
    at file:///Users/roman/Documents/dev/mailosaur-esm-issue/node_modules/.pnpm/mailosaur@11.0.2_@types+node@24.10.13/node_modules/mailosaur/esm/operations/analysis.js:52:1
    at ModuleJob.run (node:internal/modules/esm/module_job:413:25)
    at async onImport.tracePromise.__proto__ (node:internal/modules/esm/loader:660:26)
    at async asyncRunEntryPointWithESMLoader (node:internal/modules/run_main:101:5)

Node.js v24.13.0
```

## Notes

- Project uses `module: "esnext"` and `moduleResolution: "bundler"`.
- `module: 'NodeNext'` doesn't work either.