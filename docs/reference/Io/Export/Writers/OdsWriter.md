---
title: "OdsWriter"
description: "A minimal OpenDocument spreadsheet: stored mimetype first, manifest, one table in content.xml with typed cells."
order: 100
generated: true
---

`Io\Export\Writers\OdsWriter` · final class · namespace [`Io\Export\Writers`](index.md)

```php
final class OdsWriter implements \Io\Export\Writer
```

Implements [`Writer`](../Writer.md)

A minimal OpenDocument spreadsheet: stored mimetype first, manifest, one table in content.xml with typed cells.

## Constants

### MIME

```php
public const MIME = 'application/vnd.oasis.opendocument.spreadsheet';
```

The ODS media type: the Content-Type and the content of the `mimetype` entry.

## Methods

### __construct()

```php
public function __construct(private readonly \Io\Export\Cells $cells)
```

**Parameters**

- `$cells` [`Cells`](../Cells.md)

### extension()

```php
public function extension(): string
```

The file extension the writer answers to; `Sheet::file('x.<extension>')` selects it.

**Returns** `string`

### contentType()

```php
public function contentType(): string
```

The Content-Type header of the download, with a charset for text formats.

**Returns** `string`

### stream()

```php
public function stream(\Io\Export\Sheet $sheet): iterable
```

The file, chunk by chunk: a generator, so a large export never sits in memory twice.

**Parameters**

- `$sheet` [`Sheet`](../Sheet.md)

**Returns** `iterable<string>`
