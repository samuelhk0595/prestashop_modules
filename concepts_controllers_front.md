# Front Controllers

Front controllers add features accessible to customers.

## Rules for creation
1. Stored in `controllers/front/`.
2. Class name format: `<ModuleName><FileName>ModuleFrontController`.
3. Must extend `ModuleFrontController`.

## Methods
### initContent()
Assign variables to Smarty and set the template:
```php
public function initContent()
{
    parent::initContent();
    $this->context->smarty->assign(['var' => 'value']);
    $this->setTemplate('module:mymodule/views/templates/front/test.tpl');
}
```

### postProcess()
Handles POST requests. Use `Tools::getValue()` to retrieve data and `Tools::redirect()` for redirection.

## Accessing the Controller
Generate links using:
```php
Context::getContext()->link->getModuleLink('mymodule', 'controllername', ['id' => 1]);
```

## Restrictions
- `$this->auth = true;`: Only logged customers.
- `$this->ssl = true;`: Force HTTPS.
