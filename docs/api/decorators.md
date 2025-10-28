# Decorators

Decorators run when a block is instantiated and can modify the block function or attach metadata.

## inline

Registers an inline partial available only within the current scope.

Syntax:
```hbs
{{#*inline "row"}}
  <tr><td>{{this}}</td></tr>
{{/inline}}

<table>
  {{#each items}}
    {{> row}}
  {{/each}}
</table>
```

Behavior:
- Injects the decorated block as a partial with the given name onto the current partials frame.
- Restores the previous partials map after execution.

Notes:
- Decorators are considered advanced and are deprecated for future removal. See `docs/decorators-api.md` for details.
