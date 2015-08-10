# Nette Database Nested Transaction

[![Downloads this Month](https://img.shields.io/packagist/dm/minetro/ntdb.svg?style=flat-square)](https://packagist.org/packages/minetro/ntdb)
[![Latest stable](https://img.shields.io/packagist/v/minetro/ntdb.svg?style=flat-square)](https://packagist.org/packages/minetro/ntdb)

## Install
```sh
$ composer require minetro/ntdb
```

## Resources

Based on this articles.

* http://www.yiiframework.com/wiki/38/how-to-use-nested-db-transactions-mysql-5-postgresql/
* http://www.kennynet.co.uk/2008/12/02/php-pdo-nested-transactions/
* https://gist.github.com/neoascetic/5269127

## Usage

Support:

* MySQL / MySQLi
* PostgreSQL
* SQLite

Available methods:

* `$t->begin`
* `$t->commit`
* `$t->rollback`
* **`$t->transaction`** or **`$t->t`**

### Begin

Starts transaction.

```php
$t = new Transaction(new Connection(...));
$t->begin();
```

### Commit

Commit changes in transaction.

```php
$t = new Transaction(new Connection(...));
$t->begin();
// some changes..
$t->commit();
```

### Rollback

Revert changes in transaction.

```php
$t = new Transaction(new Connection(...));

$t->begin();
try {
    // some changes..
    $t->commit();
} catch (Exception $e) {
    $t->rollback();
}
```

### Transaction

Combine begin, commit and rollback to one method.

On success it commits changes, if exceptions is thrown it rollbacks changes.

```php
$t = new Transaction(new Connection(...));
$t->transaction(function() {
    // some changes..
});

$t->t(function() {
    // some changes..
});
}
```
