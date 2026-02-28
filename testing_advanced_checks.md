# Testing: Advanced Checks

## Static Analysis (PHPStan)
Static analysis detects errors without executing the code (e.g., calling undefined methods, type mismatches). PrestaShop uses **PHPStan**.

### Setup
```bash
composer require --dev phpstan/phpstan
php vendor/bin/prestashop-coding-standards phpstan:init
```

### Usage
You must set the `_PS_ROOT_DIR_` environment variable:
```bash
_PS_ROOT_DIR_=/path/to/prestashop vendor/bin/phpstan analyse --configuration=tests/phpstan/phpstan.neon
```

## Unit Testing (PHPUnit)
Test isolated business logic using **PHPUnit**.

### Installation
```bash
composer require --dev phpunit/phpunit
```

### Running Tests
```bash
php vendor/bin/phpunit tests
```
While full coverage is hard due to PrestaShop dependencies, focus on testing core module logic.
