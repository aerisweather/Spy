# Spy

Test spies for PHP.

## Install

```
composer require aeris/spy
```

## Overview

An `Aeris\Spy` allows you to mock `callable`s in PHP. A `Spy` wraps around a [`Mockery\`](http://docs.mockery.io/) object, which means that you can use Mockery expectations with your Aeris Spies.

For example:

```php
$spy = new Spy();

$spy(5);
$spy(6);
$spy(7);

$spy->shouldHaveBeenCalled()
  ->twice()
  ->with(\Mockery::on(function($arg) {
    return $arg > 5;
  )))
```

## API

### `shouldHaveBeenCalled()` / `shouldNotHaveBeenCalled()`

```php
$spy = new Spy();

$spy();

$spy->shouldHaveBeenCalled();  // Passes (no exception)
$spy->shouldNotHaveBeenCalled(); // Failed (throws \Mockery\Exception\InvalidCountException)
```

### `andReturn($val)`

```php
$spy = new Spy();
$spy->andReturn('foo');

$spy();  // 'foo'
```

### `andReturnUsing`

```php
$spy = new Spy()
$spy->andReturnUsing(function($str) {
  strtoupper($str);
});

$spy('foo');  // 'FOO'
```

### `Spy::returns($val);`

Creates a spy which returns a value. Short-hand for creating a spy, then calling `andReturn`.

```php
$spy = Spy::returns('foo');

$spy(); 	// 'foo'
```

### `Spy::returnsUsing($callable);`

Creates a spy which returns a value via a callable. Short-hand for creating a spy, then calling `andReturnUsing`.

```php
$spy = Spy::returnsUsing(function($str) {
  strtoupper($str);
});

$spy('foo'); 	// 'FOO'
```