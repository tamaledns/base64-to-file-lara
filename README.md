# Base64 file to FileUpload Laravel
Convert base64 String to Upload File of Laravel

## Requirements
php >= 8.0

## Installation
composer require tamaledns/base64-to-file-lara

## Example
### Create File
* Create an instance of the class `Base64ToFile`

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use tamaledns\Base64ToFile\Base64ToFile;

class FileController extends Controller
{
    public function save_base64 (Request $request) {
        $Base = new Base64ToFile($request->base64file);
    }
}
```
+ With the instance created, you will be able to access the data in the file, as well as save in the Storage of the project.

## Get file information
### Get filename
```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use tamaledns\Base64ToFile\Base64ToFile;

class FileController extends Controller
{
    public function save_base64 (Request $request) {
        $Base = new Base64ToFile($request->base64file);
        $filename = $Base->getFilename(); // example: return 'f485fd45-640c-4eac-ae13-b97088b089f5'
    }
}
```
**NOTE:**
returns a random alphanumeric name created by Laravel's Illuminate\Support\Str::class, which will be unique each time the class is instantiated

### Get extension file
```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use tamaledns\Base64ToFile\Base64ToFile;

class FileController extends Controller
{
    public function save_base64 (Request $request) {
        $Base = new Base64ToFile($request->base64file);
        $ext = $Base->getExtension(); // example: return 'png'
    }
}
```

## Get File Type
```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use tamaledns\Base64ToFile\Base64ToFile;

class FileController extends Controller
{
    public function save_base64 (Request $request) {
        $Base = new Base64ToFile($request->base64file);
        $filetype = $Base->getFileType(); // example: return 'image/jpeg'
    }
}
```

## Get Full Path
```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use tamaledns\Base64ToFile\Base64ToFile;

class FileController extends Controller
{
    public function save_base64 (Request $request) {
        $Base = new Base64ToFile($request->base64file);
        $fullpath = $Base->getFullPath(); // example: return 'f485fd45-640c-4eac-ae13-b97088b089f5.jpg'
    }
}
```

## Get File to Save
```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use tamaledns\Base64ToFile\Base64ToFile;

class FileController extends Controller
{
    public function save_base64 (Request $request) {
        $Base = new Base64ToFile($request->base64file);
        $file = $Base->file();
        $fullpath = $Base->getFullPath();
        $file->storeAs('assets/files/', $fullpath);
    }
}
```

## Get all file info like array
```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use tamaledns\Base64ToFile\Base64ToFile;

class FileController extends Controller
{
    public function save_base64 (Request $request) {
        $Base = new Base64ToFile($request->base64file);
        /**
        * This function return a array
        * return [
        *   'file'      => Illuminate\Support\Str::class,
        *   'extension' => 'png',
        *   'filename'  => 'f485fd45-640c-4eac-ae13-b97088b089f5,
        *   'full_path' => 'f485fd45-640c-4eac-ae13-b97088b089f5.jpg',
        *   'file_type' => 'image/jpeg'
        * ]
        **/
        $info = $Base->getAllinfo();
        // Save File nto Storage
        $info['file']->storeAs('assets/files/', $info['full_path']);
    }
}
```

## License
This package is licensed under the terms of the MIT licence
