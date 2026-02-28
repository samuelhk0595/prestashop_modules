# Extending Webservice (PrestaShop 9)

PrestaShop enables third-party tools to access the database through a CRUD API (Webservice). Modules can extend this by adding custom resources.

## Create the Entity
Your entity class should extend `ObjectModel` and include the `$webserviceParameters` property.

```php
class Article extends ObjectModel
{
    public $title;
    public $content;

    public static $definition = [
        'table' => 'article',
        'primary' => 'id_article',
        'multilang' => true,
        'fields' => [
            'title' => ['type' => self::TYPE_STRING, 'validate' => 'isCleanHtml', 'required' => true],
            'content' => ['type' => self::TYPE_HTML, 'lang' => true, 'validate' => 'isCleanHtml'],
        ],
    ];

    protected $webserviceParameters = [
        'objectNodeName' => 'article',
        'objectsNodeName' => 'articles',
        'fields' => [
            'title' => ['required' => true],
            'content' => [],
        ],
    ];
}
```

## Register the Hook
Register and implement the `addWebserviceResources` hook:
```php
public function hookAddWebserviceResources($params)
{
    return [
        'articles' => [
            'description' => 'Blog articles',
            'class' => 'Article',
        ],
    ];
}
```

## Accessing the Resource
The new resource will be available at `https://yourshop.com/api/articles`.
