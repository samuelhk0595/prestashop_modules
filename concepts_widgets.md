# Concepts: Widgets

Widget is an advanced concept introduced on PrestaShop 1.7, extending hooks feature.

## Limitation of hooks
If a module wants to display the same content on several places, it has to register all possible hooks. Widgets allow displaying content everywhere the module is asked to do so.

## Make a module widgets compliant
1. **Implement interface**: `MyModule extends Module implements WidgetInterface`
2. **Declare mandatory methods**: 
   - `renderWidget($hookName, array $configuration)`
   - `getWidgetVariables($hookName, array $configuration)`

## Call Widgets
- **Smarty**: `{widget name='mymodule'}`
- **PHP**: `Hook::coreRenderWidget(Module $module, $hook_name, $params);`

## Code example
```php
class MyModule extends Module implements WidgetInterface
{
    public function renderWidget($hookName, array $configuration)
    {
        $this->smarty->assign($this->getWidgetVariables($hookName, $configuration));
        return $this->fetch('module:'.$this->name.'/views/templates/widget/mymodule.tpl');
    }

    public function getWidgetVariables($hookName , array $configuration)
    {
        return ['var' => 'value'];
    }
}
```
