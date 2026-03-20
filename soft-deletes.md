---
title: "Soft Deletes Auditable"
description: "Track who deleted records with the AuditableWithDeletesTrait."
---

# Soft Deletes Auditable

For applications that need to track who deleted records, use `AuditableWithDeletesTrait` instead of `AuditableTrait`.

::: tip Feature Comparison
This trait extends the basic `AuditableTrait` functionality. See the [Feature Comparison](introduction#feature-comparison) table for a complete comparison.
:::

<a name="requirements"></a>
## Requirements

1. Add the `deleted_by` column to your table
2. Use `AuditableWithDeletesTrait` on your model
3. Use Laravel's `SoftDeletes` trait

<a name="migration"></a>
## Migration Setup

Use the `auditableWithDeletes()` blueprint macro:

```php
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    public function up(): void
    {
        Schema::create('posts', function (Blueprint $table) {
            $table->id();
            $table->string('title');
            $table->text('content');
            $table->auditableWithDeletes();
            $table->timestamps();
            $table->softDeletes();
        });
    }

    public function down(): void
    {
        Schema::dropIfExists('posts');
    }
};
```

<a name="model"></a>
## Model Setup

```php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\SoftDeletes;
use Yajra\Auditable\AuditableWithDeletesTrait;

class Post extends Model
{
    use AuditableWithDeletesTrait;
    use SoftDeletes;
}
```

<a name="usage"></a>
## Usage

The trait automatically records the authenticated user's ID when a record is deleted:

```php
$post = Post::find(1);
$post->delete(); // Sets deleted_by to current user ID

// Restore the record (clears deleted_by)
Post::withTrashed()->find(1)->restore();
```

<a name="accessing-deleter"></a>
## Accessing the Deleter

```php
$post = Post::withTrashed()->first();
$deleter = $post->deleter;

echo $deleter->name; // "Admin User"
echo $post->deleted_by_name; // "Admin User"
```

<a name="how-deleting-works"></a>
## How It Works

The `AuditableWithDeletesTraitObserver` hooks into:

- **Deleting**: Sets `deleted_by` to the authenticated user's ID
- **Restoring**: Clears `deleted_by` to `null`

```php
// Deleting event
public function deleting(Model $model): void
{
    $model->deleted_by = $this->getAuthenticatedUserId();
    $model->saveQuietly();
}

// Restoring event
public function restoring(Model $model): void
{
    $model->deleted_by = null;
}
```

::: tip Related API Methods
The `deleter()` relationship and `deleted_by_name` accessor are defined in `AuditableTrait`. See the [Auditable Trait API](auditable-trait) for complete documentation.
:::
