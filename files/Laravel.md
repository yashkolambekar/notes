# Laravel

These notes are focused on RESTful API development and does not contain any frontend related topics

Please visit the official [Laravel Docs](https://laravel.com/docs/11.x/) and the [Laravel API Docs](https://laravel.com/api/11.x/index.html)

### Installation

To get started with Laravel development, we need PHP and Composer installed in our computer, once that is done we can install Laravel globally by using Composer

```shell
composer global require laravel/installer
```

Once that is done we can initialise a Laravel app anywhere we want using

```shell
laravel new app-name
```

This will create our laravel app in the app-name directory in the current directory

We can cd into it and start our laravel app using


```shell
php artisan serve
```

For the laravel app to be accesible on the local network we need to

```shell
php artisan serve --host 0.0.0.0
```

---

### Configuration

We can configure our Laravel app by modifying the values inside our `.env` file, the values for our application will be taken from there

If we want to make more configuration, we can modify the files that are situated inside the config directory. Files inside the config folder are documented using comments, so they are easy to use.

Remember : `.env` will be given priority between it and config

Database and Database Values can be edited from `.env` as well, we need to run the command

```shell
php aritsan migrate
```

to make necessary migrations in the database

**Laravel should be served only and only at the root directory of a domain and not at any subdirectory, or it will expose sensitive information about in your Laravel Project**

---

### Environment variables encryption

If we need to encrypt Environment variables in order to add them to the source control, we can run

```shell
php artisan env:encrypt
```

This will create a file named `.env.encrypted` which we can push to our github repository. We are given a key after running this command, we need to save it as it will be used at the time of decryption of the values.

When we are in the production environment, we can run

```shell
php artisan env:decrypt --key=base64:WiP4025+BA239d2cO8SGuBPelJneEfHQClc6nbU+Eew=
```

and we will have our `.env` file made

 
## Routing

We will now look at routing (or in simple words, how to create URI/URLs)

We can install the Laravel Sanctum using the `install:api` command

```php
php artisan install:api
```

This will create a new file `routes/api.php` where we can define our routes. These routes will be routed to `<example.com/api/your-route-here>`


We can edit the `/api/` prefix by editing the `bootstrap/app.php` file and adding `apiPrefix: 'hehe'` to it. So now the new routes will be `example.com/hehe/<your-route-here>`

We can listen to multiple methods on the same route

```php
Route::get($uri, $callback);
Route::post($uri, $callback);
Route::put($uri, $callback);
Route::patch($uri, $callback);
Route::delete($uri, $callback);
Route::options($uri, $callback);
```

We can also combine the methods if we need

```php
Route::match(['get', 'post'], '/', function () {
    // ...
});
 
Route::any('/', function () {
    // ...
});
```

#### Redirecting

We have the `redirect` method in routing to redirect the user

```php
Route::redirect("/original", "/new");
```

We can also pass `301` as the third parameter to specify it as a permanent redirect


We can list our routes using

```shell
php artisan route:list
```

### Parameters in Routing

While defining routes, we can define parameters within the route using `{}`

```php
Route::get("/user/{id}", function(Request $request, String $user_id){
    return "Your user id is : " . $user_id;
});
```

We can have multiple parameters in a route we just have to define them in our callback function to be able to use them. Make sure to use `String` datatype not get errors. We can get away by not defining a datatype too

The route parameter names can also be made of alphabets and underscores

#### Optional parameters

We have to add a `?` to the end of the parameter name in order to make it optional but we have to make sure that we give it a default value


```php
Route::get("/gettime/{timezone?}", function(String $timezone = "UTC"){
    // ...
})
```

The optional parameter should be at the end of URL only, cannot come in between the URL

#### Validation

We can also validate the parameters by REGEX using the `where` method

```php
Route::get('/user/{name}', function (string $name) {
    // ...
})->where('name', '[A-Za-z]+');
```

We are also provided with some helper functions which can be checked [here](https://laravel.com/docs/11.x/routing)

We can add constraints globally which will be applied to all our routes, we need to decalre this in the boot method of `App\Providers\ServiceProvider`

```php
public function boot(): void
{
    Route::pattern('id', '[0-9]+');
}
```

This constraint will be uploaded to all the route parameters

#### Forward slashes

 The forward slashes are not allowed to be a part of Route parameters, if we want them to be used. To allow forward slashes we need to allow them using the where clause. (Only allowed at the end of route)
 
 ```php
 Route::get('/search/{search}', function (string $search) {
    return $search;
})->where('search', '.*');
```

### Route Groups

This allows user to have a common prefix to multiple URLS

```php
Route::prefix('admin')->group(function () {
    Route::get('/users', function () {
        // Matches The "/admin/users" URL
    });
});
```

### 404 or Undefined

To resolve the undefined routes we can use the fallback method


```php
Route::fallback(function(){
    return "Chhote acche se baat kar";
});
```

## Middleware

Middleware are used to authenticate and allow / handle requests sent to our app.

> Remaining

## Controllers

Instead of writing the request handling logic in our root files, we define them in the Controllers which are dedicated to store functions which can be used across the app

To create controllers, we can 


```shell
php artisan make:controller UserController
```

A `UserController` file will be created in the `app\Http\Controllers` directory. We can define public functions inside it which then can be used by us everywhere

```php
public function greet(){
    return "Hello World"
}
```

And this function can be utilised by the router 

```php
Route::get("/greet", [UserController::class, "greet"]);
```

If we need to send custom arguments to the controller we can do

```php
Route::get('/user/{id}', function ($id) {
    $customArgument = 'myCustomString';
    return (new UserController)->show($id, $customArgument);
});
```

If we need to have a controller to do just one thing, we can create an `__invoke()` function in it and it will run everytime we call the controller, we can also create this type of controller directly 

```shell
php artisan make:controller ProvisionServer --invokable
```

