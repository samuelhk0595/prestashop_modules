# Mail Templates in Modules

You can add custom email layouts from your module. These will be rendered, translated, and exported when languages are installed or generated via the Back Office.

## Layouts
Store layouts in your module (e.g., `mails/layouts/`). You can extend existing theme layouts:
```twig
{# modules/my_module/mails/layouts/custom_classic_layout.html.twig #}
{% extends '@MailThemes/classic/components/layout.html.twig' %}

{% block content %}
  <tr>
    <td>{{ 'My custom message'|trans({}, 'EmailsBody', locale)|raw }}</td>
  </tr>
{% endblock %}
```

## Registering Layouts
Use the `actionListMailThemes` hook to add your layout to the collection:
```php
public function hookActionListMailThemes(array $hookParams)
{
    if (!isset($hookParams['mailThemes'])) return;

    $themes = $hookParams['mailThemes'];
    foreach ($themes as $theme) {
        if (!in_array($theme->getName(), ['classic', 'modern'])) continue;

        $theme->getLayouts()->add(new Layout(
            'custom_template_name',
            __DIR__ . '/mails/layouts/custom_' . $theme->getName() . '_layout.html.twig',
            '',
            $this->name
        ));
    }
}
```
Preview the results in **Design > Email Theme**.
