# install package

```
composer require yousefpackage/joe-proxy
```

# then goto config folder 

in app.php


```
'providers' => [

Yousefpackage\JoeProxy\JoeProxyServiceProvider::class,

],
```

# then goto kernel.php

write this in $routeMiddleware

```
'jproxy' => \Yousefpackage\JoeProxy\Http\Middleware\LogMiddleware::class,
```

# then run this command 

```
php artisan migrate
```

# then goto env file and put this

```
MAIL_TO = "youremail"
```

# Please check that you have entered the correct information in env file 

APP_NAME
APP_URL
MAIL_MAILER
MAIL_HOST
MAIL_PORT
MAIL_USERNAME
MAIL_PASSWORD
MAIL_ENCRYPTION
MAIL_FROM_ADDRESS

# test package 

now for test this package goto your browser and write this visits-package

```
http://127.0.0.1:8000/joe-proxy
```

# using
Now Put this middleware on the route you want to calculate the number of views for.

```
->middleware('jproxy');
```

like this 

```
Route::get('/', function () {
    return view('welcome');
})->middleware('jproxy');
```

If you want to calculate the number of views you have, make a controller and then put this code

```
<?php

use Yousefpackage\JoeProxy\Models\Visit;
use Yousefpackage\JoeProxy\Models\Alert;
use Illuminate\Support\Facades\DB;

class ViewsController extends Controller
{
    function index(){

        return DB::table('logs')->select('ip')->count(); // To count the number of views 

        return Alert::all(); // If you want to know the warnings about requests
    }
}

>
```

And we find in the table that we have the visitor’s IP, his city, the page he visited and the type of his operating system
