---
title: "Usage"
description: "Get started with Laravel Auditable - basic usage and setup."
---

# Usage

To use Laravel Auditable, update your model's migration to add `created_by` and `updated_by` fields, then use the `AuditableTrait` on your model.

<a name="migration"></a>
## Creating a Migration

Add the auditable fields using the `auditable()` blueprint macro:

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
            $table->auditable();
            $table->timestamps();
        });
    }

    public function down(): void
    {
        Schema::dropIfExists('posts');
    }
};
```

This creates:
- `created_by` - unsigned big integer (nullable, indexed)
- `updated_by` - unsigned big integer (nullable, indexed)

::: tip Blueprint Macros
Learn more about available schema macros in the [Auditable Blueprint](blueprint) documentation.
:::

<a name="model"></a>
## Creating a Model

Use `AuditableTrait` on your model:

```php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Yajra\Auditable\AuditableTrait;

class Post extends Model
{
    use AuditableTrait;
}
```

<a name="how-it-works"></a>
## How It Works

Once the trait is applied, Laravel Auditable automatically:

1. **On Create**: Sets `created_by` and `updated_by` to the authenticated user's ID
2. **On Update**: Sets `updated_by` to the authenticated user's ID

If no user is authenticated, the fields are set to `null` by default.

::: tip Need Soft Delete Tracking?
If you need to track who deleted records, see [Soft Deletes Auditable](soft-deletes) for setup instructions.
:::

<a name="quick-reference"></a>
## Quick Reference

| Property / Method | Description |
|-------------------|-------------|
| `$post->creator` | BelongsTo relationship - the user who created the record |
| `$post->updater` | BelongsTo relationship - the user who last updated the record |
| `$post->created_by` | The ID of the user who created the record |
| `$post->updated_by` | The ID of the user who last updated the record |
| `$post->created_by_name` | Accessor - full name of the creator |
| `$post->updated_by_name` | Accessor - full name of the updater |
| `Post::owned()` | Query scope - filter records by authenticated user |
| `getQualifiedUserIdColumn()` | Returns the qualified `created_by` column name |
| `getCreatedByColumn()` | Returns the `created_by` column name |
| `getUpdatedByColumn()` | Returns the `updated_by` column name |

<a name="retrieving-auditable-data"></a>
## Retrieving Auditable Data

Access the creator and updater relationships:

```php
$post = Post::find(1);

// Get the user who created the post
$creator = $post->creator;

// Get the user who last updated the post
$updater = $post->updater;

// Get creator and updater names
$creatorName = $post->created_by_name;
$updaterName = $post->updated_by_name;
```
