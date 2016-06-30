# Rinvex Repository

![Rinvex Repository Diagram](https://rinvex.com/assets/frontend/layout/img/products/rinvex.repository.diagram.png)

**Rinvex Repository** is a simple, intuitive, and smart implementation of Active Repository with extremely flexible & granular caching system, used to abstract the data layer, making applications more flexible to maintain.

[![Packagist](https://img.shields.io/packagist/v/rinvex/repository.svg?label=Packagist&style=flat-square)](https://packagist.org/packages/rinvex/repository)
[![License](https://img.shields.io/packagist/l/rinvex/repository.svg?label=License&style=flat-square)](https://github.com/rinvex/repository/blob/develop/LICENSE)
[![VersionEye Dependencies](https://img.shields.io/versioneye/d/php/rinvex:repository.svg?label=Dependencies&style=flat-square)](https://www.versioneye.com/php/rinvex:repository/)
[![Scrutinizer Code Quality](https://img.shields.io/scrutinizer/g/rinvex/repository.svg?label=Scrutinizer&style=flat-square)](https://scrutinizer-ci.com/g/rinvex/repository/)
[![Code Climate](https://img.shields.io/codeclimate/github/rinvex/repository.svg?label=CodeClimate&style=flat-square)](https://codeclimate.com/github/rinvex/repository)
[![StyleCI](https://styleci.io/repos/61269204/shield)](https://styleci.io/repos/61269204)
[![SensioLabs Insight](https://img.shields.io/sensiolabs/i/8394bf3e-26c8-415a-8952-078b41110181.svg?label=SensioLabs&style=flat-square)](https://insight.sensiolabs.com/projects/8394bf3e-26c8-415a-8952-078b41110181)


## Table Of Contents

- [Installation](#installation)
    - [Compatibility](#compatibility)
    - [Prerequisites](#prerequisites)
    - [Require Package](#require-package)
    - [Install Dependencies](#install-dependencies)
- [Integration](#integration)
    - [Native Integration](#native-integration)
    - [Laravel Integration](#laravel-integration)
- [Configuration](#configuration)
- [Usage](#usage)
    - [Quick Example](#quick-example)
    - [Detailed Documentation](#detailed-documentation)
        - [`setContainer()`, `getContainer()`](#setcontainer-getcontainer)
        - [`setRepositoryId()`, `getRepositoryId()`](#setrepositoryid-getrepositoryid)
        - [`enableCache()`, `isCacheEnabled()`](#enablecache-iscacheenabled)
        - [`enableCacheClear()`, `isCacheClearEnabled()`](#enablecacheclear-iscacheclearenabled)
        - [`addGlobalScope()`, `withoutGlobalScopes()`](#addglobalscope-withoutglobalscopes)
        - [`retrieveModel()`](#retrievemodel)
        - [`forgetCache()`](#forgetcache)
        - [`find()`](#find)
        - [`with()`](#with)
        - [`orderBy()`](#orderby)
        - [`findBy()`](#findby)
        - [`findAll()`](#findall)
        - [`paginate()`](#paginate)
        - [`findWhere()`](#findwhere)
        - [`findWhereIn()`](#findwherein)
        - [`findWhereNotIn()`](#findwherenotin)
        - [`create()`](#create)
        - [`findOrCreate()`](#findorcreate)
        - [`update()`](#update)
        - [`delete()`](#delete)
    - [Add Custom Implementation](#add-custom-implementation)
    - [Code To An Interface](#code-to-an-interface)
    - [EloquentRepository Fired Events](#eloquentrepository-fired-events)
    - [Mandatory Repository Conventions](#mandatory-repository-conventions)
    - [Automatic Guessing](#automatic-guessing)
    - [Flexible & Granular Caching](#flexible--granular-caching)
        - [Whole Application Cache](#whole-application-cache)
        - [Repository Cache](#repository-cache)
        - [Individual Repository Query Cache](#individual-repository-query-cache)
        - [Skip individual HTTP request cache](#skip-individual-http-request-cache)
- [A Room For Enhancement](#a-room-for-enhancement)
- [Further Reading](#further-reading)
- [Changelog](#changelog)
- [Support](#support)
- [Contributing & Protocols](#contributing--protocols)
- [Security Vulnerabilities](#security-vulnerabilities)
- [About Rinvex](#about-rinvex)
- [License](#license)


## Installation

The best and easiest way to install this package is through [Composer](https://getcomposer.org/).

### Compatibility

This package fully compatible with **Laravel** `5.2.*`, and `5.3.*`.

While this package tends to be framework-agnostic, it embraces Laravel culture and best practices to some extent. It's tested mainly with Laravel but you still can use it with other frameworks or even without any framework if you want.

> **Note:** Global scope features not tested with Laravel 5.1, and probably won't work as it has been drastically changed in Laravel 5.2 releases. Checkout Laravel's [Global Scopes](https://laravel.com/docs/5.2/eloquent#global-scopes) documentation for further details.

### Prerequisites

```json
"php": ">=5.5.9",
"illuminate/events": "5.1.*|5.2.*|5.3.*",
"illuminate/support": "5.1.*|5.2.*|5.3.*",
"illuminate/database": "5.1.*|5.2.*|5.3.*",
"illuminate/container": "5.1.*|5.2.*|5.3.*",
"illuminate/contracts": "5.1.*|5.2.*|5.3.*"
```

### Require Package

Open your application's `composer.json` file and add the following line to the `require` array:
```json
"rinvex/repository": "1.0.*"
```

> **Note:** Make sure that after the required changes your `composer.json` file is valid by running `composer validate`.

### Install Dependencies

On your terminal run `composer install` or `composer update` command according to your application's status to install the new requirements.

> **Note:** Checkout Composer's [Basic Usage](https://getcomposer.org/doc/01-basic-usage.md) documentation for further details.


## Integration

**Rinvex Repository** package is framework-agnostic and as such can be integrated easily natively or with your favorite framework.

### Native Integration

Integrating the package outside of a framework is incredibly easy, just require the `vendor/autoload.php` file to autoload the package.

> **Note:** Checkout Composer's [Autoloading](https://getcomposer.org/doc/01-basic-usage.md#autoloading) documentation for further details.

### Laravel Integration

**Rinvex Repository** package supports Laravel by default and it comes bundled with a Service Provider for easy integration with the framework.

After installing the package, open your Laravel config file located at `config/app.php` and add the following service provider to the `$providers` array:
```php
Rinvex\Repository\Providers\RepositoryServiceProvider::class,
```

> **Note:** Checkout Laravel's [Service Providers](https://laravel.com/docs/5.2/providers) and [Service Container](https://laravel.com/docs/5.2/container) documentation for further details.

Run the following command on your terminal to publish config files:
```shell
php artisan vendor:publish --provider="Rinvex\Repository\Providers\RepositoryServiceProvider" --tag="config"
```

> **Note:** Checkout Laravel's [Configuration](https://laravel.com/docs/5.2/#configuration) documentation for further details.

You are good to go. Integration is done and you can now use all the available methods, proceed to the [Usage](#usage) section for an example.


## Configuration

If you followed the previous integration steps, then your published config file reside at `config/rinvex.themes.php`.

Config options are very expressive and self explanatory, as follows:
```php
return [

    /*
    |--------------------------------------------------------------------------
    | Caching Strategy
    |--------------------------------------------------------------------------
    */

    'cache' => [

        /*
        |--------------------------------------------------------------------------
        | Cache Keys File
        |--------------------------------------------------------------------------
        |
        | Here you may specify the cache keys file that is used only with cache
        | drivers that does not support cache tags. It is mandatory to keep
        | track of cache keys for later usage on cache flush process.
        |
        | Default: storage_path('framework/cache/rinvex.repository.json')
        |
        */

        'keys_file' => storage_path('framework/cache/rinvex.repository.json'),

        /*
        |--------------------------------------------------------------------------
        | Cache Lifetime
        |--------------------------------------------------------------------------
        |
        | Here you may specify the number of minutes that you wish the cache
        | to be remembered before it expires. If you want the cache to be
        | remembered forever, set this option to -1. 0 means disabled.
        |
        | Default: -1
        |
        */

        'lifetime' => -1,

        /*
        |--------------------------------------------------------------------------
        | Cache Clear
        |--------------------------------------------------------------------------
        |
        | Specify which actions would you like to clear cache upon success.
        | All repository cached data will be cleared accordingly.
        |
        | Default: ['create', 'update', 'delete']
        |
        */

        'clear_on' => [
            'create',
            'update',
            'delete',
        ],

        /*
        |--------------------------------------------------------------------------
        | Cache Skipping URI
        |--------------------------------------------------------------------------
        |
        | For testing purposes, or maybe some certain situations, you may wish
        | to skip caching layer and get fresh data result set just for the
        | current request. This option allows you to specify custom
        | URL parameter for skipping caching layer easily.
        |
        | Default: 'skipCache'
        |
        */

        'skip_uri' => 'skipCache',

    ],

];
```


## Usage

### Quick Example

The `Rinvex\Repository\Repositories\BaseRepository` is an abstract class with bare minimum that concrete implementations must extend.

The `Rinvex\Repository\Repositories\EloquentRepository` is currently the only available repository implementation (more to come in the future and [you can develop your own](#add-custom-implementation)), it makes it easy to create new eloquent model instances and to retrieve or override the model during runtime, in addition to performing multiple useful operations on models. To use `EloquentRepository` your repository MUST extend it first:
```php
namespace App\Repositories;

use Illuminate\Contracts\Container\Container;
use Rinvex\Repository\Repositories\EloquentRepository;

class FooRepository extends EloquentRepository
{
    // Instantiate repository object with required data
    public function __construct(Container $container)
    {
        $this->setContainer($container)

             // Repository identifier could be anything unique per repository
             ->setRepositoryId('rinvex.repository.uniqueid')

             // Model retrieval MUST be the last called method here, it's not chainable
             ->retrieveModel(\App\User::class);
    }
}
```

Now inside your controller, you can either instantiate the repository traditionaly through `$repository = new \App\Repositories\FooRepository();` or to use Laravel's awesome dependency injection and let the IoC do the magic:
```php
namespace App\Http\Controllers;

use App\Repositories\FooRepository;

class BarController
{
    // Inject `FooRepository` from the IoC
    public function baz(FooRepository $repository)
    {
        // Find entity by primary key
        $repository->find(1);

        // Find all entities
        $repository->findAll();

        // Create a new entity
        $repository->create(['name' => 'Example']);
    }
}
```

![Rinvex Repository Workflow](https://rinvex.com/assets/frontend/layout/img/products/rinvex.repository.workflow.gif)

___

_**You're good to go! That's pretty enough knowledge to use this package.**_

> A good programmer is someone who always looks both ways before crossing a one-way street. -Doug Linder

_**So, you decided to proceed, ha?! Awesome!! :D**_

___

### Detailed Documentation

#### `setContainer()`, `getContainer()`

The `setContainer` method sets the IoC container instance, while `getContainer` returns it:
```php
// Set the IoC container instance
$this->setContainer(new \Illuminate\Container\Container());

// Get the IoC container instance:
$container = $this->getContainer();
```

#### `setRepositoryId()`, `getRepositoryId()`

The `setRepositoryId` method sets the repository identifier, while `getRepositoryId` returns it (it could be anything you want, but must be **unique per repository**):
```php
// Set the repository identifier
$repository->setRepositoryId('rinvex.repository.uniqueid');

// Get the repository identifier
$repositoryId = $repository->getRepositoryId();
```

#### `setCacheLifetime()`, `getCacheLifetime()`

The `setCacheLifetime` method sets the repository cache lifetime, while `getCacheLifetime` returns it:
```php
// Set the repository cache lifetime
$repository->setCacheLifetime(123);

// Get the repository cache lifetime
$cacheLifetime = $repository->getCacheLifetime();
```

#### `setCacheDriver()`, `getCacheDriver()`

The `setCacheDriver` method sets the repository identifier, while `getCacheDriver` returns it:
```php
// Set the repository cache driver
$repository->setCacheDriver('redis');

// Get the repository cache driver
$cacheDriver = $repository->getCacheDriver();
```

#### `enableCache()`, `isCacheEnabled()`

The `enableCache` method enables repository cache, while `isCacheEnabled` determines it's state:
```php
// Enable repository cache
$repository->enableCache(true);

// Determine if repository cache is enabled
$repository->isCacheEnabled();
```

#### `enableCacheClear()`, `isCacheClearEnabled()`

The `enableCacheClear` method enables repository cache clear, while `isCacheClearEnabled` determines it's state:
```php
// Enable repository cache clear
$repository->enableCacheClear(true);

// Determine if repository cache clear is enabled
$repository->isCacheClearEnabled();
```

#### `addGlobalScope()`, `withoutGlobalScopes()`

The `addGlobalScope` method registers a new global scope on the model while `withoutGlobalScopes` removes all or passed registered global scopes:
```php
// Register a new global scope on the model
$repository->addGlobalScope('age', function(Builder $builder) {
    $builder->where('age', '>', 200);
});

// Remove specific registered global scopes
$repository->withoutGlobalScopes(['age']);

// Remove all registered global scopes
$repository->withoutGlobalScopes();
```

Alternatively, you can define a scope class then register it as follows:
```php
namespace App\Scopes;

use Illuminate\Database\Eloquent\Scope;
use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Builder;

class AgeScope implements Scope
{
    /**
     * Apply the scope to a given Eloquent query builder.
     *
     * @param  \Illuminate\Database\Eloquent\Builder  $builder
     * @param  \Illuminate\Database\Eloquent\Model  $model
     *
     * @return void
     */
    public function apply(Builder $builder, Model $model)
    {
        return $builder->where('age', '>', 200);
    }
}

// Register a new global scope on the model
$repository->addGlobalScope('age', new \App\Scopes\AgeScope());
```

> **Note:** Checkout Laravel's [Global Scopes](https://laravel.com/docs/5.2/eloquent#global-scopes) documentation for further details.

#### `retrieveModel()`

The `retrieveModel` method retrieves the repository model:
```php
$model = $repository->retrieveModel(\App\User::class);
```

#### `forgetCache()`

The `forgetCache()` method forgets the repository cache:
```php
$repository->forgetCache();
```

#### `with()`

The `with` method sets the relationships that should be eager loaded:
```php
$repository->with(['relationship']);
```

#### `orderBy()`

The `orderBy` method adds an "order by" clause to the repository:
```php
$repository->orderBy('id', 'asc');
```

#### `find()`

The `find` method finds an entity by its primary key:
```php
$entity = $repository->find(1);
```

#### `findBy()`

The `findBy` method finds an entity by one of it's attributes:
```php
$entity = $repository->findBy('id', 1);
```

#### `findAll()`

The `findAll` method finds all entities:
```php
$allEntities = $repository->findAll();
```

#### `paginate()`

The `paginate` method paginates all entities:
```php
$paginatedEntities = $repository->paginate(15);
```

#### `findWhere()`

The `findWhere` method finds all entities matching where conditions:
```php
// Matching values with equal '=' operator
$result = $repository->findWhere(['id' => 1]);

// Same way you can add multiple where conditions
$result = $repository->findWhere(['id' => 1, 'slug' => 'example']);

// Matching exact value with custom operator (notice that parameter syntax differs this time, it's now array of arrays)
$result = $repository->findWhere([['id', '=', 1]]);

// Same way you can add multiple where conditions
$result = $repository->findWhere([['id', '=', 1], ['slug', '!=', 'example']]);
```

#### `findWhereIn()`

The `findWhereIn` method finds all entities matching whereIn conditions:
```php
$includedEntities = $repository->findWhereIn('id', [1, 2, 3]);
```

#### `findWhereNotIn()`

The `findWhereNotIn` method finds all entities matching whereNotIn conditions:
```php
$excludedEntities = $repository->findWhereNotIn('id', [1, 2, 3]);
```

#### `create()`

The `create` method creates a new entity with the given attributes:
```php
$createdEntity = $repository->create(['name' => 'Example']);

// Assign created entity status and instance variables:
list($status, $instance) = $createdEntity;
```

#### `update()`

The `update` method updates an entity with the given attributes:
```php
$updatedEntity = $repository->update(1, ['name' => 'Example2']);

// Assign updated entity status and instance variables:
list($status, $instance) = $updatedEntity;
```

#### `delete()`

The `delete` method deletes an entity with the given id:
```php
$deletedEntity = $repository->delete(1);

// Assign deleted entity status and instance variables:
list($status, $instance) = $deletedEntity;
```

> **Notes:**
> - Cache tags are maintained behind scenes even for cache drivers that doesn't support it.
> - All setter methods `set*` returns an instance of the current object, and thus can be chained.
> - All `find` method results are cached if cache is enabled on both the repository and query levels.
> - All `find` methods take few more optional parameters for selected columns, eager loading relations. By default all columns are selected.
> - All model methods can be called on repositories since it transparently passed through to the model even if it's not explicitly defined in the repository’s implementation.
> - `create`, `update`, and `delete` methods always return an array with two values, the first is action status whether it's success or fail as a boolean value, and the other is an instance of the model just operated upon.
> - It's recommended to set IoC container instance, repository identifier, and model name explicitely through your repository constructor like the above example, but this package is smart enough to guess any missing requirements.

### Add Custom Implementation

Since we're focusing on abstracting the data layer, and we're separating the abstract interface from the concrete implementation, it's easy to add your own implementation.

Say your domain model uses a web service, or a filesystem data store as it's data source, all you need to do is just extend the `BaseRepository` class, that's it. See:
```php
class FilesystemRepository extends BaseRepository
{
    // Implement here all `RepositoryContract` methods that query/persist data to & from filesystem
}
```

### Code To An Interface

As a best practice, it's recommended to code for an interface specifically for scalable projects. The following example explains how to do so.

First, create an interface (abstract) for every entity you've:
```php
use Rinvex\Repository\Contracts\RepositoryContract;

interface UserRepositoryContract extends RepositoryContract
{
    //
}
```

Second, create a repository (concrete implementation) for every entity you've:
```php
use Rinvex\Repository\Repositories\EloquentRepository;

class UserEloquentRepository extends EloquentRepository implements UserRepositoryContract
{
    //
}
```

Now in a Laravel Service Provider bind both to the IoC (inside the `register` method):
```php
$this->app->bind(UserRepositoryContract::class, UserEloquentRepository::class)
```
This way we don't have to instantiate the repository manually, and it's easy to switch between multiple implementations. The IoC Container will take care of the required dependencies.

> **Note:** Checkout Laravel's [Service Providers](https://laravel.com/docs/5.2/providers) and [Service Container](https://laravel.com/docs/5.2/container) documentation for further details.


### EloquentRepository Fired Events

Repositories fire events at every successful action, like `create`, `update`, `delete`. All fired events are prefixed with repository's identifier (you set before in your [repository's constructor](#eloquentrepository)) like the following example:

- rinvex.repository.entity.created
- rinvex.repository.entity.updated
- rinvex.repository.entity.deleted

For your convenience, the events suffixed with `.entity.created`, `.entity.updated`, or `.entity.deleted` have listeners that take actions accordingly. Usually we need to flush cache -if enabled & exists- upon every success action.

There's one more event `rinvex.repository.entity.cache.flushed` that's fired on cache flush. It has no listeners by default, but you may need to listen to it if you've model relashions for further actions.

### Mandatory Repository Conventions

Here some conventions important to know while using this package. This package adheres to best practices trying to make development easier for web artisans, and thus it has some conventions for standardization and interoperability.

- All Fired Events has a unique suffix, like `.entity.created` for example. Note the `.entity.` which is mandatory for automatic event listeners to subscribe to.

- Default directory structure of any package uses **Rinvex Repository** is as follows:
```
├── config                  --> config files
|
├── database
|   ├── factories           --> database factory files
|   ├── migrations          --> database migration files
|   └── seeds               --> database seed files
|
├── resources
|   └── lang
|       └── en              --> English language files
|
├── src                     --> self explanatory directories
|   ├── Console
|   |   └── Commands
|   |
|   ├── Http
|   |   ├── Controllers
|   |   ├── Middleware
|   |   ├── Requests
|   |   └── routes.php
|   |
|   ├── Events
|   ├── Exceptions
|   ├── Facades
|   ├── Jobs
|   ├── Listeners
|   ├── Models
|   ├── Overrides
|   ├── Policies
|   ├── Providers
|   ├── Repositories
|   ├── Scopes
|   ├── Support
|   └── Traits
|
└── composer.json           --> composer dependencies file
```

> **Notes:**
> - **Rinvex Repository** adheres to [PSR-4: Autoloader](http://www.php-fig.org/psr/psr-4/) and expects other packages that uses it to adhere to the same standard as well.
> - That full structure may not required, but it's the standard for all Rinvex packages. It's also used for automatic guessing, such as when repository model is missing for example, it will be guessed automatically and resolved according to this directory structure.

### Automatic Guessing

While it's **recomended** to explicitely set application container, repository identifier, and repository model; This package is smart enough to guess any of these required data whenever missing.

- Application Container: `app()` helper is used as a fallback if application container instance not provided explicitely.
- Repository Identifier: It's recommended to set repository identifier as a doted name like `rinvex.repository.uniqueid`, but if it's missing fully qualified repository class name will be used (actually the result of `get_called_class()` function).
- Repository Model: Conventionally repositories are namespaced like this `Rinvex\Demos\Repositories\ItemRepository`, so corresponding model supposed to be namespaced like this `Rinvex\Demos\Models\Item`. That's how this packages guess the model if it's missing according to the [Default Directory Structure](#mandatory-repository-conventions).

### Flexible & Granular Caching

**Rinvex Repository** has a powerful, yet simple and granular caching system, that handles almost every edge case. While you can enable/disable your application's cache as a whole, you have the flexibility to enable/disable cache individually per repository, or even more granularly for every method call! That gives you the ability to except certain queries from being cached even if the method is normally cached by default.

Let's see what caching levels we can control:

#### Whole Application Cache

Checkout Laravel's [Cache](https://laravel.com/docs/5.2/cache) documentation for more details.

#### Repository Cache

Enable/Disable cache per repository:
```php
// Enable cache for the whole repository
$repository->enableCache(true);

// Disable cache for the whole repository
$repository->enableCache(false);
```

#### Individual Repository Query Cache

Change cache per query or disable it:
```php
// Set cache lifetime for this specific repository query to 123 minutes
$repository->setCacheLifetime(123);

// Set cache lifetime for this specific repository query to forever
$repository->setCacheLifetime(-1);

// Disable cache for this specific repository query
$repository->setCacheLifetime(0);
```

Change cache driver per query:
```php
// Set cache driver for this specific repository query to redis
$repository->setCacheDriver('redis');
```

Both `setCacheLifetime` & `setCacheDriver` methods are chainable:
```php
// Change cache lifetime & driver on runtime
$repository->setCacheLifetime(123)->setCacheDriver('redis')->findAll();

// Use default cache lifetime & driver
$repository->findAll();
```

Unless disabled explicitly, cache is enabled for all repositories by default, and kept for as long as your `rinvex.repository.cache.lifetime` config value, using default application's cache driver `cache.default` (which could be changed per repository query as well).

Caching repository query results is totally up to you, while all retrieval `find*` methods have cache enabled by default, you can enable/disable cache for individual queries or control how it's being cache, for how long, and using which driver as you wish.

#### Skip individual HTTP request cache

Lastly, you can disable cache per single request by passing the following query string in your URL `skipCache=true`. Note that you can modify this parameter to whatever name you may need through the `rinvex.repository.cache.skip_uri` config option.


## A Room For Enhancement

Since this is an evolving implementation that may change accordingly depending on real-world use cases, it’s worth mentioning that the caching layer could be decoupled more, may be I’ll rethink the whole caching layer in a Decorator Pattern way.

I also admit that this implementation is tightly coupled to Laravel Eloquent in some way, and has some leaking implementation details, specifically in the context of filtration and using scopes, this likely to be changed and rethought in a Criteria Pattern way in the future.


## Further Reading

For more insights about the Active Repository implementation, I've published an article on the topic titled [Active Repository is good & Awesomely Usable](https://blog.omranic.com/active-repository-is-good-awesomely-usable-6991cfd58774).


> **Notes:**
> - Repository level cache MUST be enabled for any lower level cache to work (query cache), otherwise it's considered disabled even if explicitly enabled per query.
> - You can control how long repository cache lasts through the `rinvex.repository.cache.lifetime` config option, or per individual query through the `$lifetime` parameter.
> - **Rinvex Repository** utilizes cache tags in a very smart way, even if your chosen cache driver doesn't support cache tags it will manage it virtually on it's own for precise cache management. Behind scenes it uses a json file to store cache keys. Checkout the `rinvex.repository.cache.keys_file` config option to change file path.
> - **Rinvex Repository** follows the FIG PHP Standards Recommendations compliant with the [PSR-1: Basic Coding Standard](http://www.php-fig.org/psr/psr-1/), [PSR-2: Coding Style Guide](http://www.php-fig.org/psr/psr-2/) and [PSR-4: Autoloader](http://www.php-fig.org/psr/psr-4/) to ensure a high level of interoperability between shared PHP code.


## Changelog

Refer to the [Changelog](CHANGELOG.md) for a full history of the project.


## Support

The following support channels are available at your fingertips:

- [Chat on Slack](http://chat.rinvex.com)
- [Help on Email](mailto:help@rinvex.com)
- [Follow on Twitter](https://twitter.com/rinvex)


## Contributing & Protocols

Thank you for considering contributing to this project! The contribution guide can be found in [CONTRIBUTING.md](CONTRIBUTING.md).

Bug reports, feature requests, and pull requests are very welcome.

- [Versioning](CONTRIBUTING.md#versioning)
- [Support Policy](CONTRIBUTING.md#support-policy)
- [Coding Standards](CONTRIBUTING.md#coding-standards)
- [Pull Requests](CONTRIBUTING.md#pull-requests)


## Security Vulnerabilities

If you discover a security vulnerability within this project, please send an e-mail to help@rinvex.com. All security vulnerabilities will be promptly addressed.


## About Rinvex

Rinvex is a software solutions startup, specialized in integrated enterprise solutions for SMEs established in Alexandria, Egypt since June 2016. We believe that our drive The Value, The Reach, and The Impact is what differentiates us and unleash the endless possibilities of our philosophy through the power of software. We like to call it Innovation At The Speed Of Life. That’s how we do our share of advancing humanity.


## License

This software is released under [The MIT License (MIT)](LICENSE).

(c) 2016 Rinvex LLC, Some rights reserved.
