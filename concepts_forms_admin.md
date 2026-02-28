# Altering Back Office Forms

You can add fields to existing modern PrestaShop forms using hooks.

## Registering Hooks
In your module:
```php
public function hookActionAdministrationPageForm(&$hookParams)
{
    $formBuilder = $hookParams['form_builder'];
    $uploadQuotaForm = $formBuilder->get('upload_quota');
    $uploadQuotaForm->add('description', TextType::class, [
        'label' => 'Description'
    ]);
}
```

## Handling Errors
For the product page form, use the following syntax to display errors:
```php
Context::getContext()->controller->errors['field_id'] = [$this->l('Error message')];
if (Context::getContext()->controller->errors) {
    http_response_code(400);
    die(json_encode(Context::getContext()->controller->errors));
}
```

## Templating
You can override Symfony/Twig templates by placing them in:
`/modules/module_name/views/PrestaShop/Admin/AdvancedParameters/administration.html.twig`.
Use `{% extends '@!PrestaShop/...' %}` to extend the original.
