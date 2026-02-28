# Module Translation (PrestaShop 9)

Internationalization (i18n) is crucial for making your module usable globally. PrestaShop provides an interface under **International > Translations** for merchants to translate wordings.

## Systems
1. **New Translation System (1.7.6+)**: Recommended for modern modules. Uses domains and Symfony-style translations.
2. **Classic Translation System**: Used for backward compatibility with older PrestaShop versions.

## Making Wordings Translatable
In your PHP code, use the `trans()` method (for modern/Symfony contexts) or `$this->l()` (for legacy/main class contexts).

### Modern Example (Symfony/Twig):
```php
$this->trans('My wording', [], 'Modules.Mymodule.Admin');
```
In Twig:
```twig
{{ 'My wording'|trans({}, 'Modules.Mymodule.Admin') }}
```

### Legacy Example:
```php
$this->l('My wording');
```

## Comparison
The new system uses **Translation Domains** (e.g., `Modules.Mymodule.Admin`), which makes wordings more organized and reusable compared to the file-based "Classic" system.
