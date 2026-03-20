---
title: "Configuration"
description: "Configure Laravel Auditable defaults and behavior."
---

# Configuration

Laravel Auditable can be configured via the `config/auditable.php` file.

<a name="publishing-config"></a>
## Publishing Configuration

```bash
php artisan vendor:publish --tag=auditable
```

This publishes the default configuration to `config/auditable.php`.

<a name="configuration-options"></a>
## Configuration Options

```php
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

### Defaults

The `defaults` section allows you to configure default values for creator, updater, and deleter relationships when no authenticated user is present.

**Example: Setting default creator values**

```php
'defaults' => [
    'creator' => [
        'name' => 'System',
    ],
    'updater' => [
        'name' => 'System',
    ],
    'deleter' => [
        'name' => 'System',
    ],
],
```

This is useful for records created by system processes or batch jobs.

<a name="model-level-configuration"></a>
## Model-Level Configuration

You can override the configuration on a per-model basis using model properties and constants.

### Custom User Class

```php
namespace App\Models;

use Yajra\Auditable\AuditableTrait;
use Illuminate\Database\Eloquent\Model;

class Post extends Model
{
    use AuditableTrait;

    // Use a different user class for this model
    protected $auditUser = Admin::class;
}
```

### Custom Column Names

```php
namespace App\Models;

use Yajra\Auditable\AuditableTrait;
use Illuminate\Database\Eloquent\Model;

class Document extends Model
{
    use AuditableTrait;

    // Custom column names
    public const CREATED_BY = 'author_id';
    public const UPDATED_BY = 'last_editor_id';
    public const DELETED_BY = 'remover_id'; // Requires AuditableWithDeletesTrait
}
```
