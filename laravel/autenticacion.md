# Autenticación

Para implementar la autenticación de usuarios en Laravel, puedes aprovechar el sistema de autenticación que Laravel proporciona de forma predeterminada. Para ello tendrás que seguir los siguientes pasos:

### **Instalar Laravel Breeze (para autenticación básica)**

Laravel Breeze es un paquete ligero para la autenticación de usuarios, y es la opción recomendada para empezar. Aquí te explico cómo usar Breeze:

**Paso 1: Instalar Breeze**

Primero, asegúrate de tener instalado el paquete Breeze. Puedes agregarlo a tu proyecto ejecutando:

```bash
composer require laravel/breeze --dev
```

**Paso 2: Ejecutar la instalación de Breeze**

Después de instalar el paquete, debes generar los archivos de autenticación y vistas básicas ejecutando:

```bash
php artisan breeze:install
```

Esto te configurará las rutas, controladores y vistas necesarias para registro, inicio de sesión, y manejo de usuarios.

Durante la instalación nos preguntará qué stack nos gustaría instalar. Seleccionaremos "Blade with Alpine"

**Blade** es el motor de plantillas nativo de Laravel que estamos usando, lo cual hace que esta opción sea la más directa. **Alpine.js** es una librería JavaScript minimalista, que permite agregar pequeñas interacciones sin la complejidad de frameworks más grandes como Vue o React. Esta opción es ideal si buscamos una solución ligera y fácil de entender, sin necesidad de incluir un framework de frontend robusto. De esta forma seguiremos usando las vistas Blade, que ya conocemos, con el añadido de Alpine.js para manejar interactividad sencilla.

**Paso 3: Ejecutar las migraciones**

El sistema de autenticación de Laravel utiliza una tabla de usuarios. Para crear esta tabla, ejecuta las migraciones. Si ya las has ejecutado anteriormente (como probablemente será nuestro caso), posiblemente no se ejecute ninguna migración:

```bash
php artisan migrate
```

**Paso 4: Iniciar el servidor**

Con eso hecho, puedes iniciar el servidor de Laravel:

```bash
php artisan serve
```

### **Configurar rutas protegidas**

Una vez que tengas el sistema de autenticación configurado, puedes proteger rutas específicas para que solo usuarios autenticados puedan acceder a ellas.

Por ejemplo, si tienes una ruta a la que solo quieres que accedan usuarios autenticados, puedes usar el middleware `auth` en tus rutas de la siguiente manera:

```php
Route::get('/dashboard', function () {
    return view('dashboard');
})->middleware('auth');
```

Esto garantiza que solo los usuarios autenticados puedan acceder a `/dashboard`. Si un usuario no autenticado intenta acceder a esta ruta, será redirigido automáticamente a la página de inicio de sesión.

### **Personalizar el sistema de autenticación**

Si necesitas personalizar la autenticación (por ejemplo, agregar nuevos campos al registro de usuario o personalizar el flujo de autenticación), puedes modificar los controladores generados por Breeze que están en `app/Http/Controllers/Auth`.

También puedes modificar las vistas que Breeze genera, las cuales se encuentran en `resources/views/auth`.

### Creación de usuarios

Dado que Breeze nos proporciona una interfaz de registro funcional, también podemos simplemente acceder a la ruta de registro, que por defecto es `/register`. Allí puedes crear el primer usuario de manera gráfica.

Podemos acceder a la ruta `register` (o cualquier ruta relacionada con autenticación, como `login` y `logout`), aunque no aparezcan explícitamente en el archivo `web.php`, es porque esas rutas están definidas en el archivo `auth.php`, que se incluye al final de tu archivo `web.php` con esta línea:

```php
require __DIR__.'/auth.php';
```

#### ¿Qué contiene el archivo `auth.php`?

Cuando ejecutamos el comando `php artisan breeze:install`, Breeze generó un conjunto de rutas preconfiguradas para manejar el registro, inicio de sesión, restablecimiento de contraseñas, etc. Estas rutas están definidas en el archivo `routes/auth.php`, que fue creado automáticamente.

