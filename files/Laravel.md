# Laravel

https://www.youtube.com/playlist?list=PL0b6OzIxLPbz7JK_YYrRJ1KxlGG4diZHJ

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

### Paramters in Routes

We can also add parameters in the routes to have dynamic data in our webapp, the dynamic variable are passed as arguments to the anonymous functions in the router.

```php
Route::get("/money/{amt}/{currency}", function(string $amt, string $curr){
    return "Money = " . $amt . " " . $curr;
});
```

In the above example, going to `localhost/money/1200/INR` will return **Money = 1200 INR**

We can also set a parameter as optional by adding a question mark at the end of the parameter's name in the route, for example

```php
Route::get("/post/{id?}", function(string $id=nul){
    return "POST ID = " . $id;
})
```

As we can see, we also added the default argument in the function parameters. We can use if else functions to do conditional rendering based on the parameters

We can also add constraints for the route parameters using the inbuilt methods

```php
Route::get("/debit/{amount}", function(string $amt){
    return "Debited ".$amt."";
})->whereNumber("amount");
```

In the above code `whereNumber("amount")` makes sure that the rout is triggered only when the amount is a number or else it will not be triggered. There are more constraints available such as `whereAlpha`, `whereAlphaNumeric`, etc.

We can also chain these constraints one after the another to apply multiple constraints.

### Named Routes

If we are using blade templates and come across a point where we have to give an anchor tag like this: `<a href='/company/about'>`, we might use it thousands of times throughout the website, and then if we change the website route structure, we will have to update the href tags everywhere, instead of doing that, we give a name to our route while deinfing it

```php
Route::get("/company/about-us", function(){
    return view("aboutcompany");
})->name("about");
```

and we use it in our blade templates :

```php
<a href="{{route('about')}}">About us</a>
```

### Redirect

We can set redirects in the router

```php
Route::redirect("/old", "/new");
```

We can also specify a third parameter for redirect codes, generally we should need only these

- 307 : Temporary Redirect
- 308 : Permanent Redirect

### Route group

We can create a group and a prefix to the routes, makes it less repetitive and grouped

```php
Route::group(["prefix"=>"/user"], function(){

    Route::get("/delete", function(){
        return view("deleteuser");
    })

    Route::get("/create", function(){
        return view("create");
    })

});
```

For example, in the above code, `http://localhost/user/delete` will render the `deleteuser` view.

### Fallback / 404

This will serve the page for all routes that do not exist, basically the 404 page.

```php
Route::fallback(function(){
    return "chal chalke dikha";
});
```

---

We can do the command below to show all the registered routes that are created by us in our app

```shell
php artisan route:list --except-vendor
```

## Blades

To echo something in page, we have to do

```php
<h1>{{"Hello there, " . $user}}</h1>
```

The `<?php ?>` are replaced by `{{}}` and we do not need to specify an echo as well, but this is only for echo and some other blade specific features

But this only echos the string as it is, we cannot use it to echo, for example `<h1>This is my heading</h1>`, the whole thing will be printed as a simple string inside <p>

To print html we have to use this syntax:

```php
{!! "<h1>This is my heading</h1>" !!}
```

### Writing php code in blade

To write php code in blade, we have to do:

```php
@php
    Your php code here
@endphp

{{-- This is a comment --}}
```

### If else condition in blade

```php
@if($yash == 1)
    {{"Yash is true"}}
@elseif($yash == 19)
    {{"Yash is 19"}}
@else
    {{"Yash is none"}}
@endif

```

### Switch condition

```php
@switch($i)
    @case(1)
        {{"i is one"}}
        @break
    @case(2)
        {{"i is two"}}
        @break
    @default
        {{"i is not one or two"}}
@endswitch
```

### Isset in blade

```php
@isset($message)
    {{$message}}
@endisset
```

This is same as the if(isset()) in php

### Empty

```php
@empty($records)
    {{"The records are empty"}}
@endempty
```

### For loop

```php
@for($i = 0; $i < 0; $i++)
    {{"The current value is $i"}}
@endfor
```

### Foreach loop

```php
@foreach($users as $user)
    {{"This is a user with name: $user"}}
@endforeach
```

### While

```php
@while($condition)
    {{"True"}}
@endwhile
```

@continue and @break also exist in blade templates

## Directives

### @include

The @include directive is used to include (kind of spawn) any view inside the current view, we can, for example include a view inside a div, then, the views will work like components

```php
<h1>Welcome to my website</h1>
<h2>About me :</h2>
<div style="padding:10px">
    @include("about")
</div>
```

We can also send variables to the included view by giving a second argument which will be an array

```php
@include("post", ['post_id' => 82923, 'author' => 'Yash'])
```

We can access the parameters inside the `post` view as variables, using `$post_id` and `$author`

There exists a directive named **@includeIf()** which includes the view only if the view exists

## Controller

To create a controller in Laravel, we can run this command

```shell
php artisan make:controller UserController
```

In the above code, UserController is the name of the controller that we want to make, The controller will be made in `app/Http/Controllers`

