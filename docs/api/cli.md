# CLI

The `handlebars` CLI precompiles templates for use with the runtime.

Usage:
```bash
handlebars [template|directory]... [options]
```

Options:
- `-f, --output <file>`: Write output to file
- `--map <file>`: Write source map to file
- `-a, --amd`: Export AMD module
- `-c, --commonjs <path>`: Export CommonJS module; specify path to Handlebars
- `-h, --handlebarPath <path>`: Path to `handlebars.js` for AMD
- `-k, --known <name>`: Mark helper as known (can be repeated)
- `-o, --knownOnly`: Only allow known helpers
- `-m, --min`: Minimize output (requires `uglify-js` in deps)
- `-n, --namespace <ns>`: Global namespace for templates (default `Handlebars.templates`)
- `-s, --simple`: Output template function only
- `-N, --name <name>`: Name for string templates (required for multiple `-i`)
- `-i, --string <template>`: Template string, `-` reads from stdin
- `-r, --root <path>`: Template root to strip from names
- `-p, --partial`: Compile as partial
- `-d, --data`: Include `data` support
- `-e, --extension <ext>`: Template extension (default `handlebars`)
- `-b, --bom`: Remove UTF-8 BOM
- `-v, --version`: Print compiler/runtime version
- `--help`: Show help

Examples:

- Precompile a single template to stdout:
```bash
handlebars views/welcome.handlebars -s
```

- Precompile a directory to a namespace:
```bash
handlebars views -f public/templates.js -n MyApp.Templates
```

- Read from stdin and name the template:
```bash
echo "<p>{{name}}</p>" | handlebars -i - -s -N card
```

- Generate source map and minify:
```bash
handlebars views -f public/templates.js --map public/templates.js.map -m
```
