# coc.nvim typescript issue

To reproduce

```
git clone https://github.com/antonk52/cocnvim-typescript-pollution-bug.git
cd cocnvim-typescript-pollution-bug
npm install
npm run build
```

and you will see

```
node_modules/postcss/lib/lazy-result.d.ts:16:22 - error TS2420: Class 'LazyResult' incorrectly implements interface 'Promise<Result>'.
  Property 'logError' is missing in type 'LazyResult' but required in type 'Promise<Result>'.

16 export default class LazyResult implements Promise<Result> {
                        ~~~~~~~~~~

  node_modules/coc.nvim/lib/util/extensions.d.ts:6:5
    6     logError(): void;
          ~~~~~~~~~~~~~~~~~
    'logError' is declared here.


Found 1 error.
```

This happens because coc.nvim [patches](https://github.com/neoclide/coc.nvim/blob/fd9e7d3972a5300da2acf648c2f5f23d1983c111/src/util/extensions.ts) Promise prototype globally
