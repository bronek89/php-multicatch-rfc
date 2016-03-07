PHP RFC: Multicatch
======
  * Version: 0.1.0
  * Date: 2015-12-24
  * Authors: Bronisław Białek <after89@gmail.com>
  * Status: Discussion
  * First Published at: 

Introduction
===== 
This RFC adds possibility to defining multiple class hinting for one catch statement. 

Motivation
===== 
Catching different types of exception as one group. 

Proposal
===== 

```php
class AE extends Exception {};
class BE extends Exception {};
class BaE extends BE {};

function foo() {
    try {
        throw new AE();
    } catch (AE|BE $e) {
        echo "3";
    } finally {
        echo "4";
    }
    return 1;
}
```

```php
try {
    // ...
} catch (DbException|ResourceNotFoundException $e) {
    throw new HttpException("not found", 404, $e);
} catch (\Throwable $e) {
    throw new HttpException("fail", 500, $e);
}
```

Backward Incompatible Changes 
=====
No BC breaks?

Proposed PHP Version(s) 
=====
PHP 7.1

Patches and Tests 
=====
  * https://github.com/php/php-src/compare/master...bronek89:master
  * `php run-tests.php Zend/tests/try/try_catch_finally_008.phpt`

Links
=====
  * http://stackoverflow.com/questions/8439581/catching-multiple-exception-types-in-one-catch-block - Stack Overflow question 
  * http://docs.oracle.com/javase/7/docs/technotes/guides/language/catch-multiple.html - similar feature in Java

Changelog
=====
  * v0.1: RFC created with patch proposal
