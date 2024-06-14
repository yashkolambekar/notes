# Laravel 

Laravel notes from the tutorial

## Inertia

Inertiajs is used as a glue between React and Laravel, it ensures smooth functioning of our SPA using Laravel.

## Models

```shell
php artisan make:model Project -fm
```

This will create a model with the name 'Project' and the `-fm` flag makes factory and migration for tha model along the side of the model.


## Migrations

Migration files are used to create and modify database tables.

<details>
    <summary>Example of a migration table create function</summary>

```php
public function up(): void
    {
        Schema::create('tasks', function (Blueprint $table) {
            $table->id();
            $table->string("name");
            $table->longText("descripton")->nullable();
            $table->string('image_path')->nullable();
            $table->string("status");
            $table->string("priority");
            $table->timestamp("due_date")->nullable();
            $table->foreignId("assigned_user_id")->constrained("users");
            $table->foreignId("created_by")->constrained("users");
            $table->foreignId("updated_by")->constrained("users");
            $table->foreignId("project_id")->constrained("projects");
            $table->timestamps();
        });
    }
```
</details>


## Factories

Factories are used to manufacture fake data as per the migration files

<details>
    <summary>Example of a Factory</summary>

```php
 public function definition(): array
    {
        return [
            'name' => fake()->name(),
            'descripton' => fake()->realText(),
            'due_date' => fake()->dateTimeBetween("now", "+1 year"),
            'status' => fake()->randomElement(['pending', 'in_progress', 'completed']),
            'priority' => fake()->randomElement(['low', 'medium', 'high']),
            'image_path' => fake()->imageUrl(),
            'assigned_user_id' => 1,
            'created_by' => 1,
            'updated_by' => 1,
            'project_id' => fake()->biasedNumberBetween(1, 30, 'sin')
        ];
    }
```

</details>


## Seeders

Seeders are used to seed the database, we have to call the factory from a seeder to make factories work

<details>
    <summary>
    Example of a Seeder
    </summary>

```php
public function run(): void
    {
        // User::factory(10)->create();

        User::factory()->create([
            'name' => 'Yash',
            'email' => 'yash@gmail.com',
            'password' => bcrypt('123123123'),
            'email_verified_at' => time()   
        ]);

        Project::factory()->count(30)->hasTasks(30)->create();

    }
```    
</details>


## Controllers

Controllers in Laravel are used for logic and communication between the routes and model, to make a controller we have to do

```shell
php artisan make:controller ProjectController --model=Project --requests --resource
```
 
The flags here do the following things

`--model=Project` tells that the controller is being made for the Project model

`--requests` tells that 

`--resource` tells that this controller is a resource controller and hence Laravel gives us some predefined functions