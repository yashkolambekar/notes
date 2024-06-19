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
    
}

```
</details>

### Using Controllers to Return Data

Now, we can use these controllers to perform actions and return output to routes

For, example

```php
public function announce(Request $request){
    return "Hello World this is an important announcement";
}
```

This is an method from the AppController, we can call it on a specific route


```php
Route::get('/', [AppController::class, 'announce']);
```

The first argument in the above code is the route, which is `/` and second is the array, in which first defines the name of the controller that we have to work with (it has to be imported in the file) and second is the function that we have to work with


### Accessing  Route Parameters in the Controller

This will be our route declaration

```php
Route::get('/about/{your_name?}', [AppController::class, 'about']);
```

This will be our controller method

```php
public function about(Request $request){
    $name = "";
    if(strlen($request->route('your_name')) > 0){
        $name = $request->route('your_name');
    }
    return "Dear ". $name  . " About us: We don't trust you";
}
```

This function adds your optional query parameter in the returned data. We use the `route` method to do that. And we can use the `query` method to take the input of normal queries which are given like `?name=Yash`

## Blade

`.blade.php` files are used in Laravel to make views, it is a very convenient tool instead of using plain php.

We start and end php in a blade file using `@php` and `@endphp`

```php
@php
    $hello_world = "Hello world, greetings from us"
@endphp
```

To echo variables in the blade file, we have to do `{{$variable_name}}`

```php
<h1>Hello, {{$username}}</h1>
```

## Migrations


To make a migration, we have to first use shell

```shell
php artisan make:migration create_parties_table
```

Remember, the name of the Tables are plural and the name of Models are singular

<details>
<summary>
A migration file will look something like this
</summary>

```php
public function up(): void
    {
        Schema::create('parties', function (Blueprint $table) {
            $table->id();
            $table->string("full_name", 100);
            $table->string("phone_number", 15);
            $table->timestamps();
        });
    }
```
</details>

 This is how the schema for table is defined, we can add additional constraints on top of the columns using the `->` methods

 ```php
$table->string("phone_number", 15)->unique(); // a constraint
 ```

 All these values that we define are mandatory, they have to be filled, to make a value otpional, we have to add a column modifier which will make that column `nullable`


 ```php
$table->string('address')->nullable();
 ```

It means that address column can also have null as the value, which means it can be skipped as well.

## Models

Models are the representation of the tables that are in our database. Models represent the entities in our Relational Database.

We have to create a model using the commands

```shell
php artisan make:model Party
```

Once it is made, we can require it in our Controller by doing `use App\Models\Party`

Then, it provides us a lot of methods to work with the Model and Database, let's have a look at it.

### Declaring Fillables

Before we perform any actions using the Model, we have to declare the fillables, meaning, the fields in the database that we will work with

```php
class Party extends Model
{
    use HasFactory;

    // Fillable columns
    protected $fillable = ["full_name", "phone_number", "country"];

}
```

So, we have declared that the Party model has 3 fillables, and we will be allowed to insert only these three values using our Model.

### Create a record

```php
$params = [
    "full_name" => "Yash",
    "phone_number" => 9988886622,
    "country" => "Bharat"
];

Party::create($params);
```

### Showing all records

```php
$parties = Party::all();
dd($parties); // or echo $parties;
```

### Showing record by using 'id'

```php
$id = 12;
$party = Party::find(12);
dd($party);
```

### Showing record by some other column

```php
$party = Party::where("phone_no", "12910912");
dd($party);
```

### Update record

```php
$id = 12;
$party = Party::find(12);
$party->full_name = "Jignesh Kumar";
$party->save(); 
```

### Delete record

```php
$id = 12;
$party = Party::find(12);
$party->delete(); 
```

All the above things that we saw with regards to the Model were using the Eloquent ORM which is a very user friendly way of interacting with the DB.

We also have DB Facade which we can use, but it ignores the Model and directly interacts with the DB. We need at some places, but Eloquent ORM shall be used mainly.