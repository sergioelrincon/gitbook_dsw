# Laravel Jetstream

## **Introducción a Laravel Jetstream**

Laravel Jetstream es un conjunto de herramientas y funcionalidades avanzadas que Laravel nos ofrece para implementar un sistema de autenticación completo en nuestras aplicaciones. Con Jetstream, podemos:

* Crear y gestionar usuarios.
* Implementar el inicio de sesión y registro de usuarios.
* Recuperar contraseñas y verificar correos.
* Administrar sesiones activas de usuario y, opcionalmente, habilitar equipos y autenticación en dos factores.

Jetstream se construye sobre **Laravel Fortify**, que proporciona las rutas y funcionalidades de autenticación. Jetstream utiliza estas funciones y añade una interfaz que se puede personalizar fácilmente para crear sistemas de autenticación robustos y listos para usarse.

**¿Qué es Laravel Fortify?** Fortify es el sistema de autenticación "sin interfaz" de Laravel. Esto significa que gestiona toda la lógica de autenticación (iniciar sesión, registro, verificación, etc.) sin crear vistas o pantallas. En cambio, Jetstream se encarga de proporcionar estas vistas y las herramientas para que el usuario interactúe con la autenticación de Fortify.

***

## **Laravel Jetstream y Livewire**

Cuando instalamos Laravel Jetstream, podemos elegir entre dos opciones para la interfaz: **Livewire** o **Inertia.js**. Para esta actividad, trabajaremos con **Livewire**, que utiliza el motor de plantillas **Blade** (que ya conocemos) para permitir una interfaz dinámica sin necesidad de JavaScript adicional.

Livewire nos permite hacer que las páginas se actualicen en tiempo real sin tener que recargar la página. Por ejemplo, si actualizamos algo en el perfil de usuario, podemos ver los cambios sin necesidad de recargar.

***

## **Instalación de Laravel Jetstream**

Para instalar Laravel Jetstream en un proyecto Laravel existente, sigue estos pasos:

1.  **Instalar Jetstream** usando Composer, que es el gestor de dependencias de PHP:

    ```bash
    composer require laravel/jetstream
    ```
2.  **Instalar la interfaz con Livewire** ejecutando el siguiente comando:

    ```bash
    php artisan jetstream:install livewire
    ```

    Este comando genera las rutas, controladores y vistas necesarias para usar Jetstream con Livewire.
3.  **Compilar los activos (CSS y JavaScript)**: Ejecuta los siguientes comandos para instalar las dependencias necesarias y compilar los recursos:

    ```bash
    npm install && npm run dev
    ```
4.  **Ejecutar migraciones** para crear las tablas necesarias en la base de datos:

    ```bash
    php artisan migrate
    ```

***

## **Archivos y carpetas importantes**

Después de instalar Jetstream, aquí tienes algunos archivos y carpetas importantes en los que trabajarás:

* **`config/fortify.php`**: Archivo de configuración donde puedes personalizar el comportamiento de Fortify, como las rutas de redirección tras la autenticación y el uso de autenticación en dos factores.
* **`resources/views`**: Carpeta donde Jetstream coloca las vistas para las páginas de autenticación y gestión de perfiles. Las vistas de Livewire están en **`resources/views`**. Por ejemplo, el diseño general se encuentra en `resources/views/layouts/app.blade.php`.
* **`app/Actions`**: Carpeta donde se encuentran las clases de "Acción". Estas clases representan una acción específica (como crear un equipo o eliminar un usuario). Puedes personalizar estas clases para cambiar el comportamiento de Jetstream en el backend.

***

## **Comando `route:list` y las rutas de Fortify**

Laravel Fortify registra automáticamente las rutas para la autenticación. Puedes ver todas las rutas disponibles en tu proyecto usando el siguiente comando en la terminal:

```bash
php artisan route:list
```

Este comando muestra una lista de todas las rutas en la aplicación, incluyendo las que Fortify registra para el inicio de sesión, registro, restablecimiento de contraseñas, etc. Al ejecutar este comando, podrás identificar las rutas para cada funcionalidad de autenticación en tu proyecto.

***

## **Personalización del perfil de usuario**

Jetstream permite añadir campos adicionales a los perfiles de usuario. Para agregar un campo, sigue estos pasos:

1.  **Crea una migración** para añadir el campo en la tabla de usuarios. En la terminal, ejecuta:

    ```bash
    php artisan make:migration add_biography_to_users_table --table=users
    ```

    Esto creará una migración en la carpeta `database/migrations`. Abre el archivo de migración y agrega el campo en la función `up`:

    ```php
    public function up()
    {
        Schema::table('users', function (Blueprint $table) {
            $table->string('biography')->nullable();
        });
    }
    ```
2.  **Ejecuta la migración**:

    ```bash
    php artisan migrate
    ```
