Cloudinary Media Editing PHP SDK
=========================
## About
The Cloudinary Media Editing PHP SDK allows you to quickly and easily integrate your application with Cloudinary.
Effortlessly edit and deliver your cloud's assets.

### Additional documentation
This Readme provides basic installation and usage information.
For the complete documentation, see the [Media Editing SDK Guide](https://cloudinary.com/documentation/media_editing_api_sdks).
## Table of Contents
- [Key Features](#key-features)
- [Version Support](#Version-Support)
- [Installation](#installation)
- [Usage](#usage)
    - [Setup](#Setup)
    - [Create Media Source](#Create-Media-Source)
    - [Transform and Store](#Transform-and-Store)
    - [Cache warmup](#Cache-warmup)

# Key Features
### Media Delivery API
- [CacheApi](https://cloudinary.com/documentation/media_editing_api_reference#/Cache)
- [DeliveryProfileApi](https://cloudinary.com/documentation/media_editing_api_reference#/Delivery%20Profile)
- [MappingFunctionApi](https://cloudinary.com/documentation/media_editing_api_reference#/Mapping%20Function)
- [MediaSourceApi](https://cloudinary.com/documentation/media_editing_api_reference#/Media%20Source)
- [MediaTargetApi](https://cloudinary.com/documentation/media_editing_api_reference#/Media%20Target)

### Media Editing API
- [TransformApi](https://cloudinary.com/documentation/media_editing_api_reference#transform_api)

## Version Support
| SDK Version | PHP < 7.3 | PHP 7.3 | PHP 7.4 | PHP 8.x |
|-------------|-----------|---------|---------|---------|
| 0.x         | x         | v       | v       | v       |


## Installation
```bash
composer require "cloudinary/media-editing"
```

# Usage

### Setup
```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');

// Configure with CLOUDINARY_URL
$config = Cloudinary\Configuration::getDefaultConfiguration()
    ->setCloudinaryUrl('cloudinary://key:secret@cloud_name');
```

### Create Media Source
Example of how to add Media Storage, in this case a new media source:
```php
$apiInstance = new Cloudinary\MediaDelivery\Api\MediaSourceApi(null, $deliveryConfig);

// Payload to create the Media Source
$mediaSourceCreatePayload = [
    "display_name" => "my_media_source",
    "source_type"  => "s3",
    "config"       => [
        "s3_bucket_name" => "my_bucket",
        "s3_bucket_folder" => "my_bucket_folder",
        "s3_access_key" => "123456789",
        "s3_secret_key" => "123456789",
        "s3_uri_template" => "s3://my_bucket/images/{{vars.signature}}/{{fwd_key}}",
    ],
];

try {
    $result = $apiInstance->createMediaSource($mediaSourceCreatePayload);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling MediaSourceApi->createMediaSource: ', $e->getMessage(), PHP_EOL;
}
```

### Transform and Store
Example of how to transform and store an asset:
```php
$apiInstance = new TransformAndStoreApi(null, $config);

$mediaSource = new MediaConnectorInstance();
$mediaSource->setId("11fcd4a3b294515067f1266c7e7f0422")->setFwdKey("sample");

$mediaTarget = new MediaConnectorInstance();
$mediaTarget->setId("33832c937c251b8566e4210736cec544")->setFwdKey("new_sample");

$transformRequest = new TransformRequest();

$transformation = new TransformationDescriptor();
$transformation->setCanonicalTransformation("c_scale,w_500");

$transformRequest->setInputType("media_source")
   ->setMediaSource($mediaSource)
   ->setMediaTarget($mediaTarget)
   ->setTransformationDescriptor($transformation);

try {
    $result = $apiInstance->transformAndStore($transformRequest);
    print_r($result);
} catch (\Exception $e) {
    echo 'Exception when calling TransformAndStoreApi->transformAndStore: ', $e->getMessage(), PHP_EOL;
}
```

### Cache warmup
Example of how to perform a cache warmup:

```php
$apiInstance = new Cloudinary\Api\CacheApi(null, $config);

$cacheWarmupRequestPayload = new \Cloudinary\MediaDelivery\Model\CacheWarmupRequestPayload(); // \Cloudinary\MediaDelivery\Model\CacheWarmupRequestPayload | Payload to warm up the cache

$cacheWarmupRequestPayload->setUrl("<your url>");
// $cacheWarmupRequestPayload->setUrl("https://<cloud_name>.media.cloudinary.net/image/upload/c_scale,w_500/sample");

try {
    $result = $apiInstance->warmup($cacheWarmupRequestPayload);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling CacheApi->warmup: ', $e->getMessage(), PHP_EOL;
}
```

## Get Help
- [Open a Github issue](https://github.com/CloudinaryLtd/media-editing-php/issues) (for issues related to the SDK)
- [Open a support ticket](https://cloudinary.com/contact) (for issues related to your account)

## About Cloudinary
Cloudinary is a powerful media API for websites and mobile apps alike, Cloudinary enables developers to efficiently manage, transform, optimize, and deliver images and videos through multiple CDNs. Ultimately, viewers enjoy responsive and personalized visual-media experiences—irrespective of the viewing device.

## Additional Resources
- [Cloudinary Transformation and REST API References](https://cloudinary.com/documentation/cloudinary_references): Comprehensive references, including syntax and examples for all SDKs.
- [MediaJams.dev](https://mediajams.dev/): Bite-size use-case tutorials written by and for Cloudinary Developers
- [DevJams](https://www.youtube.com/playlist?list=PL8dVGjLA2oMr09amgERARsZyrOz_sPvqw): Cloudinary developer podcasts on YouTube.
- [Cloudinary Academy](https://training.cloudinary.com/): Free self-paced courses, instructor-led virtual courses, and on-site courses.
- [Code Explorers and Feature Demos](https://cloudinary.com/documentation/code_explorers_demos_index): A one-stop shop for all code explorers, Postman collections, and feature demos found in the docs.
- [Cloudinary Roadmap](https://cloudinary.com/roadmap): Your chance to follow, vote, or suggest what Cloudinary should develop next.
- [Cloudinary Facebook Community](https://www.facebook.com/groups/CloudinaryCommunity): Learn from and offer help to other Cloudinary developers.
- [Cloudinary Account Registration](https://cloudinary.com/users/register/free): Free Cloudinary account registration.
- [Cloudinary Website](https://cloudinary.com)

## License
Released under the MIT license See the [LICENSE](https://github.com/cloudinary/media-editing-php/blob/main/LICENSE) file for details.
