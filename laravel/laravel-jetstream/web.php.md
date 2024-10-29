# web.php

Al instalar JetStream se añade código a nuestro fichero web.php. Esa porción de código añade una ruta para el **dashboard** (panel de control) en tu aplicación Laravel, y utiliza middleware para restringir el acceso a esa ruta solo a los usuarios que cumplen con ciertas condiciones. Veamos cada parte:

#### Explicación detallada

1.  **Middleware**:

    ```php
    Route::middleware([
        'auth:sanctum',
        config('jetstream.auth_session'),
        'verified',
    ])->group(function () {
        // rutas aquí
    });
    ```

    * Este bloque aplica un conjunto de middleware a todas las rutas definidas dentro del `group(function () { ... })`. Esto significa que cualquier ruta dentro del grupo solo será accesible para usuarios que pasen todas las condiciones definidas en el middleware.
    * Los middleware en este caso son:
      * **`auth:sanctum`**: Asegura que el usuario esté autenticado usando Sanctum, el sistema de autenticación de Laravel. Esto significa que solo los usuarios autenticados pueden acceder a estas rutas.
      * **`config('jetstream.auth_session')`**: Esto se refiere a una configuración en `config/jetstream.php` que ayuda a manejar la sesión de usuario para mantenerla activa. Este middleware gestiona el estado de la sesión para evitar que se cierre automáticamente después de un periodo de inactividad.
      * **`verified`**: Este middleware asegura que el correo electrónico del usuario haya sido verificado. Solo los usuarios que tengan un correo verificado podrán acceder a estas rutas.
2.  **Ruta para el Dashboard**:

    ```php
    Route::get('/dashboard', function () {
        return view('dashboard');
    })->name('dashboard');
    ```

    * Esta ruta especifica que cuando se visita la URL `/dashboard`, Laravel mostrará la vista `dashboard`.
    * `->name('dashboard')` le da un nombre a la ruta (`dashboard`), que luego puede utilizarse para hacer referencia a esta ruta en el código (por ejemplo, `route('dashboard')` en un enlace).
    * Esta ruta estará protegida por el middleware aplicado. Esto significa que:
      * Solo los usuarios **autenticados** (loggeados) pueden acceder a `/dashboard`.
      * Su **sesión** debe estar activa, gracias al middleware `jetstream.auth_session`.
      * Además, el correo del usuario debe estar **verificado** para acceder a esta ruta.

En definitiva, este grupo de rutas asegura que solo los usuarios autenticados, con sesiones activas y correos verificados, puedan acceder al dashboard (`/dashboard`). Al aplicar estos middleware, Jetstream protege esta sección de la aplicación, limitando el acceso a aquellos usuarios que cumplan con estas condiciones de seguridad y autenticación.

Si quisiéramos proteger rutas ya existentes en la aplicación para que solo accedan a ellas los usuarios validados, tendríamos que añadir algo similar a esto:

```php

Route::get('/', [FormController::class, 'loadForm'])->name('doubt.form');
...

// Rutas protegidas por autenticación
Route::middleware([
    'auth:sanctum',
    config('jetstream.auth_session'),
    'verified',
])->group(function () {
    Route::get('/verDudas', [VerdudasController::class, 'loadDudas'])->name('load.dudas');
    Route::delete('/deleteDudas/{id}', [VerdudasController::class, 'deleteDudas'])->name('delete.dudas');
    ...
});

```
