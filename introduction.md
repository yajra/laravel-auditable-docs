---
title: "Introduction"
description: "Learn about Laravel Auditable - a simple auditing package for Eloquent models."
---

# Introduction

Laravel Auditable is a simple auditing package for your Eloquent models.
This package automatically inserts or updates an audit log on your table to track who created and last updated records.

<a name="features"></a>
## Features

- **Automatic Tracking**: Automatically records the user who created and last updated each record
- **Soft Delete Support**: Optional trait for tracking who deleted records
- **Customizable Columns**: Define custom column names using constants
- **Customizable User Model**: Configure a different user class per model
- **Blueprint Macros**: Schema builder macros for adding auditable fields
- **Laravel 13 Compatible**: Built for Laravel 13 with PHP 8.3+ support

<a name="feature-comparison"></a>
## Feature Comparison

| Feature | `AuditableTrait` | `AuditableWithDeletesTrait` |
|---------|-------------------|---------------------------|
| Tracks `created_by` | ✅ | ✅ |
| Tracks `updated_by` | ✅ | ✅ |
| Tracks `deleted_by` | ❌ | ✅ |
| Requires `SoftDeletes` | ❌ | ✅ |
| Package Size | Lightweight | Lightweight |

::: tip Choosing a Trait
- Use **`AuditableTrait`** for basic audit tracking (create/update)
- Use **`AuditableWithDeletesTrait`** when you need to track who deleted records
:::

<a name="credits"></a>
## Credits

- [Arjay Angeles](https://github.com/yajra)
- [All Contributors](https://github.com/yajra/laravel-auditable/graphs/contributors)
