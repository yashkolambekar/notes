# Laravel

Any request made to the app goes to the `/public/index.php` file and then actions are taken from thereon, there is no specific code in that file, it works kind of like a router.

## Installation

To install laravel globally on your device, we have to do

```shell
composer global require laravel/installer
```

and then, we can create a new laravel project

```shell
laravel new example-app
```

and then all the on screen instructions shall be followed

if we are planning to use the laravel project as a backend api we shall also do

```shell
php artisan install:api
```

## Routes

We can set routes using the `Routes` provided by Laravel, we have `routes/web.php` file which let's us specify routes for our website

```php
Route::get('/', function () {
    return view('welcome');
});

Route::get("/hello", function (){
    return "Hello by Laravel";
});
```

We also have different route files for console, api and other such methods. `web.php` is for webapp

We get 7 methods in web.php such as get, post, patch, delete, update.

We can also add parameters in the routes to have dynamic data in our webapp, the dynamic variable are passed as arguments to the anonymous functions in the router.


```php
Route::get("/money/{amt}/{currency}", function(string $amt, string $curr){
    return "Money = " . $amt . " " . $curr;
});
```

In the above example, going to `localhost/money/1200/INR` will return **Money = 1200 INR**

We can do the command below to show all the registered routes that are created by us in our app

```shell
php artisan route:list --except-vendor
```