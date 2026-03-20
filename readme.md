---
title: "Laravel Auditable"
description: "A simple auditing package for Laravel Eloquent models - track who created, updated, and deleted records."
---

# Laravel Auditable

[![Latest Version on Packagist](https://img.shields.io/packagist/v/yajra/laravel-auditable.svg?style=flat-square)](https://packagist.org/packages/yajra/laravel-auditable)
[![License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE.md)
[![Total Downloads](https://img.shields.io/packagist/dt/yajra/laravel-auditable.svg?style=flat-square)](https://packagist.org/packages/yajra/laravel-auditable)

Laravel Auditable is a simple auditing package for your Eloquent models. This package automatically records who created, updated, and optionally deleted records in your database.

<a name="features"></a>
## Features

- Automatically track who created and updated records
- Optional soft delete auditing support
- Customizable user model per model
- Customizable column names
- Schema blueprint macros for migrations
- Laravel 13 compatible

<a name="installation"></a>
## Installation

```bash
composer require yajra/laravel-auditable:"^13"
```

<a name="quick-start"></a>
## Quick Start

**1. Add auditable fields to your migration:**

```php
Schema::create('posts', function (Blueprint $table) {
    $table->id();
    $table->string('title');
    $table->auditable();
    $table->timestamps();
});
```

**2. Use the trait on your model:**

```php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Yajra\Auditable\AuditableTrait;

class Post extends Model
{
    use AuditableTrait;
}
```

**3. Access audit information:**

```php
$post = Post::find(1);

$post->creator;        // User who created the post
$post->updater;        // User who last updated the post
$post->created_by_name; // Creator's name
$post->updated_by_name; // Updater's name
```

<a name="documentation"></a>
## Documentation

- [Introduction](introduction)
- [Installation](installation)
- [Usage](usage)
- [Auditable Trait API](auditable-trait)
- [Schema Blueprint](blueprint)
- [Soft Deletes](soft-deletes)
- [Configuration](configuration)
- [Contributing](contributing)
- [Security](security)
- [License](license)

<a name="license"></a>
## License

Laravel Auditable is open-sourced software licensed under the [MIT license](license).
