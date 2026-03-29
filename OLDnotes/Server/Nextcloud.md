It's a service that simulates all google services and more.
Can be used as a interface for a Drive, Photo Gallery, Mail, Messages and a lot more.

When using it as a Photo Gallery there's some extentions that do not have previews (such as HEIC and MOV), I fixed this by adding this types in the config file
```php
  'maintenance' => false,
  'enable_previews' => true,
  'enabledPreviewProviders' =>
  array (
    'OC\Preview\PNG',
    'OC\Preview\JPEG',
    'OC\Preview\GIF',
    'OC\Preview\BMP',
    'OC\Preview\XBitmap',
    'OC\Preview\MP3',
    'OC\Preview\TXT',
    'OC\Preview\MarkDown',
    'OC\Preview\OpenDocument',
    'OC\Preview\Krita',
    'OC\Preview\HEIC',
  ),
);
```

(Solution from this forum https://help.nextcloud.com/t/solved-image-previews-only-working-for-heic-photos/164302/8)