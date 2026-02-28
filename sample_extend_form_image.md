# Sample: Extending Forms with Image Upload

This tutorial explains how to add an "Upload Image" field to an existing Symfony-based form (e.g., Suppliers).

## Workflow
1. **Hook onto Form**: Use `action<Entity>FormBuilderModifier` to add a `FileType::class` field.
2. **Handle Persistence**: Use `actionAfterCreate<Entity>FormHandler` or `actionAfterUpdate<Entity>FormHandler`.

## Implementation Example
### Adding the field
```php
$formBuilder->add('upload_image_file', FileType::class, [
    'label' => 'Upload Logo',
    'required' => false,
]);
```

### Handling the upload
In the "AfterUpdate" hook:
```php
public function hookActionAfterUpdateSupplierFormHandler(array $params)
{
    $uploadedFile = $params['form_data']['upload_image_file'];
    if ($uploadedFile instanceof UploadedFile) {
        // Use an Uploader service to save the file
        $this->get(SupplierImageUploader::class)->upload($params['id'], $uploadedFile);
    }
}
```

## Best Practices
- **Use Doctrine**: Store image metadata (like filename) in a custom Doctrine entity.
- **Uploader Class**: Isolate the image processing logic (resizing, temporary files, storage) in a dedicated service.
- **Preview**: Use a `CustomContentType` to show a preview of the existing image in the form.
