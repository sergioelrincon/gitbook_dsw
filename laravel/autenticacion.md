# Autenticación

Para implementar la autenticación de usuarios en Laravel, puedes aprovechar el sistema de autenticación que Laravel proporciona de forma predeterminada. Para ello tendrás que seguir los siguientes pasos:

#### 1. **Instalar Laravel Breeze (para autenticación básica)**

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

#### 2. **Configurar rutas protegidas**

Una vez que tengas el sistema de autenticación configurado, puedes proteger rutas específicas para que solo usuarios autenticados puedan acceder a ellas.

Por ejemplo, si tienes una ruta a la que solo quieres que accedan usuarios autenticados, puedes usar el middleware `auth` en tus rutas de la siguiente manera:

```php
Route::get('/dashboard', function () {
    return view('dashboard');
})->middleware('auth');
```

Esto garantiza que solo los usuarios autenticados puedan acceder a `/dashboard`. Si un usuario no autenticado intenta acceder a esta ruta, será redirigido automáticamente a la página de inicio de sesión.

#### 3. **Personalizar el sistema de autenticación**

Si necesitas personalizar la autenticación (por ejemplo, agregar nuevos campos al registro de usuario o personalizar el flujo de autenticación), puedes modificar los controladores generados por Breeze que están en `app/Http/Controllers/Auth`.

También puedes modificar las vistas que Breeze genera, las cuales se encuentran en `resources/views/auth`.

####
