# Autenticación

Las versiones actuales de Laravel permiten usar varios [subsistemas de autenticación](https://laravel.com/docs/10.x/starter-kits). Podemos optar por instalar uno de ellos, pero en nuestro caso utilizaremos _laravel/ui_, ya que es bastante sencillo de instalar y utilizar.

La instalación de _laravel/ui_ se realiza a través del siguiente comando:

```
composer require laravel/ui
```

Este comando instala las librerías necesarias en la carpeta "vendor". Sin embargo, también necesitamos generar la interfaz de usuario de inicio de sesión y registro de usuarios con Bootstrap . Para ello tendremos que ejecutar el comando que se muestra a continuación, **teniendo en cuenta** que debemos responder que "no" cuando nos pregunte si queremos sobreescribir los ficheros "app.blade.php" y "HomeController.php".

```
php artisan ui bootstrap --auth
```

La ejecución del comando anterior generará los siguientes cambios:

* Se creará la carpeta "app/Http/Controllers/Auth" que incluye nuevos controladores, como LoginController y RegisterContrroller.
* Se creará la carpeta "resources/views/auth" que incluye algunas vistas, como la de login y la de registro de usuario.
* Se modificará el fichero "routes/web.php" para incluir la ruta /home y varias rutas de autenticación.

Posteriormente tendremos que modificar lo siguiente:

* Eliminar la siguiente línea del fichero "web.php", ya que nuestra aplicación no tiene la ruta "/home": ~~Route::get('/home', \[App/Http/Controllers/HomeController::class, 'index'])->name('home');~~
* Cambiar la constante "HOME" del fichero "app/Providers/RouteServiceProvider.php" para que apunte a nuestra ruta principal. Este valor lo utiliza Laravel para redirigir al usuario después de validarse.

### Laravel Middleware

Laravel Middleware nos permite innpeccionar y filtrar peticiones HTTP de acceso a nuestra aplicación para establecer restricciones y así controlar el acceso a determinadas rutas. Por ejemplo, impidiendo acceder a un usuario básico  al panel de control de nuestra aplicación y redirigiéndolo a la página principal o a una pantalla de error.

Para crear un nuevo middleware, tenemos que ejecutar lo siguiente:

```
php artisan make:middleware AdminAuthMiddleware
```

El nuevo middleware se creará en "app/Http/Middleware" varias clases que, mediante el método "handle", nos permitirá establecer las restricciones de acceso en función del perfil de usuario. Por ejemplo, en "AdminAuthMiddleware.php" podemos implementar en el método "handle" un código similar a éste para permitir el acceso solo a los usuarios con perfil "admin" :

```
use Illuminate\Support\Facades\Auth;
...
if (Auth::user() && Auth::user()->getRole() == 'admin') {  
    return $next($request);  
} else {  
    return redirect()->route('error.user');  
}
```

De esta forma, se permite al usuario acceder a la ruta solo si su rol es "admi" y en caso contrario se la redirije a una página de error.

En nuestro fichero "web.php" debemos  conectar el middleware anterior con la ruta correspondiente , incluyendo el siguiente código asociado a las rutas que deseemos:

```
Route::middleware('admin')->group(function () {
    Route::get('/admin', 'App\Http\Controllers\Admin\AdminHomeController@index')->name("admin.pub.index");
    ...
});
```

Además, también tendremos que  editar el fichero  "app/Http/Kernel.php"  para asociar el rol con el cotrolador correspondiente.Para ello añadimos  la línea siguiente al array $routeMiddleware:

&#x20;`'admin' => \App\Http\Middleware\AdminAuthMiddleware::class,`
