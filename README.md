# Laravel + React 

<h1>Laravel React Bank Accounts Panel</h1>

<p>A modern and intuitive web application built with <strong>Laravel</strong> and <strong>React</strong> for managing bank accounts. This project provides a sleek and responsive user interface for viewing, adding, editing, and deleting bank accounts, all backed by a robust <strong>Laravel</strong> API for seamless data management. It combines the power of <strong>Laravel</strong> for backend development and the dynamic nature of <strong>React</strong> for front-end interactions.</p>

<h2>Features</h2>
<ul>
    <li><strong>User Authentication</strong>: Secure login and registration system powered by Laravel's built-in authentication.</li>
    <li><strong>Bank Account Management</strong>: Add, edit, view, and delete bank account details.</li>
    <li><strong>Responsive UI</strong>: Built with React and styled with modern CSS frameworks for a seamless experience across devices.</li>
    <li><strong>API Integration</strong>: A RESTful API built with Laravel to handle all operations securely and efficiently.</li>
    <li><strong>Data Validation</strong>: Ensures that all data inputs, such as account numbers and balances, are validated on both the client and server sides.</li>
    <li><strong>Role-Based Access</strong>: Allows for different levels of user access (admin, user) with appropriate privileges for managing bank accounts.</li>
</ul>

Back-end 
- [x] Laravel 10 + PHP 8

Front-end 
- [x] React 18 + TypeScript + Vite
- [x] React Router v6
- [x] Tailwind CSS / SASS
- [x] Node 20+

---

### Set Up 

Create `.env` file from the example
```
cp .env.example .env
```

Generate an application key
```
php artisan key:generate
```

Install dependencies 
```
composer install && npm install
``` 

Run Laravel and React dev server concurrently
```
npm run dev
``` 

Preview production build 
```
npm run production
``` 

---

### Routes 

##### `routes/web.php` 

```php
Route::get('/{any}', function () {
    return view('app');
})->where('any', '^(?!api).*');
```

Home: http://localhost:8000

Login: http://localhost:8000/login

404: http://localhost:8000/i-dont-exist

##### `routes/api_v1.php` 

```php
// Authenticated API (sanctum)
Route::group([
    'middleware' => ['api_authenticated']
], function() {
    Route::get('/example-authenticated', [ExampleController::class, 'authenticated']);
});

// Public API
Route::group([
    'middleware' => ['api_public'],
], function () {
    Route::get('/example', [ExampleController::class, 'index']);
});

``` 

`API Example:` http://localhost:8000/api/v1/example 

`API Protected Example:` http://localhost:8000/api/v1/example-authenticated 

---

### Middleware Groups 

Middleware groups `web`, `api_public` and `api_authenticated` are defined in `app/Http/Kernel.php` 

---

### Vite `.env` Variables 

Any `.env` file variables prefixed with `VITE_` will be accessible in our React application using `import.meta.env`. 

This is because the `vite.config.ts` is injecting them. 

```ts
// vite.config.ts
...
    define: {
        __APP_ENV__: JSON.stringify(env.APP_ENV),
    },
...
```

To provide typings for `import.meta.env`, you can include the necessary type definitions in the `resources/app/env.d.ts` file.

---

### Laravel Docs 

https://laravel.com/docs/10.x
