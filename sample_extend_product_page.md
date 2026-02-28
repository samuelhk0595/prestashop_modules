# Sample: Extending Product Page (PS 8.1+)

PrestaShop 8.1 introduced a new product page architecture. Many old `displayAdminProducts*` hooks were removed.

## Adding a Custom Field
Use the `actionProductFormBuilderModifier` hook to modify the product's FormBuilder.

### 1. Register the Hook
```php
public function install()
{
    return parent::install() && $this->registerHook('actionProductFormBuilderModifier');
}
```

### 2. Implement the Modifier
Create a modifier class (e.g., `src/Form/Modifier/ProductFormModifier.php`):
```php
public function modify(int $productId, FormBuilderInterface $productFormBuilder): void 
{
    $seoTab = $productFormBuilder->get('seo');
    $this->formBuilderModifier->addAfter(
        $seoTab,
        'tags',
        'my_custom_field',
        TextType::class,
        ['label' => 'My Field']
    );
}
```

## Adding a Custom Tab
To add a tab, add a new `FormType` directly to the `$productFormBuilder` (not to a sub-tab).
```php
$this->formBuilderModifier->addAfter(
    $productFormBuilder,
    'pricing',
    'my_custom_tab',
    CustomTabType::class,
    ['data' => $data]
);
```

## Backward Compatibility
If your module uses `displayAdminProductsExtra`, PrestaShop 8.1+ will automatically create a custom tab named "Modules" to display its content, but this hook is not recommended for new modules.
