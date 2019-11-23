# Concrete5 @deprecated

This is an **ongoing** list of `@deprecated` code within concrete5 and their best replacement methods that I came up with.


# Controllers

### ~~Controller->redirect()~~
All controllers extending from `\Concrete\Core\Controller\AbstractController` are affected

@deprecated
```php
// Context: controller
$this->redirect('/dashboard/system/some');
```
Replacement
```php
use Concrete\Core\Routing\Redirect;

Redirect::to('/dashboard/system/some')->send();
```
---

### ~~Controller->isPost()~~
@deprecated
```php
// Context: controller
$this->isPost()
```
Replacement
```php
$this->getRequest()->isPost()
```


# Package

### ~~Package::getByHandle()~~
@deprecated
```php
$packageCtrl = Package::getByHandle('concrete5_doctrine_behavioral_extensions');
```
Replacement
```php
// Context: controller
use Concrete\Core\Package\PackageService;

// Important: Don't add this line to the constructor. At this stage $app will be "null"
$packageCtrl = $this->app->make(PackageService::class)->getClass('concrete5_doctrine_behavioral_extensions');
```
```php
// Context: controller - better example
public function on_start()
{
    parent::on_start();
    $packageCtrl = $this->app->make(PackageService::class)->getClass('concrete5_doctrine_behavioral_extensions');
}
```
```php
// Elsewhere in a class context
use Concrete\Core\Package\PackageService;

$app = \ApplicationFacade::getFacadeApplication();
return $app->make(PackageService::class)->getClass('concrete5_doctrine_behavioral_extensions');
```

# Attribute

### ~~AbstractCategory::getByHandle()~~
@deprecated
```php
/** @var \Concrete\Core\Attribute\Category\PageCategory  $category */
$category = $categoryEntity->getController();
$key = $category->getByHandle($handle);
```

Replacement
```php
/** @var \Concrete\Core\Attribute\Category\PageCategory  $category */
$category = $categoryEntity->getController();
$key = $category->getAttributeKeyByHandle($handle);
```

### ~~AbstractCategory::getByID()~~
@deprecated
```php
/** @var \Concrete\Core\Attribute\Category\PageCategory  $category */
$category = $categoryEntity->getController();
$key = $category->getByID($id);
```

Replacement
```php
/** @var \Concrete\Core\Attribute\Category\PageCategory  $category */
$category = $categoryEntity->getController();
$key = $category->getAttributeKeyByID($id);
```
