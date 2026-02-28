# Concepts: Hooks

[Hooks](https://devdocs.prestashop-project.org/9/development/components/hook/) are a way to associate your code to some specific PrestaShop events.

## Naming scheme
Hook names are prefixed with “action” or “display”.
- `action<Something>`: Triggered by events.
- `display<Something>`: Result in something being displayed.

## Using hooks
### Registration
Call `Module::registerHook($hookName)` usually during installation.

### Execution
Create a non-static public method: `hookDisplayHeader(array $params)`.

## Triggering a hook
- **Legacy Controller**: `Hook::exec('displayLeftColumn')`
- **Symfony Controller**: `$this->dispatchHook($hookName, $parameters)`
- **Smarty**: `{hook h='hookName'}`
- **Twig**: `{{ renderHook('hookName', { params }) }}`
