# Adding a configuration page with Symfony forms

With the new Symfony architecture, there is a much modern way of integrating settings forms (Configure action) for your modules.

## Create the configuration form type
Create a DemoConfigurationFormType.php file in src/Form.

```php
class DemoConfigurationFormType extends TranslatorAwareType
{
 public function buildForm(FormBuilderInterface $builder, array $options): void
 {
 $builder
 ->add('config_text', TextType::class, [
 'label' => $this->trans('Configuration text', 'Modules.Demosymfonyformsimple.Admin'),
 'help' => $this->trans('Maximum 32 characters', 'Modules.Demosymfonyformsimple.Admin'),
 ]);
 }
}
```

## Create the Data configuration
Create a DemoConfigurationTextDataConfiguration.php file in src/Form.

## Create the form data provider
Create a DemoConfigurationTextFormDataProvider.php file in src/Form.

## Create and register the form handler
You can use PrestaShop native's Handler.

## Create the configuration controller
Create a DemoConfigurationController.php file in src/Controller.

## Add this route to the getContent() method
```php
public function getContent()
{
 $route = $this->get('router')->generate('demo_configuration_form_simple');
 Tools::redirectAdmin($route);
}
```
