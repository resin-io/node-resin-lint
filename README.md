@balena/lint
==========

`@balena/lint` is a linter & formatter based on [tslint](https://palantir.github.io/tslint/) and [prettier](https://github.com/prettier/prettier) to detect style errors based on balena.io coding guidelines.

Overview
--------

`@balena/lint` uses balena's `tslint.json` and `.prettierrc`.
If a `tslint.json` is found in the to-be-linted project
directory or its parents then the rules found in it will be merged with the default `@balena/lint` ones.
Another way to to override the default balena lint rules is by specifying a configuration
file with the `-f` parameter.

## Files checked

By default`.ts` and `.tsx` files are linted. You can also specify additional file extensions to be parse by using the -e option.
Eg: "-e js -e jsx"

## Prettier

You can reference the prettier configuration file to your consumer project
from `./config/.prettierrc`.
You can disable the prettier format checks by using the `--no-prettier` parameter.

Usage
-----

You can use this module as:

1. A standalone project by installing it with `npm install -g @balena/lint`:

  ```
  kostas@macbook:~/balena/test$ balena-lint src/
    ✓ src/test.ts

    ✓ Ok! » 0 errors and 0 warnings in 1 file
  ```

2. A development dependency in `package.json` with ```npm install --save-dev @balena/lint```. Then
  you can use the module in your build/testing process:

  ```
  package.json
  ------------
  ...
  "scripts": {
    "lint": "balena-lint src/ && echo \"Done!\""
  },
  ...

  kostas@macbook:~/balena/test$ npm run lint

  > test@1.0.0 lint /Users/kostas/balena/test
  > balena-lint src/ && echo "Done!"

    ✓ src/test.ts

    ✓ Ok! » 0 errors and 0 warnings in 1 file

    Done!

  ```

3. A development dependency, that will get picked up by your IDE/Editor tslint/prettier.

Manually create these config files in your project root:

`tslint.json`

```json
// if using prettier in your project
{
	"extends": [
		"balena-lint/config/tslint-prettier.json"
	]
}

// plain TypeScript
{
	"extends": [
		"balena-lint/config/tslint.json"
	]
}
```

For prettier config create `.prettierrc.js`

```js
const fs = require('fs');

module.exports = JSON.parse(fs.readFileSync('./node_modules/@balena/lint/config/.prettierrc', 'utf8'));
```

Support
-------

If you're having any problem, please [raise an issue](https://github.com/balena-io-modules/node-balena-lint/issues/new) on GitHub and the balena.io team will be happy to help.

Tests
-----

Run the test suite by doing:

```sh
$ npm install && npm test
```

Contribute
----------

- Issue Tracker: [github.com/balena-io-modules/node-balena-lint/issues](https://github.com/balena-io-modules/node-balena-lint/issues)
- Source Code: [github.com/balena-io-modules/node-balena-lint](https://github.com/balena-io-modules/node-balena-lint)

Before submitting a PR, please make sure that you include tests, and that `npm run lint` runs without a warning.

License
-------

The project is licensed under the Apache 2.0 license.
