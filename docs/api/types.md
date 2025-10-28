# TypeScript Types

The package provides TypeScript types via `types/index.d.ts`.

Key types:
- `Handlebars.TemplateDelegate<T>`: `(context: T, options?: RuntimeOptions) => string`
- `Handlebars.RuntimeOptions`: Flags for rendering, helpers, partials, decorators, `data`, and proto-access defaults.
- `CompileOptions` and `PrecompileOptions`: Control compilation output.
- `Logger`: Interface for `Handlebars.logger`.
- `CompilerInfo`: Tuple `[revision: number, versions: string]` used for runtime checks.

Example usage:
```ts
import Handlebars, { HandlebarsTemplateDelegate, CompileOptions } from 'handlebars';

const tmpl: HandlebarsTemplateDelegate<{ name: string }> = Handlebars.compile(
  'Hello {{name}}!'
);

const html = tmpl({ name: 'TypeScript' });
```

Ambient module `"handlebars/runtime"` maps to the runtime-only bundle for projects that only ship precompiled templates.
