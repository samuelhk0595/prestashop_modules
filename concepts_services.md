# Concepts: Symfony Services

You can modify the Symfony container configuration from a module.

## Create and declare a new Symfony service
1. **Define the class**: Place in `src/YourService.php` with a namespace.
2. **Register in `config/services.yml`**:
```yaml
services:
  your_company.your_module.your_service:
    class: YourCompany\YourModule\YourService
    arguments: ["@translator", "My message"]
```

## Override an existing Symfony service
- **Override**: Replace the service entirely by using the same name.
- **Decorate**: Use the `decorates` keyword. The old service is available as `<service_name>.inner`.

## Services in Legacy environment
Since 1.7.6, you can access services in legacy controllers/front-office.
- `config/admin/services.yml`: Back office legacy.
- `config/front/services.yml`: Front office.

Access via `$this->get('service_name')` in controllers or modules.
