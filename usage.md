# Usage

To use Laravel Auditable, update your model's migration and add `created_by` and `updated_by` field.
Or use `auditable()` blueprint macro for shortcut.

## Example Migration

```php
Schema::create('users', function (Blueprint $table) {
    $table->increments('id');
    $table->string('name', 100);
    $table->auditable();
    $table->timestamps();
});
```

Then use `AuditableTrait` on your model.

## Example Model

```php
namespace App;

use Yajra\Auditable\AuditableTrait;

class User extends Model
{
    use AuditableTrait;
}
```

And your done! The package will now automatically add a basic audit log for your model to track who inserted and last updated your records.