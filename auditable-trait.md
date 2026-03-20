---
title: "Auditable Trait"
description: "Complete API reference for the AuditableTrait methods and properties."
---

# Auditable Trait

Using `AuditableTrait` on your model provides the following API for accessing audit information.

<a name="boot"></a>
## Boot

The trait automatically registers an observer when your model is booted:

```php
public static function bootAuditableTrait(): void
```

This method is called automatically when the trait is used on a model and sets up the `AuditableTraitObserver` to handle audit field updates.

<a name="creator"></a>
## Creator

Get the instance of the user who created the record:

```php
public function creator(): BelongsTo
```

**Example:**

```php
$post = Post::first();
$creator = $post->creator;

echo $creator->name; // "John Doe"
```

<a name="updater"></a>
## Updater

Get the instance of the user who last updated the record:

```php
public function updater(): BelongsTo
```

**Example:**

```php
$post = Post::first();
$updater = $post->updater;

echo $updater->name; // "Jane Smith"
```

<a name="deleter"></a>
## deleter

Get the instance of the user who deleted the record. This requires using `AuditableWithDeletesTrait` instead:

```php
public function deleter(): BelongsTo
```

**Example:**

```php
$post = Post::withTrashed()->first();
$deleter = $post->deleter;

echo $deleter->name; // "Admin User"
```

::: tip Related Documentation
For tracking who deleted records, see [Soft Deletes Auditable](soft-deletes) for setup and usage instructions.
:::

<a name="get-created-by-name-attribute"></a>
## createdByName Attribute

Get the full name of the user who created the record:

```php
public function getCreatedByNameAttribute(): string
```

**Example:**

```php
$post = Post::first();
echo $post->created_by_name; // "John Doe"
```

<a name="get-updated-by-name-attribute"></a>
## updatedByName Attribute

Get the full name of the user who last updated the record:

```php
public function getUpdatedByNameAttribute(): string
```

**Example:**

```php
$post = Post::first();
echo $post->updated_by_name; // "Jane Smith"
```

<a name="get-deleted-by-name-attribute"></a>
## deletedByName Attribute

Get the full name of the user who deleted the record. This requires `AuditableWithDeletesTrait`:

```php
public function getDeletedByNameAttribute(): string
```

**Example:**

```php
$post = Post::withTrashed()->first();
echo $post->deleted_by_name; // "Admin User"
```

<a name="scope-owned"></a>
## scopeOwned

A query scope that limits results to records owned by the current authenticated user. This filters records where `created_by` matches the current user's ID:

```php
public function scopeOwned(Builder $query): Builder
```

**Example:**

```php
auth()->loginUsingId(1);

$posts = Post::owned()->get();

// Equivalent SQL:
// SELECT * FROM posts WHERE posts.created_by = 1
```

::: tip When to Use scopeOwned
Use this scope to implement record ownership, filtering queries to show only records created by the authenticated user.
:::

<a name="get-qualified-user-id-column"></a>
## getQualifiedUserIdColumn

Get the fully qualified column name for the `created_by` field:

```php
public function getQualifiedUserIdColumn(): string
```

**Example:**

```php
$post = new Post();
echo $post->getQualifiedUserIdColumn(); // "posts.created_by"
// or "posts.author_id" if CREATED_BY constant is defined
```

<a name="get-user-instance"></a>
## getUserInstance

Get an instance of the configured user class:

```php
public function getUserInstance(): Model
```

**Example:**

```php
$post = new Post();
$user = $post->getUserInstance();
// Returns a new instance of the configured user model
```

<a name="get-user-class"></a>
## getUserClass

Get the user class name, respecting any `auditUser` property override:

```php
protected function getUserClass(): string
```

**Example:**

```php
$post = new Post();
echo $post->getUserClass(); // "App\Models\User"
// or "App\Models\Admin" if $auditUser is set
```

<a name="get-created-by-column"></a>
## getCreatedByColumn

Get the column name for the created by field:

```php
public function getCreatedByColumn(): string
```

**Example:**

```php
$post = new Post();
echo $post->getCreatedByColumn(); // "created_by"
// or "author_id" if CREATED_BY constant is defined
```

<a name="get-updated-by-column"></a>
## getUpdatedByColumn

Get the column name for the updated by field:

```php
public function getUpdatedByColumn(): string
```

**Example:**

```php
$post = new Post();
echo $post->getUpdatedByColumn(); // "updated_by"
// or "last_editor_id" if UPDATED_BY constant is defined
```

<a name="get-deleted-by-column"></a>
## getDeletedByColumn

Get the column name for the deleted by field. This requires `AuditableWithDeletesTrait`:

```php
public function getDeletedByColumn(): string
```

**Example:**

```php
$post = new Post();
echo $post->getDeletedByColumn(); // "deleted_by"
```
