# supports virtual hosting settings for Laravel8

## 目的資料夾架構

網站根目錄
hostpath/public_html

上傳目錄-
由於cpanel不能產生捷徑, 所以上傳路徑設定在public_html下的storage實體目錄

hostpath/public_html/storage

laravel主程式目錄
hostpath/system

## 修改過程以原來的目錄架構表示

    步驟1

打開 public/index.php

找到有 
```php
__DIR__.'/../ 
```
的地方

改成
```php
__DIR__.'/../system/
```

例如
```php
require __DIR__.'/../vendor/autoload.php';
```
改成
```php
require __DIR__.'/../system/vendor/autoload.php';
```



    步驟2 設定指令能使用

打開 server.php 
```php
if ($uri !== '/' && file_exists(__DIR__.'/public'.$uri)) {
    return false;
}

require_once __DIR__.'/public/index.php';
```
改成
```php
if ($uri !== '/' && file_exists(__DIR__.'/../public_html'.$uri)) {
    return false;
}

require_once __DIR__.'/../public_html/index.php';
```


    步驟3 設定儲存路徑

打開 config/filesystems.php

找到public的部分
```php
'root' => storage_path('app/public'),
```
改成
```php
'root' => public_path('../../public_html/storage'),
```

    步驟4 放入對應資料夾

`除了public之外的資料都放入system目錄`
`public內的資料放入public_html`







