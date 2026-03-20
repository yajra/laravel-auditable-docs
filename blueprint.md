---
title: "Auditable Schema Blueprint"
description: "Blueprint macros for adding and removing auditable fields in migrations."
---

# Auditable Schema Blueprint

The package provides Laravel Schema Blueprint macros for easily adding auditable fields to your migrations.

<a name="auditable"></a>
## Adding Auditable Fields

Use the `auditable()` macro to add `created_by` and `updated_by` columns:

```php
Schema::create('posts', function (Blueprint $table) {
    $table->id();
    $table->string('title');
    $table->text('content');
    $table->auditable();
    $table->timestamps();
});
```

This creates:
- `created_by` - `unsignedBigInteger`, nullable, indexed
- `updated_by` - `unsignedBigInteger`, nullable, indexed

<a name="auditable-with-deletes"></a>
## Adding Auditable Fields with Soft Deletes

Use the `auditableWithDeletes()` macro to add `created_by`, `updated_by`, and `deleted_by` columns:

```php
Schema::create('posts', function (Blueprint $table) {
    $table->id();
    $table->string('title');
    $table->text('content');
    $table->auditableWithDeletes();
    $table->timestamps();
    $table->softDeletes();
});
```

This creates:
- `created_by` - `unsignedBigInteger`, nullable, indexed
- `updated_by` - `unsignedBigInteger`, nullable, indexed
- `deleted_by` - `unsignedBigInteger`, nullable, indexed

<a name="drop-auditable"></a>
## Dropping Auditable Fields

Use the `dropAuditable()` macro to remove `created_by` and `updated_by` columns:

```php
Schema::table('posts', function (Blueprint $table) {
    $table->dropAuditable();
});
```

<a name="drop-auditable-with-deletes"></a>
## Dropping Auditable Fields with Deletes

Use the `dropAuditableWithDeletes()` macro to remove `created_by`, `updated_by`, and `deleted_by` columns:

```php
Schema::table('posts', function (Blueprint $table) {
    $table->dropAuditableWithDeletes();
});
```
