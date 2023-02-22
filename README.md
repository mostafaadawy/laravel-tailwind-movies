# Laravel Movie with Tailwind

Laravel is a web application framework with expressive, elegant syntax. We believe development must be an enjoyable and creative experience to be truly fulfilling. Laravel takes the pain out of development by easing common tasks used in many web projects, such as:

- [Simple, fast routing engine](https://laravel.com/docs/routing).
- [Powerful dependency injection container](https://laravel.com/docs/container).
- Multiple back-ends for [session](https://laravel.com/docs/session) and [cache](https://laravel.com/docs/cache) storage.
- Expressive, intuitive [database ORM](https://laravel.com/docs/eloquent).
- Database agnostic [schema migrations](https://laravel.com/docs/migrations).
- [Robust background job processing](https://laravel.com/docs/queues).
- [Real-time event broadcasting](https://laravel.com/docs/broadcasting).

Laravel is accessible, powerful, and provides tools required for large, robust applications.

## Learning Laravel

Laravel has the most extensive and thorough [documentation](https://laravel.com/docs) and video tutorial library of all modern web application frameworks, making it a breeze to get started with the framework.

If you don't feel like reading, [Laracasts](https://laracasts.com) can help. Laracasts contains over 1500 video tutorials on a range of topics including Laravel, modern PHP, unit testing, and JavaScript. Boost your skills by digging into our comprehensive video library.

- `composer require laravel/sail --dev`
- `php artisan sail:install`
- `ubuntue`
- `cd` to home 
- `vim .bashrc` 
- `alias sail='[ -f sail ] && sh sail || sh vendor/bin/sail'`
- `cd ../../mnt/c/wamp/www/laravel-tailwind-movies/`
- `sail up`
- `sail artisan migrate`
- add phpmyadimn service on port 9000 in docker-compose.yml
```sh
phpmyadmin:
        depends_on:
            - mysql
        image: phpmyadmin/phpmyadmin
        environment:
            - PMA_HOST=mysql
            - PORT=3306
        networks:
            - sail
        ports:
            - 9000:80
```
- `sail up` 
- phpmyadmin root and pw from .env `sail` and `password`
- now brows database with phpmyadmin `http://localhost:9000`
# Tailwind Css
tailwind can be used with deferent platform we apply it with laravel and we will use it with `webpack.mix`
- Installing [Tailwind CSS](https://tailwindcss.com/docs/guides/laravel#mix) via `npm`
- from terminal of web container in network sail terminal `npm install -D tailwindcss postcss autoprefixer`
- Add Tailwind to your Laravel Mix configuration In your webpack.mix.js file, add tailwindcss as a PostCSS plugin.
- we `"require(tailwindcss)"` to be generated in the output of webpack, so we edit it from
```sh
mix.js('resources/js/app.js', 'public/js')
    .postCss('resources/css/app.css', 'public/css', [
        //
    ]);
```
- to be 
```sh
mix.js("resources/js/app.js", "public/js")
  .postCss("resources/css/app.css", "public/css", [
    require("tailwindcss"),
  ]);
```
- `npx tailwindcss init -p` that creates js file
- Configure your template paths Add the paths to all of your template files in your `tailwind.config.js` file edit the next code 
```sh
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [],
  theme: {
    extend: {},
  },
  plugins: [],
}
```
- to be 
```sh
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./resources/**/*.blade.php",
    "./resources/**/*.js",
    "./resources/**/*.vue",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```
- `npm run watch` in container terminal or terminal to run webpack to optimize using tailwind
- now we can use its style sheet in our layout.blade.php
- we can check that in welcome blade
remove custome blades such as
```sh
        <style>
            body {
                font-family: 'Nunito', sans-serif;
            }
        </style>
```
- then add link for stylesheet tailwind generated ` <link rel="stylesheet" href="{{ asset('/css/app.css') }}">`
