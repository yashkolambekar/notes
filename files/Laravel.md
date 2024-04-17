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

## Routes

The routes are defined in the `/routes/web.php` file, we have to define our routes there

```php
// /routes/web.php

<?php

use Illuminate\Support\Facades\Route;

Route::get('/', function () {
    return view('welcome');
});

Route::get("/yash", function(){
    return "Hello world!";
});

```

## Models

Models are the representation of Entities in the application, a model contains the structure and methods of the particular entity, Models make it easier for us to work with data, we do not need to manually create and write queries.

Models are stored in `app/Http/Models/`

We have one file for each entity, to create a model we have to run the command

```shell
php artisan make:model Customer
```

This will create a file `app/Http/Models/Customer.php`.
In this file, we may define the realtionship this model has with other models. For example

```php
// Customer.php

class Customer extends Model
{
    use HasFactory;

    public function invoices(){
        return $this->hasMany(Invoice::class);
    }

}
```

This code says that the model `Customer` shares a one-to-many relationship with the `Invoice` model.

We have to define the structure or schema of the entity in the given file at `database/migrations/`. For example, the name of the file for creation of `Invoice` in the current project is `2024_04_17_152649_create_invoices_table.php`. In this file,

```php
public function up(): void
    {
        Schema::create('invoices', function (Blueprint $table) {
            $table->id();
            $table->integer("customer_id");
            $table->integer("amount");
            $table->string("status");
            $table->dateTime("billed_at");
            $table->dateTime("paid_at")->nullable();
            $table->timestamps();
        });
    }
```

we have defined how our Invoice entity will look like.


### Faker

To start working with some dummy data, we are provided with a library called `faker` which creates dummy data at the time of creation of the tables.

To use it, firstly we need our Models and their Schemas defined as mentioned above

Then, we set up, this thing named factories inside `database/factories/`

For example, the file `CustomerFactory.php` looks like:

```php
 public function definition(): array
    {

        $type = $this->faker->randomElement(["i", "b"]);
        $name = $type == "i" ? $this->faker->name() : $this->faker->company();

        return [
            "name" => $name,
            "type" => $type,
            "email" => $this->faker->safeEmail(),
            "city" => $this->faker->city(),
            "state" => $this->faker->state(),
            "postalcode" => $this->faker->postcode(),
        ];
    }
```

This defines what type of dummy data we will like to send to the database from the faker.

Then the last step is to write a seeder which will spawn/seed our database with the required amount of data

In the `database/seeders/`, we have a `CustomerSeeder.php`

```php
public function run()
    {
        Customer::factory()->count(25)->hasInvoices(10)->create();
        Customer::factory()->count(100)->hasInvoices(5)->create();
        Customer::factory()->count(5)->hasInvoices(28)->create();
        Customer::factory()->count(5)->hasInvoices(0)->create();
    }
```

We need to import the `Customer` model here using `use App\Models\Customer;`

In the above code, 4 batches of customers are created, the `count()` defines how many customers to create, `hasInvoices()` define how many invoices that customer will have and `create()` is the final call.

Now finally, to update the changes in the datbase, we have to do

```shell
php artisan migrate:fresh --seed
```

## Routes

Firstly we should install the `api` essentials of Laravel using the command below

```shell
php artisan install:api
```

After, that we should see a `api.php` file in `routes/`

In the file, we do

```php
Route::group(['prefix'=> 'v1', 'namespace' => 'App\Http\Controllers\Api\V1'], function () {
    Route::apiResource("customers", CustomerController::class);
    Route::apiResource("invoices", InvoiceController::class);
});
```

The group, has a prefix - `v1`, which means all our URIs will be prefixed wih `http://localhost/api/v1/`. And we then define the namespace for the controllers at our location of Controllers, btw we have moved them to a subfolder named `Api/V1` for maintainbility.

And inside the Controllers, we must have the logic to return the records

```php
public function index()
    {
        return Customer::all();
    }
```

The above code returns all the Customer records, same as `SELECT * FROM Customers`

## PHP Objects to JSON

To convert the objects to JSON at the time of returning the values and to limit the fields that we return to user, we will use something called resource

to make a resource, we first initiate it using the shell

```shell
php artisan make:resource V1\SingleCustomer
```

This will create a file `app/Http/Resources/V1/SingleCustomer.php` and it will be used to work on the conversion of the data

```php
public function toArray(Request $request): array
    {
        return [
            "id" => $this->id,
            "name" => $this-> name,
            "email"=> $this->email,
            "postalCode" => $this->postalcode
        ];
    }
```

Here, we are defining what will be returned when data is sent to the `SingleCustomer` resource.

To use this, we need to import and use it in the controller

In the `Controllers/V1/CustomerController.php` we have a function named `show()` to show single customer data based on the id, here we will use our `SingleCustomer` resource

```php
public function show(Customer $customer)
    {
        return new SingleCustomer($customer);
    }
```

We passed the `$customer` object and the returned value is the JSON object as per our specifications

<br>
<br>
<br>

https://www.youtube.com/watch?v=YGqCZjdgJJk&t=1850s

Stopped at 31:12