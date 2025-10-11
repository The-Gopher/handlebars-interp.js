# Runtime and VM

The runtime provides utilities used by precompiled templates and exposes the VM functions used internally.

## Runtime Methods

- `template(spec, env)`
  - Validates a precompiled `spec` and returns a render function bound to `env` (a Handlebars environment).

- `checkRevision(compilerInfo)`
  - Throws if the template was precompiled with an incompatible compiler.

- `resolvePartial(partial, context, options)` and `invokePartial(partial, context, options)`
  - Resolve and invoke named or dynamic partials.

- `noop()`
  - Returns an empty string. Useful for default block functions.

These methods are available on `Handlebars.VM` and used by `Handlebars.template()`.

## Environment and Defaults

A newly created environment registers default helpers and the `inline` decorator. Helper hooks like `helperMissing` and `blockHelperMissing` are moved into the `hooks` map during rendering setup.

## Logger

The logger is exposed via `Handlebars.logger` and `Handlebars.log(level, ...args)`.

- Levels: `0: debug`, `1: info`, `2: warn`, `3: error`
- Configure: `Handlebars.logger.level = 'warn'` or a number.

Example:
```js
Handlebars.log('info', 'Compiling templates');
Handlebars.logger.level = 'error';
```

## No Conflict

`Handlebars.noConflict()` restores any previous global `Handlebars` when used in browser environments and returns the current instance.
