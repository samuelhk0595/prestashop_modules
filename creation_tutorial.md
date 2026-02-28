# Tutorial: Creating your first module

Before you start writing code for your PrestaShop module, we recommend reading PrestaShop’s Coding standards. 

Let’s create a first simple module, this will allow us to better describe its structure. We will name it “My module”.

First, create the module’s folder, in PrestaShop’s /modules folder. Let’s call it mymodule. This will be the module’s “technical” name.

This folder must contain the main file, a PHP file of the same name as the folder, which will handle most of the processing: mymodule.php.

## The constant test
The main mymodule.php file must start with the following test:

```php
<?php
if (!defined('_PS_VERSION_')) {
 exit;
}
```

This checks for the presence of an always-existing PrestaShop constant (its version number), and if it does not exist, it stops the module from loading. 

## The main class
The main file must contain the module’s main class.

```php
class MyModule extends Module
{
}
```

## The constructor method
```php
public function __construct()
{
 $this->name = 'mymodule';
 $this->tab = 'front_office_features';
 $this->version = '1.0.0';
 $this->author = 'Firstname Lastname';
 $this->need_instance = 0;
 $this->ps_versions_compliancy = [
 'min' => '8.0.0',
 'max' => '9.99.99',
 ];
 $this->bootstrap = true;

 parent::__construct();

 $this->displayName = $this->trans('My module', [], 'Modules.Mymodule.Admin');
 $this->description = $this->trans('Description of my module.', [], 'Modules.Mymodule.Admin');
}
```

## Building the install() and uninstall() methods
```php
public function install()
{
 return parent::install();
}

public function uninstall()
{
 return parent::uninstall();
}
```
