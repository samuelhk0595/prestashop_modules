# Doctrine ORM in Modules

Doctrine is the default ORM for Symfony and is integrated into PrestaShop modules since 1.7.6.

## Define an Entity
Place entities in `src/Entity/`. Use annotations for mapping:
```php
/**
 * @ORM\Table()
 * @ORM\Entity()
 */
class ProductComment
{
    /**
     * @ORM\Id
     * @ORM\Column(name="id_product_comment", type="integer")
     * @ORM\GeneratedValue(strategy="AUTO")
     */
    private $id;
    // ...
}
```

## Database Management
Do NOT use `doctrine:schema:update` directly as it may create incompatible foreign keys. Instead, use SQL scripts in your module's `install()` method. 
You can use `./bin/console doctrine:schema:update --dump-sql` to generate the SQL base.

## Using Doctrine
### Saving an Entity
```php
$entityManager = $this->container->get('doctrine.orm.entity_manager');
$comment = new ProductComment();
$comment->setTitle('Great!');
$entityManager->persist($comment);
$entityManager->flush();
```

### Fetching Entities
```php
$repository = $entityManager->getRepository(ProductComment::class);
$comments = $repository->findByProductId($id);
```