3. **Edita la vista del perfil** para mostrar y editar el nuevo campo. La vista del perfil generalmente se encuentra en `resources/views/profile/show.blade.php`. Agrega un campo para "biografía" en el formulario.
4.  **Actualiza el modelo `User`** para permitir el nuevo campo. Abre `app/Models/User.php` y asegúrate de que `biography` esté en la lista de atributos asignables masivamente (`$fillable`):

    ```php
    protected $fillable = [
        'name',
        'email',
        'password',
        'biography', // nuevo campo
    ];
    ```

***

## **Gestión de sesiones activas**

Jetstream permite que los usuarios administren sus sesiones activas. Esto significa que un usuario puede ver en qué dispositivos o navegadores ha iniciado sesión y cerrar sesión en otros dispositivos si lo desea. Para usar esta funcionalidad:

1. **Prueba iniciar sesión en varios navegadores** o en una ventana de incógnito para crear varias sesiones.
2. **Administra las sesiones** desde la interfaz de usuario en la sección de perfil. Allí verás las sesiones activas y podrás cerrar sesión en otros dispositivos.

***

## **Autenticación de dos factores**&#x20;

Para mejorar la seguridad, puedes habilitar la autenticación de dos factores (2FA) en Jetstream. Esto permite a los usuarios configurar un segundo factor de autenticación (como un código desde una app de autenticación).

1. Abre el archivo `config/fortify.php` y habilita la autenticación de dos factores configurando la opción `features` para incluir `Features::twoFactorAuthentication()`.
2. En la sección de perfil de usuario, verás la opción para habilitar la autenticación de dos factores y se generarán códigos QR para configurarla en aplicaciones de autenticación.

***

***

## Aclaraciones

### **¿Por qué es necesario compilar los activos (CSS y JavaScript)?**

En un proyecto Laravel, los "activos" son los recursos estáticos de la aplicación, como los archivos CSS y JavaScript, que hacen que la aplicación sea visualmente atractiva e interactiva. Laravel Jetstream usa **Tailwind CSS** (para el estilo) y **JavaScript** (para la interactividad en el navegador).

Estos archivos de estilo y scripts se escriben inicialmente en un formato que es más fácil de desarrollar y organizar, pero necesitan "compilarse" para ser optimizados antes de usarlos en producción. La compilación realiza tareas como:

* **Minimización**: Reduce el tamaño de los archivos, eliminando espacios en blanco y comentarios, lo cual mejora la velocidad de carga.
* **Agrupación**: Combina múltiples archivos en uno solo, reduciendo el número de solicitudes al servidor.
* **Traspilación**: Convierte código moderno a versiones compatibles con navegadores antiguos.

### **¿Qué son los activos?**

Los activos (o "assets" en inglés) son todos los recursos de frontend (CSS, JavaScript, imágenes, fuentes) que se envían al navegador para hacer que la aplicación funcione y se vea bien. Por ejemplo:

* **CSS** para dar estilo a las páginas (colores, fuentes, diseños).
* **JavaScript** para añadir funcionalidad dinámica e interactiva.
* **Imágenes** y otros archivos multimedia que se muestran en la aplicación.

### **¿Qué es npm y por qué se utiliza en este paso?**

**npm** (Node Package Manager) es un administrador de paquetes para JavaScript. Se utiliza para instalar y gestionar dependencias de JavaScript y herramientas que ayudan en el desarrollo web.

En Laravel, **npm** se usa para:

* Instalar **Tailwind CSS** y otros paquetes de frontend.
* Ejecutar comandos como `npm run dev` para compilar los archivos CSS y JavaScript.
* Mantener los paquetes actualizados y bien organizados.

Cuando ejecutas `npm install`, npm lee el archivo `package.json` (donde están listadas las dependencias del proyecto) y descarga todos los paquetes y herramientas necesarias.

### **¿Deberías tener npm instalado?**

Sí, es necesario tener npm instalado para poder compilar los activos de Jetstream. npm se instala automáticamente con **Node.js**, por lo que solo necesitas instalar Node.js.

### **¿Cómo instalar npm (y Node.js) si no lo tienes?**

Para instalar **Node.js** (y, con él, npm):

1.  **Verifica si ya está instalado**: Abre la terminal y escribe:

    ```bash
    node -v
    npm -v
    ```

    Si aparece un número de versión, ya lo tienes instalado.
2. **Instala Node.js y npm**: Si no los tienes, sigue estos pasos:
   *   **Linux (Debian/Ubuntu)**:

       ```bash
       sudo apt update
       sudo apt install nodejs npm
       ```
   * **Windows** y **Mac**:
     * Descarga el instalador de [Node.js desde su sitio oficial](https://nodejs.org).
     * Ejecuta el instalador y sigue los pasos. Esto instalará tanto Node.js como npm.
3. **Verifica la instalación** ejecutando `node -v` y `npm -v` nuevamente para asegurarte de que estén correctamente instalados.

Con npm y Node.js instalados, puedes compilar los activos del proyecto con los comandos de npm, lo cual es esencial para ver los cambios en CSS y JavaScript en el navegador.
