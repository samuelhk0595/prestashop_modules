# Core Changes: PrestaShop 9.0.x

PrestaShop 9.0 introduces significant technical updates, focusing on modernizing the architecture and improving security.

## PHP Support
- **Minimum**: PHP 8.1
- **Supported**: PHP 8.2, 8.3, and 8.4

## Symfony Upgrade
PrestaShop 9 has been upgraded to **Symfony 6.4** (from 4.4 in PS 8.x). This involves several breaking changes in the framework layer.

### Removed Dependencies
- `guzzlehttp/guzzle`: Replaced by Symfony HTTP Client.
- `swiftmailer/swiftmailer`: Replaced by **Symfony Mailer**. SSL encryption for mail is no longer supported (use TLS or none).
- `league/tactician-bundle`: Replaced by Symfony Messenger.

## Modern Controllers
- `FrameworkBundleAdminController` is deprecated. Use **`PrestaShopAdminController`**.
- Controllers must now be defined as **services**.
- `$this->get('service_name')` is no longer available in modern controllers. Use **Dependency Injection** (Constructor, Method, or `#[Autowire]` attribute).

## New Architecture
- **Dedicated Kernels**: Separate kernels for Back Office, Admin API, and Front Office (experimental).
- **Symfony Layout**: The Back Office layout is now fully rendered by Symfony using Twig components.

## Migrated Pages
Several pages have been migrated to the new architecture and no longer use `HelperForm` or `HelperList`:
- Attributes & Features
- Shopping Carts
- Order Statuses
- Image Settings
- Products (the new version introduced in 8.1 is now the only one).

## Hooks and Trans()
- `trans()` method no longer automatically escapes strings. You must use `htmlspecialchars` if needed.
- Many legacy product page hooks were removed (e.g., `displayAdminProductsCombinationBottom`). Use `actionProductFormBuilderModifier` instead.
