# Composer in PrestaShop Modules

Composer is used to manage dependencies and provides an autoloader for your module's classes.

## Setup `composer.json`
Create the file in your module root:
```json
{
    "name": "author/mymodule",
    "autoload": {
        "psr-4": {
            "MyNamespace\\": "src/"
        }
    },
    "config": {
        "prepend-autoloader": false
    },
    "type": "prestashop-module"
}
```

## Important: `prepend-autoloader`
You **must** set `"prepend-autoloader": false`. This ensures that Core dependencies are not overridden by the module's own dependencies, preventing system crashes.

## Generating the Autoloader
Run the following in the module folder:
```bash
composer dump-autoload
```
This creates the `vendor/` directory. Remember to include `vendor/` in your final module zip package (but exclude `require-dev` libraries).

## Autoloading Namespaces
The convention is `PrestaShop\Module\ModuleName`. Using namespaces allows you to use Symfony services and modern PHP features cleanly.
