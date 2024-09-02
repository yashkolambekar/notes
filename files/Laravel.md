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

> Not fully covered but covered enough I suppose


## HTTP Requests

The Request class which is situated in `Http\Illuminate\Request` provides us easy ways to deal with HTTP Requests

To use the class we just have to define it in the function parameter of the Route, it is automatically injected

```php
Route::get("/status", function(Request $request){...
```

#### Getting the path of the request

```php
$path = $request->path();
```

This will return the path of the request, not the full path, only the path after domain, basically what we define in the route generally.

To get the request url we can use the `url()` function and to get the url with the query parameters we can use the `fullUrl()` function

To remove a particular query from the url we can use 

```php
$newurl = $request->fullUrlWithoutQuery(['country']);
```

This will remove the `?country=*` from the url.

#### Getting the host

To get the host of the request or we can say to get the domain name of the request we can use

```php
$host = $request->host();
```


### Accesing Headers

To access the headers of the request, we can use 

```php
$value = $request->header('X-Header-Name');
$value = $request->header('X-Header-Name', 'default');
```

The second parameter is returned if the header is not present in the request, it is the default value

We also have a `hasHeader()` function to check if the request has the header or not


### IP Addresses

```php
$ipAddress = $request->ip();
```

This return the IP address of the request and `ips()` returns an array of addresses if they exist (if forwarded by proxies).


### Input

To get the url parameters as well as post request body values, we need to use the `input()` or `collect()` method

```php
$params = $request->input()
```

We can access the one parameter at a time using by passing it in the function

```php
$product = $request->input("product");
```

We can pass second parameter to set a default value as well, if the parameter in the request is non existent

```php
$product = $request->input("cart.products.0");
```

We can also access the array and json objects using the dot `.` notation

#### For query

If we want to perform all this to just the query string, we can do it with the `query()` method.


### Input presence

To check if the input has certain params we can use `has` method


```php
if($request->has("id")){
    // ---
}
```

We can also pass an array of strings so the function will evaluate true only when all of those parameters are available. We also have a `hasAny()` method which evaluates as true when atleast 1 parameter is available.

### Input presence + not null

```php
if($request->filled("phone"){
    // ---
})
```

We also have `anyFilled` function which can match any of the following options from the given array

### Files

```php
$file = $request->file('photo');
```

We are also provided with the `hasFile` option which will help us check if the file exists

We also have a `->isValid()` method to check if s file was uploaded successfully without any errors

We are provided with `path()` and `extension()` method which can be used to detect the path of the file and extension of the file


#### Saving the file

We get the `store()` method to save the uploaded file in a directory under the `/storage/app` directory.

```php
$request->file('photo')->store("assets");
```

The uploaded file with the name `photo` will be saved in the /storage/app/assets directory with a random name

We can assign a custom name to that file using `storeAs` method, but we also have to define the extension in the name

```php
$request->file("photo")->store('assets', 'mywallpaper.jpg');
```

## Responses

We can return plaintext responses but that is not advised, we are advised to use the response object for the purpose of sending reponses

```php
Route::get('/home', function () {
    return response('Hello World', 200)
                  ->header('Content-Type', 'text/plain');
});
```

We can chain headers to the response object for better access

```php
return response($content)
            ->header('Content-Type', $type)
            ->header('X-Header-One', 'Header Value')
            ->header('X-Header-Two', 'Header Value');
```

#### Redirect using the response

We can redirect using the response 

```php
Route::get('/dashboard', function () {
    return redirect('/home/dashboard');
});
```

To external domains

```php
return redirect()->away('https://www.google.com');
```

#### Json responses

```php
return response()->json([
    'name' => 'Abigail',
    'state' => 'CA',
]);
```


### Downloads

The file downloads response basically forces users to download the files at the given path

```php
return response()->download($pathToFile);
return response()->download(storage_path('app/photos/mypics.pdf'));
```

We also have two more optional params

```php
return response()->download($pathToFile, $name, $headers);
```


#### Streamed downloads

Used to download files without saving to disk, obtained from some other stream

```php
use App\Services\GitHub;
 
return response()->streamDownload(function () {
    echo GitHub::api('repo')
                ->contents()
                ->readme('laravel', 'laravel')['contents'];
}, 'laravel-readme.md');
```


### Show Files

```php
return response()->file($pathToFile);
return response()->file($pathToFile, $headers);
```


## Validation

> Remaining


