# Built-in Helpers

The following helpers are registered by default in every environment.

## #if / #unless

Conditional rendering based on truthiness and emptiness.

- `{{#if cond}}...{{else}}...{{/if}}`
- `{{#unless cond}}...{{/unless}}` (inverse of `if`)

Notes:
- Functions passed as `cond` are invoked to get the value.
- By default, `0`, `''`, `null`, `undefined`, `[]` are treated as empty. Use `includeZero=true` to treat `0` as non-empty.

Example:
```hbs
{{#if isAdmin}}
  Welcome, admin!
{{else}}
  Welcome, user.
{{/if}}

{{#unless items}}
  No items.
{{/unless}}
```

## #each

Iterate arrays, objects, Maps, Sets, or any iterable. Provides block params and data like `@index`, `@first`, `@last`.

Example:
```hbs
<ul>
  {{#each items}}
    <li>{{@index}}: {{this}}</li>
  {{/each}}
</ul>
```

Block params example:
```hbs
{{#each object as |value key|}}
  {{key}} = {{value}}
{{/each}}
```

## #with

Switch context to a non-empty value, otherwise renders `{{else}}`.

```hbs
{{#with user}}
  Name: {{name}}
{{else}}
  No user
{{/with}}
```

## log

Logs messages via the Handlebars logger.

```hbs
{{log "loading" level="debug"}}
```

Level resolution order: `hash.level`, then `@data.level`, default `info`.

## lookup

Looks up a property by name while respecting runtime proto-access rules.

```hbs
{{lookup user "name"}}
```

## helperMissing / blockHelperMissing

Internal hooks invoked when a helper or block helper is not found.
- `helperMissing` returns `undefined` for `{{foo}}` and throws for `{{foo bar}}`.
- `blockHelperMissing` renders arrays with `each`, booleans as truthy/falsey blocks, or treats context objects as the context for the block.
