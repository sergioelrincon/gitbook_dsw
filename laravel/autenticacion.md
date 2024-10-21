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

####
