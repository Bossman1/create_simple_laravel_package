<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400"></a></p>

- Make ```Packages/Laravel/PackageName``` directory in root laravel project

- Inside this folder type command ```composer init``` and follow steps provided by composer init

  - in base ```composer.json```  file set path to new package
     
     ```
    'autoload': {
         "psr-4": {
            "Laravel\\PackageName\\": "Packages/Laravel/PackageName/src"
        }
     },
    ```
- Run command ```composer dump-autoload```

- Create ServiceProvider  , In root directory type command   ```php artisan make:provider PackageNameServiceProvider```  and from Providers folder move it in ```"Packages/Laravel/PackageName/src"``` folder,  register it in ```config/app.php``` file inside providers array  <small>(exp: Laravel\Test\PackageNameServiceProvider::class)</small>

- Make controller: ```php artisan make:controller PackageNameController -r```  and move it in ```"Packages/Laravel/PackageName/src"``` folder

- Create view ```"Packages/Laravel/PackageName/src/views/test.blade.php"```

- In controller ```index()``` function return view  ```return view('Laravel.PackageName.views.test');```

- Create ```"Packages/Laravel/PackageName/src/routes.php"``` file and put inside
```
   	use Illuminate\Support\Facades\Route;

   	Route::resource('/test', \Laravel\PackageName\PackageNameController::class);
```
- in  PackageNameServiceProvider.php put:
```
        $this->loadRoutesFrom(__DIR__."/routes.php");
        $this->loadViewsFrom(__DIR__."/views", "test");
        $this->publishes([
            __DIR__."/views" => base_path('resources/views/Laravel/Test/views')
        ]);

```
- Publishing:   ```php artisan vendor:publish --provider="Laravel\Test\PackageNameServiceProvider"```

- You can test plugin with to access this url: <link>yourSite.lc/test</link>
 
