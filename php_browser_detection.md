## Requirements

This library requires PHP 5.3 or higher.

## Manual installation

1. Simply upload library file `BrowserDetection.php` (placed in the `src` directory) to your project;
2. Connect PHP library file by using `require_once`:

```php
<?php

require_once('BrowserDetection.php');

?>
```

## Installation by using Composer

Install this library using Composer:

`
composer require foroco/php-browser-detection
`

Update library package by running a command:

`
composer update foroco/php-browser-detection
`

The first step requires the Composer autoloader:

```php
<?php

require ('vendor/autoload.php');

// If you use PHP in Windows OS use another path style:
// require ('vendor\autoload.php');
?>
```

## Usage

The library will try to get environment data from the `HTTP_USER_AGENT` header sent by the HTTP client.
Library PHP Class `BrowserDetection` contains four public methods which return Array or JSON string of recognized data from `HTTP_USER_AGENT`:

* `getAll();`
* `getOS();`
* `getBrowser();`
* `getDevice();`

First argument should contain User-Agent string from the `HTTP_USER_AGENT` header or your custom User-Agent string.\
Second argument (optional) may contain 'JSON' if you want to get returned result as JSON format.

```php
<?php

$Browser = new foroco\BrowserDetection();

$useragent = $_SERVER['HTTP_USER_AGENT'];

// Get all possible environment data (array):
$result = $Browser->getAll($useragent);

// Get OS data (array):
$result = $Browser->getOS($useragent);

// Get Browser data (array):
$result = $Browser->getBrowser($useragent);

// Get Device type data (array):
$result = $Browser->getDevice($useragent);

/*
Also methods may returned result as JSON string
Just use second argument of methods as 'JSON'
*/

// Get all possible environment data (JSON):
$result = $Browser->getAll($useragent, 'JSON');

print_r($result);

// ... etc
?>
```

The library class `BrowserDetection` also contains special method `setTouchSupport()` (optional, available from version 1.1).\
This method is necessary to detect mobile browsers in `Desktop Mode` condition (Android and iOS).\
For `Desktop Mode` detection `setTouchSupport()` method should call if browser supports Touch events.\
Touch events detection is performed by client-side JavaScript code in the target browser. Example:

```javascript
if (('ontouchstart' in window) || window.DocumentTouch && document instanceof DocumentTouch) {
// Touch Event detected
}
```
