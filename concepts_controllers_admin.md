# Admin Controllers (PrestaShop 9)

In PrestaShop 9.0+, `FrameworkBundleAdminController` is deprecated. Use `PrestaShopAdminController` for new controllers.

## How to declare a new Controller
Create a class in `src/Controller/`:
```php
namespace MyModule\Controller;

use PrestaShopBundle\Controller\Admin\PrestaShopAdminController;
use Symfony\Component\HttpFoundation\Response;

class DemoController extends PrestaShopAdminController
{
    public function demoAction(): Response
    {
        return $this->render('@Modules/your-module/templates/admin/demo.html.twig', [
            'data' => 'content',
        ]);
    }
}
```

## Dependency Injection
Controllers must be defined as services in `config/services.yml`:
```yaml
services:
  MyModule\Controller\DemoController:
    autowire: true
    autoconfigure: true
```

## Helper Methods
`PrestaShopAdminController` provides:
- `$this->getConfiguration()`
- `$this->getTranslator()`
- `$this->getRouter()`
- `$this->dispatchHookWithParameters()`

## Routing
Define routes in `config/routes.yml`:
```yaml
your_route_name:
  path: your-module/demo
  methods: [GET]
  defaults:
    _controller: 'MyModule\Controller\DemoController::demoAction'
```
Module routes are prefixed with `/modules/` by default. Use `_disable_module_prefix: true` to remove it.
