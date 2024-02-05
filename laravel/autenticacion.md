# Autenticación

Laravel dispone de varios [sistemas de autenticación](https://laravel.com/docs/10.x/starter-kits). Nosotros utilizaremos _laravel/ui_, ya que es el único que no requiere frameworks CSS o Javascript adicionales (Tailwind CSS, React, Vue, etc.).

La instalación de _laravel/ui_ se realiza a través del siguiente comando:

```
composer require laravel/ui
```

También necesitamos generar la estructura de ficheros de Bootstrap necesarios para implementar las pantallas de inicio de sesión. Para ello tendremos que ejecutar el comando que se muestra a continuación, **teniendo en cuenta** que debemos responder que "no" cuando nos pregunte si queremos sobreescribir los ficheros "app.blade.php" y "HomeController.php".

```
php artisan ui bootstrap --auth
```

La ejecución del comando anterior generará los siguientes cambios:

* Se creará la carpeta "app/Http/Controllers/Auth".
* Se creará la carpeta "resources/views/auth".
* Se modificará el fichero "routes/web.php".

Posteriormente tendremos que modificar lo siguiente:

* Eliminar la siguiente línea del fichero "web.php", ya que nuestra aplicación no tiene la ruta "/home": ~~Route::get('/home', \[App/Http/Controllers/HomeController::class, 'index'])->name('home');~~
* Cambiar la constante "HOME" del fichero "app/Providers/RouteServiceProvider.php" para que apunte a nuestra ruta principal. Este valor lo utiliza Laravel para redirigir al usuario después de validarse.

### Laravel Middleware

Laravel Middleware nos permite establecer restricciones en nuestra aplicación para controlar el acceso a determinadas páginas. Por ejemplo, impidiendo acceder a un usuario básico acceder al panel de control de nuestra aplicación y redirigiéndolo a la página principal.

Para crear un nuevo middleware, tenemos que ejecutar lo siguiente:

```
php artisan make:middleware AdminAuthMiddleware
```

El nuevo middleware se creará en "app/Http/Middleware/AdminAuthMiddleware.php" y mediante su método "handle" podremos establecer las restricciones que queramos. Por ejemplo:

```
use Illuminate\Support\Facades\Auth;
...
if (Auth::user() && Auth::user()->getRole() == 'editor') {  
    return $next($request);  
} else {  
    return redirect()->route('error.user');  
}
```

De esta forma, se permite al usuario acceder a la ruta solo si su rol es "editor" y en caso contrario se la redirije a una página de error.

En nuestro fichero "web.php" debemos incluir el siguiente código para controlar el acceso a las rutas que deseemos. La forma de hacerlo es la siguiente:

```
Route::middleware('editor')->group(function () {
    Route::get('/publicar', 'App\Http\Controllers\Admin\AdminPubController@index')->name("admin.pub.index");
    ...
});
```

Además, también tendremos que registrar el middleware en "app/Http/Kernel.php", añadiendo la línea `'editor' => \App\Http\Middleware\AdminAuthMiddleware::class,` al array $routeMiddleware.
