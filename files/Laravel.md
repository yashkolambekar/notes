# Laravel

These notes are focused on RESTful API development and does not contain any frontend related topics

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


---

### Routing

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
Route::get('/user/{id}/{name}', function (string $id, string $name) {
    // ...
})->where(['id' => '[0-9]+', 'name' => '[a-z]+']);
```