# Auditable Trait

Using `AuditableTrait` trait on your model will give you the following api.

<a name="creator"></a>
## Creator

Get the instance of the `User` who created the record.

```php
$post = Post::first();
$creator = $post->creator;
```

<a name="updater"></a>
## Updater

Get the instance of the `User` who last updated the record.
```php
$post = Post::first();
$updater = $post->updater;
```

<a name="owned"></a>
## Owned Scope

A query scope that limits the results to a list of records that the current user owned.

```php
auth()->loginUsingId(1);

$posts = Post::owned()->get();
```


