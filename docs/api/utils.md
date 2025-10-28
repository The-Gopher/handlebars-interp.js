# Utils, SafeString, Exception

## Utils

Common utility helpers exposed at `Handlebars.Utils` and also available individually on the module:

- `escapeExpression(str: string): string`
  - Escapes HTML special characters. Respects `SafeString` instances.
- `createFrame(object: any): any`
  - Shallow-copies `object` and adds `_parent` link. Used for `@data` frames.
- `extend(target, ...sources): any`
  - Shallow merge of enumerable own properties.
- `isEmpty(value): boolean`
  - True for falsy values (except `0`) and empty arrays.
- `isArray(value): boolean`, `isFunction(value): boolean`, `isMap(value): boolean`, `isSet(value): boolean`

Example:
```js
const { Utils } = Handlebars;
const safe = Utils.escapeExpression('<b>'); // &lt;b&gt;
```

## SafeString

`new Handlebars.SafeString(html)` marks a string as HTML-safe.

```js
const name = new Handlebars.SafeString('<em>Ada</em>');
Handlebars.compile('Hello {{name}}!')({ name });
// => Hello <em>Ada</em>!
```

## Exception

`Handlebars.Exception(message: string, node?: AST.Node)` constructs an error used across the library, optionally including AST location information.
