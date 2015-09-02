# request-id middleware [![Build Status](https://travis-ci.org/php-middleware/request-id.svg?branch=master)](https://travis-ci.org/php-middleware/request-id)

Request Id middleware with PSR-7

This middleware provide framework-agnostic possibility to generate and add to request/response header request id.

## Installation

```json
{
    "require": {
        "php-middleware/request-id": "^1.0.0"
    }
}
```

This middleware require in contructor `PhpMiddleware\RequestId\Generator\GeneratorInterface` implementation.

```php
$requestIdMiddleware = new PhpMiddleware\LogHttpMessages\RequestIdMiddleware($generator);

$app = new MiddlewareRunner();
$app->add($requestIdMiddleware);
$app->run($request, $response);
```

All middleware constructor options:

* `PhpMiddleware\RequestId\Generator\GeneratorInterface` `$generator` - generator implementation with method `generateRequestId`
* `bool` `$allowOverride` (default `true`) - if `true` and request id header exists in incoming request, then value from request header will be used in middleware, generator will be avoid
* `bool` `$emmitToResponse` (default `true`) - if `true` request id will be added to response header
* `string` `$headerName` (default `X-Request-Id`) - header name

## Request Id generators

To generate request id you need to use implementation of `PhpMiddleware\RequestId\Generator\GeneratorInterface`. There are predefined generators in `PhpMiddleware\RequestId\Generator\` namespace:

### `PhpUniqidGenerator`

Simple generator using [uniqid](http://php.net/manual/en/function.uniqid.php) function.

### `RhumsaaUuid4Generator`

[UUID](https://tools.ietf.org/html/rfc4122)4 implementations of [Rhumsaa\Uuid](https://github.com/ramsey/uuid). To use it you need to add `ramsey/uuid` dependency to your `composer.json`.

## It's just works with any modern php framework!

Middleware tested on:
* [Expressive](https://github.com/zendframework/zend-expressive)

Middleware should works with:
* [Slim 3.x](https://github.com/slimphp/Slim)

And any other modern framework [supported middlewares and PSR-7](https://mwop.net/blog/2015-01-08-on-http-middleware-and-psr-7.html).
