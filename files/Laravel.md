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




---

We can do the command below to show all the registered routes that are created by us in our app

```shell
php artisan route:list --except-vendor
```














Youtube Playlist: 

https://www.youtube.com/playlist?list=PL0b6OzIxLPbz7JK_YYrRJ1KxlGG4diZHJ

Video 13 (Controllers) about to start