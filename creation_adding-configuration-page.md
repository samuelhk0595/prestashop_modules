# Adding a configuration page (Legacy architecture)

This guide is about the legacy way of creating configuration pages for modules using HelperForm.

## The getContent() method
```php
public function getContent()
{
 $output = '';

 if (Tools::isSubmit('submit' . $this->name)) {
 $configValue = (string) Tools::getValue('MYMODULE_CONFIG');

 if (empty($configValue) || !Validate::isGenericName($configValue)) {
 $output = $this->displayError($this->l('Invalid Configuration value'));
 } else {
 Configuration::updateValue('MYMODULE_CONFIG', $configValue);
 $output = $this->displayConfirmation($this->l('Settings updated'));
 }
 }

 return $output . $this->displayForm();
}
```

## Displaying the form
The configuration form itself is displayed with the displayForm() method using HelperForm.

```php
public function displayForm()
{
 // Init Fields form array
 $form = [
 'form' => [
 'legend' => [
 'title' => $this->l('Settings'),
 ],
 'input' => [
 [
 'type' => 'text',
 'label' => $this->l('Configuration value'),
 'name' => 'MYMODULE_CONFIG',
 'size' => 20,
 'required' => true,
 ],
 ],
 'submit' => [
 'title' => $this->l('Save'),
 'class' => 'btn btn-default pull-right',
 ],
 ],
 ];

 $helper = new HelperForm();
 // ... settings ...
 return $helper->generateForm([$form]);
}
```
