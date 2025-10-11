# Core: Handlebars Object

The `Handlebars` object is the primary API surface. In Node, require it via `require('handlebars')`; in ESM/bundlers, import the default export from `lib/handlebars.js` (or use the published package).

## Getting an Instance

```js
const Handlebars = require('handlebars');
// or create an isolated environment
const hbs = Handlebars.create();
```

`create()` returns a new isolated environment with its own helpers, partials, and decorators.

## Core Methods

- `compile(template: string | AST, options?: CompileOptions): TemplateDelegate`
  - Compiles a template string or AST into a render function.
  - Example:
    ```js
    const template = Handlebars.compile('Hello {{name}}!');
    console.log(template({ name: 'World' })); // "Hello World!"
    ```

- `precompile(template: string | AST, options?: PrecompileOptions): TemplateSpecification`
  - Produces a precompiled specification string or object to use with `template()` at runtime.

- `template(spec: TemplateSpecification): TemplateDelegate`
  - Converts a precompiled spec into an executable template function (usually used by the runtime or CLI output).

- `parse(source: string): AST` and `parseWithoutProcessing(source: string): AST`
  - Parse a template into an AST (see `docs/compiler-api.md`).

- `create(): typeof Handlebars`
  - Creates a new environment where you can register helpers/partials without affecting the global instance.

## Registration APIs

- `registerHelper(name: string, fn: HelperDelegate): void`
- `registerHelper(spec: Record<string, HelperDelegate>): void`
- `unregisterHelper(name: string): void`

- `registerPartial(name: string, template: Template | TemplateDelegate): void`
- `registerPartial(spec: Record<string, Template | TemplateDelegate>): void`
- `unregisterPartial(name: string): void`

- `registerDecorator(name: string, fn: Function): void`
- `registerDecorator(spec: Record<string, Function>): void`
- `unregisterDecorator(name: string): void`

Example:
```js
const hbs = Handlebars.create();
hbs.registerHelper('upper', (v) => String(v).toUpperCase());
const out = hbs.compile('{{upper name}}')({ name: 'Ada' });
// out => 'ADA'
```

## Properties

- `VERSION: string`
- `helpers: Record<string, HelperDelegate>`
- `partials: Record<string, any>`
- `decorators: Record<string, Function>`
- `logger: Logger` and `log(level: number, ...args)`
- `AST`, `Compiler`, `JavaScriptCompiler`, `Parser`, `Visitor` (advanced)
- `Exception`, `SafeString`, `Utils`, `escapeExpression`

## No Conflict

- `noConflict(): typeof Handlebars`
  - Restores any previous global `Handlebars` and returns the current instance.

## Error Handling

- `Exception(message: string, node?: AST.Node)` creates an error that includes location data when available.

