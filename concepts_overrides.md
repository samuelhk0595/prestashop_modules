# Concepts: Overrides

Overrides allow you to modify class and controller files using inheritance.

## Important note
Overrides are exclusive and risky. They are not recommended for distributed modules (Addons). Use Hooks or Symfony Service Decoration where possible.

## Class & controller override
- **Class Override**: Create a file in `/modules/<name>/override/classes/Product.php`. The class must be named `Product extends ProductCore`.
- **Controller Override**: Create a file in `/modules/<name>/override/controllers/front/ProductController.php`. Class `ProductController extends ProductControllerCore`.

## Override a module
You can override a module's main class or its controllers.
- **Main Class**: Put file in `/override/modules/blockuserinfo/blockuserinfo.php`. Class name: `BlockUserInfoOverride extends BlockUserInfo`.
- **Controllers**: Put in `/override/modules/blockreassurance/controllers/admin/AdminBlockListingController.php`. Class `AdminBlockListingControllerOverride extends AdminBlockListingController`.

Don't forget to clean the cache after adding an override.
