# Auditable Schema Blueprint

<a name="auditable"></a>
## Adding auditable fields

```php
Schema::create('users', function (Blueprint $table) {
    $table->increments('id');
    $table->string('name', 100);
    $table->auditable();
    $table->timestamps();
});
```

<a name="drop-auditable"></a>
## Dropping auditable fields

```php
Schema::create('users', function (Blueprint $table) {
    $table->dropAuditable();
});
```