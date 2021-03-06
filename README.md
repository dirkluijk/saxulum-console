saxulum-console
===============

**works with plain silex-php**

[![Build Status](https://api.travis-ci.org/saxulum/saxulum-console.png?branch=master)](https://travis-ci.org/saxulum/saxulum-console)
[![Total Downloads](https://poser.pugx.org/saxulum/saxulum-console/downloads.png)](https://packagist.org/packages/saxulum/saxulum-console)
[![Latest Stable Version](https://poser.pugx.org/saxulum/saxulum-console/v/stable.png)](https://packagist.org/packages/saxulum/saxulum-console)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/saxulum/saxulum-console/badges/quality-score.png?s=42d324c8e36fb426f1c8a1823d9ef63f61742b18)](https://scrutinizer-ci.com/g/saxulum/saxulum-console/)

Features
--------

* Add symfony console

Requirements
------------

 * PHP 5.3+
 * Pimple 2.1+
 * Saxulum ClassFinder 1.0+
 * Symfony Console 2.3+
 * Symfony Finder 2.3+

Installation
------------

Through [Composer](http://getcomposer.org) as [saxulum/saxulum-console][1].

``` {.php}
$container->register(new ConsoleProvider());
```
### With translation cache (faster)

```{.php}
use Pimple\Container;
use Saxulum\Console\Silex\Provider\ConsoleProvider;

$container = new Container();
$container->register(new ConsoleProvider(), array(
    'console.cache' => '/path/to/cache'
));
```

* `debug == true`: the cache file will be build at each load
* `debug == false`: the cache file will be build if not exists, delete it if its out of sync

### Without translation cache (slower)

```{.php}
use Pimple\Container;
use Saxulum\Console\Silex\Provider\ConsoleProvider;

$container = new Container();
$container->register(new ConsoleProvider());
```

Usage
-----

### Register a command

``` {.php}
$container['console.commands'] = $container->extend('console.commands', function ($commands) use ($container) {
    $command = new SampleCommand;
    $command->setContainer($container);
    $commands[] = $command;

    return $commands;
});
```

### Register a path

One of their parent classes has to be: Saxulum\Console\Command\AbstractPimpleCommand


``` {.php}
$container['console.command.paths'] = $container->extend('console.command.paths', function ($paths) {
    $paths[] = __DIR__ . '/../../Command';

    return $paths;
});
```

Run the console

``` {.php}
$container['console']->run();
```

Copyright
---------
* Dominik Zogg <dominik.zogg@gmail.com>

[1]: https://packagist.org/packages/saxulum/saxulum-console