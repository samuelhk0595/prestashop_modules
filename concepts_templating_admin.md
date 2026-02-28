# Overriding Back Office Views (Twig)

Since PrestaShop 1.7, the Back Office uses **Twig** as its templating engine.

## Identify the Template
Use the **Symfony Debug Toolbar** (Twig metrics) to find the template name (e.g., `@PrestaShop/Admin/Product/CatalogPage/catalog.html.twig`).

## Overriding in a Module
Create the same folder structure in your module:
`modules/foo/views/PrestaShop/Admin/Product/CatalogPage/catalog.html.twig`.

### Extend the Original
Use `@!PrestaShop` (or `@PrestaShopCore` in PS 8+) to extend the base file and override specific blocks:
```twig
{% extends '@!PrestaShop/Admin/Product/CatalogPage/catalog.html.twig' %}

{% block product_catalog_filters %}
    Hello world! (Overridden)
{% endblock %}
```

## Benefits
This allows deep customization of the Back Office UI (moving columns, adding widgets, changing layouts) without modifying Core files.
