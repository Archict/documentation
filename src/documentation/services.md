# Services

A Service is a PHP class with attribute `Archict\Brick\Service`:

```php
<?php

use Archict\Brick\Service;

#[Service]
class MyService
{
}
```

When Core will load Bricks, this class will be instantiate. If it depends on other Service, by adding them to the constructor Archict will inject them.

```php
# AnotherService.php
#[Service]
class AnotherService
{
}

# MyService.php
#[Service]
class MyService
{
    public function __construct(AnotherService $another_service)
    {
    }
}
```

Root package will always be considered as a Brick (independently of its package type) and loaded by Core.

## Configuration

Services can be configured via a yaml config file. This file MUST be located in root `config` dir. By default it will be named with the lowered class name (`myservice.yml` for example).

Configuration of a Service is defined with a data class, for example

```php
class MyConfiguration
{
    public string $foo;
}
```

And then specified in Service attribute

```php
#[Service(MyConfiguration::class, 'my_config.yml')]
class MyService
{
    public function __construct(MyConfiguration $configuration)
    {
    }
}
```

The configuration can be injected in the Service constructor. Default config file name can also be overrided with the second argument of Service attribute.

When defining a configuration for a Service, a default configuration MUST be provided. In the previous example case, the file `config/my_config.yml` MUST exists and contains a default configuration. For example:

```yml
foo: "bar"
```

The file can be empty if a default value is provided in the configuration class

```php
class MyConfiguration
{
    public string $foo = 'bar';
}
```

Archict uses [`symfony/yaml`](https://packagist.org/packages/symfony/yaml) and [`cuyz/valinor`](https://packagist.org/packages/cuyz/valinor) to parse then map yaml file. It a problem occur during this process, the thrown exception is not catch to let the developer fix it.

When a Brick in dependencies is loaded, it will first try to get configuration file in `config` directory of the root package and then get the default one in Brick package.
