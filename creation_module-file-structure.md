# Module file structure

A module is made of a lot of files, all stored in a folder that bears the same name as the module, that folder being in turn stored in the /modules folder at the root of the main PrestaShop folder: /modules/<modulename>/.

## Main files and directories
Example:
mymodule
├── config
│ ├── admin
│ │ └── services.yml
│ ├── front
│ │ └── services.yml
│ └── services.yml
├── controllers
├── override
├── src
│ ├── Controller
│ └── Entity
├── translations
├── upgrade
├── vendor
├── views
│ ├── css
│ ├── img
│ ├── js
│ └── templates
├── config.xml
├── logo.png
└── mymodule.php

### config/ folder
The config folder is the place where configuration files are stored. In particular, Routes and Services.

### controllers/ folder
The controllers folder contains the legacy-style Controller files.
Symfony-based controllers go in the "src" folder.

### src/ folder
The src folder is the recommended folder to place all of your module’s PHP classes–like Grids, Entities, Forms, and so on.

### views/ folder
The views folder contains your module’s template files (.tpl for Smarty or .html.twig for Twig) as well as static assets used by the module (css, js or image files). 
