# Carrier Modules (PrestaShop 9)

Carrier modules extend shipping functionality by providing custom cost calculation and tracking.

## Principles
Your module class must extend `CarrierModule`.

```php
class MyOwnCarrier extends CarrierModule
{
    public function getOrderShippingCost($params, $shipping_cost)
    {
        // Compute cost based on ranges
        return 5.00;
    }

    public function getOrderShippingCostExternal($params)
    {
        // Compute cost without ranges (e.g., API call)
        return 10.00;
    }
}
```

## Controlling Carrier ID Changes
PrestaShop duplicates carriers when they are edited. To track the current ID, use the `actionCarrierUpdate` hook:

```php
public function hookActionCarrierUpdate($params)
{
    $id_carrier_old = (int)$params['id_carrier'];
    $id_carrier_new = (int)$params['carrier']->id;
    
    if ($id_carrier_old === (int)Configuration::get('MYCARRIER_ID')) {
        Configuration::updateValue('MYCARRIER_ID', $id_carrier_new);
    }
}
```

## Important Note
Use the `id_reference` field for persistent identification, as `id_carrier` changes on every update.
