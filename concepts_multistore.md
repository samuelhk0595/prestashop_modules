# Multistore Development

PrestaShop's Multistore feature allows running multiple shops from a single installation. Modules must be designed to respect the shop context.

## Configuration Variables
Use `Configuration::get('MY_VAR')` to get the value for the current shop context.
- `Configuration::updateValue('MY_VAR', 'val')`: Updates for the current context (Shop or Group).
- `Configuration::updateGlobalValue('MY_VAR', 'val')`: Updates for all shops.

## Handling Context
Always check the current context if your module performs specific actions:
```php
if (Shop::getContext() == Shop::CONTEXT_SHOP) {
    // Specific to one shop
}
```

## SQL Restrictions
When writing custom SQL, use these methods to ensure data is filtered by shop:
- `Shop::addSqlRestriction()`: Adds `WHERE id_shop = ...`
- `Shop::addSqlAssociation('product', 'p')`: Joins the `product_shop` table.
- `Shop::addSqlRestrictionOnLang('pl')`: Restricts by shop in `_lang` tables.

### Example:
```php
$sql = 'SELECT * FROM '._DB_PREFIX_.'product p ' . Shop::addSqlAssociation('product', 'p');
```

## Images and Files
Store files with a suffix related to the shop ID if they need to be different per shop (e.g., `image-s1.jpg` for shop 1).
