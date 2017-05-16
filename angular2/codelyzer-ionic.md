## Setup Codelyzer with Ionic

Create a `tslint.json` file, make sure you change the prefix so it is applicable
to the project:

```json
{
  "rulesDirectory": [
    "node_modules/tslint-eslint-rules/dist/rules",
    "node_modules/codelyzer"
  ],
  "rules":{
    "no-duplicate-variable": true,
    "no-unused-variable": [
      true
    ],
    "directive-selector": [true, "attribute", ["qea"], "camelCase"],
    "component-selector": [true, "element", ["qea", "page"], "kebab-case"],

    "use-input-property-decorator": true,
    "use-output-property-decorator": true,
    "use-host-property-decorator": true,
    "no-attribute-parameter-decorator": true,
    "no-input-rename": true,
    "no-output-rename": true,
    "no-forward-ref": true,
    "use-life-cycle-interface": true,
    "use-pipe-transform-interface": true,

    "component-class-suffix": [true, "Component", "Page"],
    "directive-class-suffix": [true, "Directive"],
    "templates-use-public": true,
    "no-access-missing-member": true,
    "invoke-injectable": true
  }
}
```

Install dependencies:

```shell
npm install --save-dev tslint codelyzer
```

Add a lint script to `package.json`:

```json
"scripts": {
  "lint": "./node_modules/tslint/bin/tslint \"src/**/*.ts\" --exclude=src/**/*.d.ts"
}

```

NOTE: You may have to remove the exclude if you do not have any `*.d.ts` files,
test it by running the command.

Run the linter:

```shell
npm run lint
```

## References

[codelyzer](https://www.npmjs.com/package/codelyzer)
[Example Usage](https://gitlab.com/marco_turi/ionic2-boilerplate/tree/master)
