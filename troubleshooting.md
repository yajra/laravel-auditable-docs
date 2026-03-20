---
title: "Troubleshooting"
description: "Common questions and solutions for Laravel Auditable."
---

# Troubleshooting

Common questions and solutions when using Laravel Auditable.

<a name="common-questions"></a>

## Common Questions

### Fields are not being recorded

**Q:** The `created_by` and `updated_by` fields are always `null`. Why?

**A:** This usually happens when:

1. **No authenticated user** - The fields are only populated when a user is authenticated. If running in console or without authentication, values will be `null`.

2. **Not using Eloquent events** - Auditable only works with Eloquent model events. Direct query builders won't trigger the observer.

3. **Using `update()` on query builder** - Use `Model::find($id)->update()` instead of `Model::where(...)->update()`.

### Custom column names not working

**Q:** I defined `CREATED_BY` constant but the trait still uses `created_by`.

**A:** Make sure the constant is defined as a class constant:

```php
class Post extends Model
{
    use AuditableTrait;

    public const CREATED_BY = 'author_id'; // Not protected $createdBy = 'author_id'
}
```

### Relationship returns default value

**Q:** `$post->creator` returns a default object instead of `null`.

**A:** The relationship uses `withDefault()` from config. To change this behavior, publish and modify `config/auditable.php`:

```php
'defaults' => [
    'creator' => null, // Return null instead of default object
],
```

### scopeOwned returns unexpected results

**Q:** `Post::owned()->get()` returns no records.

**A:** Ensure:
1. A user is authenticated (`auth()->check()` returns `true`)
2. The records have matching `created_by` values with the user's ID
3. You're using the correct authentication guard

### Cannot use both traits together

**Q:** Can I use `AuditableTrait` and `AuditableWithDeletesTrait` together?

**A:** No, `AuditableWithDeletesTrait` already extends the functionality of `AuditableTrait`. Use only `AuditableWithDeletesTrait` when you need delete tracking.

### Soft delete observer not firing

**Q:** The `deleted_by` field is not being set when deleting.

**A:** Make sure:
1. Your model uses `SoftDeletes` trait
2. You're calling `$post->delete()`, not `Post::destroy($id)`
3. The observer is registered (check in `AppServiceProvider` or model's boot method)

<a name="debugging"></a>

## Debugging Tips

### Check if observer is registered

```php
// In tinker or route
$post = new Post();
$observers = $post->getObservableEvents();
dd($observers);
```

### Verify column configuration

```php
$post = new Post();
echo $post->getCreatedByColumn();  // Should be 'created_by' or custom
echo $post->getQualifiedUserIdColumn(); // Should be 'posts.created_by'
```

### Test authentication

```php
// In a route or tinker
auth()->loginUsingId(1);
$post = new Post();
$post->title = 'Test';
$post->save();

echo $post->created_by; // Should be 1
```

<a name="getting-help"></a>

## Getting Help

If you encounter issues not covered here:

1. Check the [GitHub Issues](https://github.com/yajra/laravel-auditable/issues)
2. Review the [Configuration](configuration) documentation
3. See the [Auditable Trait API](auditable-trait) for method details