The name should be In `PascalCase`, it is recommended

Then, we can create methods in the controller that will be used

```php
class PageController extends Controller
{
    public function greet(){
        return "Jay Shree Ram bhai ji!";
    }
}
```

Then, we specify it in the router

```php
Route::get("/greet", [PageController::class, "greet"]);
```

(We also have to include the PageController using the `use` keyword)

### Controller Group in Router

We do not have to specify the Controller name again and again, we can just specify it once and include the routes under it with the method name

```php
Route::controller(PageController::class)->group(function () {
    Route::get("/greet", "greet")->name("greet");
    Route::get("/greet/{message}", "greetWithMessage")
    ->name("greetwithmessage");
});
```

### Single Action Controller

If we have a controller which does only thing, we can use it directly in the router without having to specify the method. For it to work we need to set the function name `__invoke()`

## Migration (Database)

To create tables in our database, we have to run a command in the terminal

```shell
php artisan make:migration create_students_table
```

(but we should rather make it using model command)

This will create a migration file which is used to define tables and schema. We have a function named `up()` inside the newly created migration file, we have to define schemas there.

```php
public function up(): void
    {
        Schema::create("students", function (Blueprint $table) {
            $table->id();
            $table->string("name", 30);
            $table->string("city", 15);
        });
    }
```

The `Schema::create` creates a new table.

It's first argument is the table name <br>
The second argument is a function which takes in `Blueprint $table` as the argument and then columns are defined inside that function

After all that is done, we have to run the migrate command

```shell
php artisan migrate
```

### Updating the Table

We have to create migrations for that as well

```shell
php artisan make:migration update_students_table --table=students
```

We have to give the --table flag, it is important

Then we can add things in there as we want

Remember: DO NOT DELETE Migration files, make new to update the stuff, but never delete.

### Rename Columns

```php
$table->renameColumn('from', 'to');
```

### Drop / Delete columns

```php
$table->dropColumn("city");  // single
$table->dropColumn(["city", "street", "pin"]); // multiple
```

### Change / Update columns

```php
$table->string("city", 100)->change();
$table->string("city", 100)->unsigned()->change();
```

### Rename Table

```php
$table->rename("from", "to");
```

### PRIMARY KEY

```php
$table->primary('user_id');
```

### FOREIGN KEY

```php
$table->unsignedBigInteger("id");
$table->foreign("user_id")->references("id")->on("users");
```

Remember that the default datatype of `id()` is `Unsigned Big Integer`

### Run SQL commands

If we want to run any SQL statements

```php
DB::statement("ALTER TABLE users ADD CONSTRAINT age CHECK (age < 18);");
```

### Constraints

- **NOT NULL**

  ```php
  ->nullable();
  ```

- **UNIQUE**

  ```php
  ->unique();
  ```

- **DEFAULT**

  ```php
  ->default("value");
  ```

- **Invisible** \
  This makes the column invisible to normal SQL queries such as SELECT, can be used for password columns or other such sensitive information

  ```php
  ->invisible();
  ```

- **Unsinged** \
  This makes the INTEGER unsigned, so it cannot be set to a negative value

  ```php
  ->unsigned();
  ```

## Seeding

Seeding means to add fake / temporary data in the fields to work with some dummy data.

First we create a model using the artisan command

```shell
php artisan make:model ModelName
```

Then, we create a seeder file using the artisan command

```shell
php artisan make:seeder SeederName
```

After that is done, we have to define what data we have to insert, inside the Seeder file:

```php
use App\Models\student;
.
.
.
public function run(): void
    {
        student::create([
            "name" => "Yash",
            "email" => "y@yassh.in",
            "class" => "13th"
        ]);
    }
```

Then, we call this seeder inside the DatabaseSeeder file

```php
public function run(): void
    {
        $this->call([StudentSeeder::class]);
    }
```

We can add multiple seeders in the array of seeders to call them.

TO insert multiple records at once

```php
$students->each(function ($student) {
            student::create([
                "name" => $student->name,
                "email" => $student->email
            ]);
        });
```

Here, the `$students` must be a `collect`

We have to compulsorily have timestamps() in our schema if we are using the create method

### Fake records

```php
for( $i = 0; $i < 10; $i++ ){
    student::create([
        "name" => fake()->name(),
        "email" => fake()->email()
    );
}
```

## Factory 

Factories allows us to easily populate our datbases with fake data

First we need to create a model 

```shell
php artisan make:model student
```

Then we create the factory

```shell
php artisan make:factory studentFactory
```

after this, we specify what fake data we need inside the newly created factory

```php
public function definition(): array
{
    return [
        "name" => fake()->name(),
        "email" => fake()->email()
    ];
}
```

after this, we go to include the file in the DatabaseSeeder.php file and after that we specify how many counts of data we want

```php
public function run(): void
{
    student::factory()->count(10)->create();
}
```

here, we are creating 10 records of students from the fake methods we have specified in the student factory

To create the model and factory together with one command, we can do

```shell
php artisan make:model teacher -f
```

The `-f` flag makes the factory


# On video 20