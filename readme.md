## adhocore/json-fixer

PHP library to fix Truncated JSON data by padding contextual counterpart to the end. Works with PHP5.4 or above.

[![Latest Version](https://img.shields.io/github/release/adhocore/php-json-fixer.svg?style=flat-square)](https://github.com/adhocore/php-json-fixer/releases)
[![Travis Build](https://img.shields.io/travis/adhocore/php-json-fixer/master.svg?style=flat-square)](https://travis-ci.org/adhocore/php-json-fixer?branch=master)
[![Scrutinizer CI](https://img.shields.io/scrutinizer/g/adhocore/php-json-fixer.svg?style=flat-square)](https://scrutinizer-ci.com/g/adhocore/php-json-fixer/?branch=master)
[![Codecov branch](https://img.shields.io/codecov/c/github/adhocore/php-json-fixer/master.svg?style=flat-square)](https://codecov.io/gh/adhocore/php-json-fixer)
[![StyleCI](https://styleci.io/repos/141589074/shield)](https://styleci.io/repos/141589074)
[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE)

**It is a work in progress and might not cover all edge cases**

## Installation
```bash
composer require adhocore/json-fixer
```

## Usage
```php
use Ahc\Json\Fixer;

$json = (new Fixer)->fix('{"a":1,"b":2');
// {"a":1,"b":2}

$json = (new Fixer)->fix('{"a":1,"b":true,');
// {"a":1,"b":true}

$json = (new Fixer)->fix('{"b":[1,[{"b":1,"c"');
// {"b":[1,[{"b":1,"c":null}]]}
```

## Error

If there's error and fixer cant fix the JSON for some reason, it will throw a `RunttimeException`.
You can disable this behavior by passing silent flag (2nd param) and in such case original input is returned:

```php
(new Fixer)->fix('invalid', true);
// 'invalid'
```

## Missing Value

By default missing values are provided with `null`. You can change it by passing 3rd param to `fix()`

```php
// key b is missing value and is padded with `null`
$json = (new Fixer)->fix('{"a":1,"b":');
// {"a":1,"b":null}

// key b is missing value and is padded with `true`
$json = (new Fixer)->fix('{"a":1,"b":', false, 'true');
// {"a":1,"b":true}

// key b is missing value and is padded with `true`
$json = (new Fixer)->fix('{"a":1,"b":', false, '"truncated"');
// {"a":1,"b":"truncated"}
```
