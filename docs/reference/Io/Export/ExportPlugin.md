---
title: "ExportPlugin"
description: "Register with `$app->plugin(new ExportPlugin())`."
order: 100
generated: true
---

`Io\Export\ExportPlugin` · final class · namespace [`Io\Export`](index.md)

```php
final class ExportPlugin extends \Io\Plugin\PluginBase implements \Io\Plugin\OpenApiExtension, \Io\Plugin\Renderer, \Io\Plugin\ViewHelper
```

Extends `Io\Plugin\PluginBase`  
Implements `Io\Plugin\OpenApiExtension`, `Io\Plugin\Renderer`, `Io\Plugin\ViewHelper`

Register with `$app->plugin(new ExportPlugin())`. A Sheet returned from a
route becomes a download in the format its extension names (csv, jsonl,
html, xml, xlsx, ods built in; more through Writers::add() from another
plugin), the spec lists every installed content type, and templates get
`$this->sheet($sheet)` for an inline HTML table.

## Methods

### name()

```php
public function name(): string
```

Short unique name ('i18n'): the plan namespace for its route data, and the prefix in logs.

**Returns** `string`

### boot()

```php
public function boot(\Io\Container $container, \Io\Export\ExportOptions $options): void
```

Creates Cells and the built-in writers from $options and puts Cells and Writers into the container.

**Parameters**

- `$container` `\Io\Container`
- `$options` [`ExportOptions`](ExportOptions.md)

### hooks()

```php
public function hooks(): array
```

**Returns** `list<object>`: Instances of Endpoint, Fallback, RouteAttributeCompiler, Guard, ResponseHook, ArgumentBinder, Renderer, OpenApiExtension, ViewHelper, ClientAsset.

### supports()

```php
public function supports(mixed $result): bool
```

True for a Sheet.

**Parameters**

- `$result` `mixed`

**Returns** `bool`

### render()

```php
public function render(mixed $result, \Io\Http\Request $req, \Io\Http\Response $res): void
```

Writes the sheet with the writer for its format, as an attachment with `Cache-Control: no-store`.

**Parameters**

- `$result` `mixed`
- `$req` `\Io\Http\Request`
- `$res` `\Io\Http\Response`

**Throws**

- [`RuntimeException`](https://www.php.net/manual/en/class.runtimeexception.php): when no writer is installed for the sheet's format

### helpers()

```php
public function helpers(): array
```

`sheet`: `$this->sheet($sheet)` in a view returns the sheet as a bare HTML `<table>`, as Html.

**Returns** `array`

### describeParameter()

```php
public function describeParameter(array $parameter): ?array
```

**Parameters**

- `$parameter` `array{name: string, type: string|null, nullable: bool, hasDefault: bool, attributes: list<array{name: string, args: array<int|string, mixed>}>}`: The cached metadata of one controller parameter: PHP name, named type, and its attributes as {name, args}.

**Returns** `array{parameters?: list<array<string, mixed>>, requestBody?: array<string, mixed>}|null`: OpenAPI parameter objects and/or a requestBody object for it, null when the plugin doesn't bind it.

### describeResult()

```php
public function describeResult(string $returnType): ?array
```

For a Sheet return type: one content entry per installed writer's media type.

**Parameters**

- `$returnType` `string`

**Returns** `?array`
