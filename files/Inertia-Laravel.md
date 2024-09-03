# Inertia with React + Laravel

Inertia.js is used to glue the backend with frontend in Inertia

## Steps to Install

1. Install react and react-dom

    ```shell
    npm react react-dom
    ```

2. Install vite

    ```shell
    npm i --save-dev @vitejs/plugin-react
    ```

3. Install Inertia in Composer

    ```shell
    composer require inertiajs/inertia-laravel
    ```

4. Add a app.blade.php in resources/views

    ```html
    <!DOCTYPE html>
    <html lang="en">

    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
        @vite('resources/js/app.js')
        @inertiaHead
    </head>

    <body>
        @inertia
    </body>

    </html>
    ```

5. Add inertia middleware

    ```shell
    php artisan inertia:middleware
    ```

6. Add the middleware to bootstrap/app.php

    ```php
    ->withMiddleware(function (Middleware $middleware) {
        $middleware->web(append: [
            HandleInertiaRequests::class,
        ]);
    })
    ```

7. Install inertia react

    ```shell
    npm i @inertiajs/react
    ```

8. Add code to resources/js/app.js

    ```js
    import './bootstrap';

    import { createInertiaApp } from '@inertiajs/react'
    import { createRoot } from 'react-dom/client'

    createInertiaApp({
    resolve: name => {
        const pages = import.meta.glob('./Pages/**/*.jsx', { eager: true })
        return pages[`./Pages/${name}.jsx`]
    },
    setup({ el, App, props }) {
        createRoot(el).render(<App {...props} />)
    },
    })
    ```

9. Rename the app.js to app.jsx

10. Add react in vite.config.js

    ```js
    import { defineConfig } from 'vite';
    import laravel from 'laravel-vite-plugin';
    import react from "@vitejs/plugin-react"

    export default defineConfig({
        plugins: [
            laravel({
                input: ['resources/js/app.jsx'],
                refresh: true,
            }),
            react(),
        ],
        resolve: {
            alias: {
                "@" : "/resources/js",
            }
        }
    });
    ```

11. Edit the app.blade.php file and change the app.js to app.jsx and add the react refresh

    ```html
    @viteReactRefresh
    @vite('resources/js/app.jsx')
    ```

12. Make Pages folder in resources/js folder and start defining pages/components inside that

13. Run 

    ```shell
    npm run dev
    ```

    ```shell
    php artisan serve
    ```

## Install tailwind

1. Run 

    ```shell
    npm install -D tailwindcss postcss autoprefixer
    npx tailwindcss init -p
    ```

2. Edit tailwind.config.js

    ```shell
    /** @type {import('tailwindcss').Config} */
    export default {
    content: [
        "./resources/**/*.blade.php",
        "./resources/**/*.jsx",
        "./resources/**/*.js",
    ],
    theme: {
        extend: {},
    },
    plugins: [],
    }
    ```

3. Edit resources/css/app.css

    ```css
    @tailwind base;
    @tailwind components;
    @tailwind utilities;
    ```

4. Import the css file in app.jsx

    ```jsx
    import "../css/app.css";
    ```

5. Stop and Restart the dev server

    ```shell
    npm run dev
    ```

## Routing

In the web.php file where we define our routes, we just have to return the jsx page which inertia will render


```php
Route::get("/", function(){
    return inertia("About");
});

Route::get("/about", function(){
    return inertia("About/About");
});
```

We have to define the folder name if the jsx file is inside a folder inside the Pages folder.

Instead of `inertia()` helper function, we can also use `Inertia::render()`, it does the same thing, it might be useful to know this while working in controllers

### Passing props

```php
// web.php
Route::get("/profile", function(){
    return Inertia::render("Profile", ["name"=> "Yash"]);
});
```

```jsx
// Profile.jsx
const Profile = ({name}) => {
    return(
        <>
            <p>Hello {name}</p>
        </>
    );
}
```