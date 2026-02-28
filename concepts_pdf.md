# PDF Files and Templates

PrestaShop generates PDFs (Invoices, Delivery Slips, etc.) using Smarty templates and TCPDF.

## PDF Templates
Templates are located in the `/pdf` folder. Key files:
- `invoice.tpl`: Main invoice template.
- `delivery-slip.tpl`: Delivery slip template.
- `header.tpl` / `footer.tpl`: Common layouts.

## Customizing PDF Content
Use dynamic hooks to add information to PDF templates.
Hook name format: `displayPDF<TemplateClassName>`.

### Example: Adding data to Invoice
In your module:
```php
public function hookDisplayPDFInvoice($hookArgs)
{
    $customer = $this->context->customer;
    $hookArgs['object']->custom_data = "Some value";
}
```
In your theme's PDF template (`invoice.note-tab.tpl`):
```twig
{if $order_invoice->custom_data}
    {$order_invoice->custom_data}
{/if}
```

## PDF Variables
Commonly available Smarty variables:
- `{lastname}`, `{firstname}`, `{id_order}`, `{order_name}`
- `{total_paid}`, `{total_products}`, `{total_shipping}`

## Custom PDF Generation
You can also trigger your own PDF generation using the `PDFGenerator` class within a module method.