Si abres `auth.php`, deberías ver algo similar a esto:

```php
<?php

use App\Http\Controllers\Auth\AuthenticatedSessionController;
use App\Http\Controllers\Auth\RegisteredUserController;
use App\Http\Controllers\Auth\PasswordResetLinkController;
use App\Http\Controllers\Auth\NewPasswordController;
use App\Http\Controllers\Auth\EmailVerificationPromptController;
use App\Http\Controllers\Auth\VerifyEmailController;
use App\Http\Controllers\Auth\EmailVerificationNotificationController;
use App\Http\Controllers\Auth\ConfirmablePasswordController;
use App\Http\Controllers\Auth\PasswordController;
use Illuminate\Support\Facades\Route;

Route::middleware('guest')->group(function () {
    Route::get('register', [RegisteredUserController::class, 'create'])
                ->name('register');

    Route::post('register', [RegisteredUserController::class, 'store']);

    Route::get('login', [AuthenticatedSessionController::class, 'create'])
                ->name('login');

    Route::post('login', [AuthenticatedSessionController::class, 'store']);

    Route::get('forgot-password', [PasswordResetLinkController::class, 'create'])
                ->name('password.request');

    Route::post('forgot-password', [PasswordResetLinkController::class, 'store'])
                ->name('password.email');

    Route::get('reset-password/{token}', [NewPasswordController::class, 'create'])
                ->name('password.reset');

    Route::post('reset-password', [NewPasswordController::class, 'store'])
                ->name('password.update');
});

Route::middleware('auth')->group(function () {
    Route::get('verify-email', [EmailVerificationPromptController::class, '__invoke'])
                ->name('verification.notice');

    Route::get('verify-email/{id}/{hash}', [VerifyEmailController::class, '__invoke'])
                ->middleware(['signed', 'throttle:6,1'])
                ->name('verification.verify');

    Route::post('email/verification-notification', [EmailVerificationNotificationController::class, 'store'])
                ->middleware('throttle:6,1')
                ->name('verification.send');

    Route::get('confirm-password', [ConfirmablePasswordController::class, 'show'])
                ->name('password.confirm');

    Route::post('confirm-password', [ConfirmablePasswordController::class, 'store']);

    Route::put('password', [PasswordController::class, 'update'])->name('password.update');

    Route::post('logout', [AuthenticatedSessionController::class, 'destroy'])
                ->name('logout');
});
```

#### ¿Cómo funciona?

* Las rutas como `/register`, `/login`, y `/logout` están definidas en este archivo.
* Estas rutas están protegidas o abiertas dependiendo de los **middlewares** que las envuelven. Por ejemplo:
  * `Route::middleware('guest')` agrupa las rutas a las que solo pueden acceder los invitados (es decir, usuarios no autenticados), como el registro y el inicio de sesión.
  * `Route::middleware('auth')` agrupa las rutas a las que solo pueden acceder los usuarios autenticados, como la verificación de email y el cierre de sesión.

Por eso, aunque no veamos las rutas explícitamente en `web.php`, están siendo incluidas gracias a la línea `require __DIR__.'/auth.php';`, que hace referencia a este archivo y agrega esas rutas al sistema de enrutamiento de Laravel.

#### ¿Qué hacer si no quieres que los usuarios se puedan registrar?

Si quieres deshabilitar el registro de usuarios (por ejemplo, si prefieres crear los usuarios manualmente o usar otro método), simplemente puedes comentar o eliminar las rutas relacionadas con el registro en `auth.php`:

```php
// Elimina o comenta estas líneas
Route::get('register', [RegisteredUserController::class, 'create'])->name('register');
Route::post('register', [RegisteredUserController::class, 'store']);
```

Con esto, los usuarios no podrán acceder a `/register` ni registrar nuevas cuentas en el sistema.

####
