Cloudinary Media Editing PHP SDK
=========================
## About
The Cloudinary Media Editing PHP SDK allows you to quickly and easily integrate your application with Cloudinary.
Effortlessly edit and deliver your cloud's assets.

## Installation
```bash
composer require "cloudinary/media-editing"
```
# Usage
### Setup
```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');

// Configure HTTP basic authorization: basicAuth
$config = Cloudinary\Configuration::getDefaultConfiguration()
    ->setCloudinaryUrl('cloudinary://key:secret@cloud_name');

$apiInstance = new Cloudinary\Api\CacheApi(null, $config);

$cacheInvalidateRequestPayload = new \Cloudinary\Model\CacheInvalidateRequestPayload(); 
// \Cloudinary\Model\CacheInvalidateRequestPayload | Payload to invalidate the cache

try {
    $apiInstance->invalidate($cacheInvalidateRequestPayload);
} catch (Exception $e) {
    echo 'Exception when calling CacheApi->invalidate: ', $e->getMessage(), PHP_EOL;
}
```

# APIs
### Media Delivery API
* [Media Delivery API](https://github.com/cloudinary/media-delivery-api-php/blob/main/README.md)

### Media Editing API
* [Media Editing API](https://github.com/cloudinary/media-editing-api-php/blob/main/README.md)

## Get Help
If you run into an issue or have a question, you can either:
- Issues related to the SDK: [Open a Github issue](https://github.com/cloudinary/media-editing-php/issues)
- Issues related to your account: [Open a support ticket](https://cloudinary.com/contact)

## Licence
Released under the MIT license.
