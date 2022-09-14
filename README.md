# virtual hosting settings for Laravel8 supports
# E.g:cpanel

## 目的資料夾架構

通常使用像cpanel這類平台他的public_html上一層都還會放很多系統檔案
所以我是把除了public的檔案放進laravelapp這個目錄, 看起來比較乾淨

laravel主程式目錄
hostpath/laravelapp

網站根目錄
hostpath/public_html

上傳目錄-
由於cpanel不能產生捷徑, 所以上傳路徑設定在public_html下的storage實體目錄
hostpath/public_html/storage

## 修改過程以原來的目錄架構表示

    步驟1

打開 public/index.php

找到所有 
```php
__DIR__.'/../ 
```
的地方

取代成
```php
__DIR__.'/../laravelapp/
```

例如
```php
require __DIR__.'/../vendor/autoload.php';
```
改成
```php
require __DIR__.'/../laravelapp/vendor/autoload.php';
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

如果有使用laravel admin可能會多一個admin上傳路徑的設定
找到admin的部分做修改
重點就是在'root' => public_path()路徑前面補上 "../../public_html" 後面通常會有自訂上傳目錄
例如
```php
'root' => public_path('../../public_html/uploads/admin'),
```

    步驟4 放入對應資料夾

`除了public之外的資料都放入laravelapp目錄`
`public內的資料放入public_html`







