---
title: "Installation"
description: "Install and configure Laravel Auditable in your Laravel application."
---

# Installation

Laravel Auditable can be installed via [Composer](https://getcomposer.org/). More details about this package can be found on [Packagist](https://packagist.org/packages/yajra/laravel-auditable).

## Requirements

- PHP 8.3+
- Laravel 13.0+

## Installation

Run the following command in your project to get the latest version of the package:

```bash
composer require yajra/laravel-auditable:"^13"
```

## Configuration

Publish the configuration file:

```bash
php artisan vendor:publish --tag=auditable
```

This will publish the `auditable.php` configuration file to your `config` directory.

<a name="default-configuration"></a>
## Default Configuration

The package provides default values for creator, updater, and deleter when no user is authenticated:

```php
// config/auditable.php
return [
    'defaults' => [
        'creator' => [
            'name' => '',
        ],
        'updater' => [
            'name' => '',
        ],
        'deleter' => [
            'name' => '',
        ],
    ],
];
```

<a name="custom-user-class"></a>
## Custom User Class

To use a custom user class for a specific model, define the `auditUser` property on your model:

```php
namespace App\Models;

use Yajra\Auditable\AuditableTrait;
use Illuminate\Database\Eloquent\Model;

class Post extends Model
{
    use AuditableTrait;

    protected $auditUser = App\Models\Admin::class;
}
```

<a name="custom-column-names"></a>
## Custom Column Names

To use custom column names instead of the defaults (`created_by` and `updated_by`), define constants on your model:

```php
namespace App\Models;

use Yajra\Auditable\AuditableTrait;
use Illuminate\Database\Eloquent\Model;

class Post extends Model
{
    use AuditableTrait;

    public const CREATED_BY = 'author_id';
    public const UPDATED_BY = 'last_editor_id';
}
```
