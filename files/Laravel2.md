# Laravel 2

(2nd file not Version 2.0)


## MVC

**MVC** stands for Model View Controller.

- **Model** has the responsiblity for operations related to Data and Database.

- **View** is the end result / page that is shown to the user, the visual content. This is not required in Laravel as an API

- **Controller** is the logical part of the application, it contains the core logic. It is a meditator betwween the Model and View.

## Routes

Routes are defined in the routes folder, we have web.php for web routes and api.php for api routes although we need to install the api routes using `php artisan install api`

The example below is a basic route:

```php
Route::get("/Hello", function(){
    return "Hello World";
});
```

The example below includes a parameter from the url

```php
Route::get("/index/{name}", function($name){
    return "Index page" . " " . $name;
});
```

To make this parameter optional, we have to add a question mark after the declaring the param in the url `/index/{name?}`

We can assign names to the routes using the `->name()` method. 

```php
Route::get("/program/signup", function(){
    return view('signup')
})->name('registration');
```

The name of this route is `registration` which can be used at many places to address that particular route. These are called named routes, this feature is useful because we can change the physical address of a route without making any changes in the program code. The name is like a variable name for that route.

## Controller 

```shell
php artisan make:controller AppController 
```

'AppController' is the name of the controller that we have made, this controller will made under app/Http/Controllers

<details>
<summary>
An empty controller looks like this
</summary>

```php
<?php

namespace App\Http\Controllers; // the location of this file

use Illuminate\Http\Request;

// AppController is a inhertired class of the Controller class
class AppController extends Controller 
{
    //
}

```
</details>