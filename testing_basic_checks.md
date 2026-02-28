# Testing: Basic Checks

Ensuring your module is stable and follows coding standards is critical for production use.

## Syntax Check (Linter)
Verify that your PHP files are valid for the target PHP versions:
```bash
find . -type f -name '*.php' ! -path "./vendor/*" ! -path "./tests/*" -exec php -l -n {} \;
```
It's important to test against the minimum and maximum PHP versions your module supports.

## Coding Standards
PrestaShop modules follow the same rules as the core. Use `prestashop/php-dev-tools` to manage these rules.

### Setup:
```bash
composer require --dev prestashop/php-dev-tools friendsofphp/php-cs-fixer
php vendor/bin/prestashop-coding-standards cs-fixer:init
```

### Fix Style Issues:
```bash
php vendor/bin/php-cs-fixer fix
```

## License Headers
Use [Header-Stamp](https://github.com/PrestaShopCorp/header-stamp) to apply license headers to your files:
```bash
php vendor/bin/header-stamp --license=path/to/license.txt --exclude=vendor,tests
```
