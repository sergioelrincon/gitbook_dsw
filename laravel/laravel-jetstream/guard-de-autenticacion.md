# Guard de autenticación

El **guard** (o guardián de autenticación) en Laravel es un mecanismo que define cómo se autentican los usuarios y cómo se almacenan y gestionan sus sesiones dentro de la aplicación. En esencia, el guardián controla el acceso y mantiene la autenticación de los usuarios, es decir, establece qué usuario está conectado, cómo se valida y cómo se mantiene la sesión.

## **Conceptos básicos**

1. **Tipos de Guardián**:
   * Laravel tiene configurado un guardián por defecto llamado `web`, que utiliza sesiones y cookies para autenticar a los usuarios en aplicaciones web.
   * Otro guardián común es `api`, que se usa para autenticaciones en aplicaciones API sin estado (stateless), donde no se guarda la sesión, sino que se utilizan tokens para verificar a los usuarios en cada solicitud.
2. **Configuración del Guardián**:
   * Los guardianes se configuran en el archivo `config/auth.php` de Laravel. Allí, puedes ver una lista de todos los guardianes y sus configuraciones.
   * Cada guardián se asocia a un **driver** (controlador) que define cómo gestiona la autenticación. Los drivers más comunes son `session` para aplicaciones web y `token` para APIs.
3.  **Ejemplo de Configuración**:

    ```php
    'guards' => [
        'web' => [
            'driver' => 'session',
            'provider' => 'users',
        ],

        'api' => [
            'driver' => 'token',
            'provider' => 'users',
            'hash' => false,
        ],
    ],
    ```

    En este ejemplo:

    * El guardián `web` utiliza el driver `session` y está configurado para usar el proveedor `users` (la tabla de usuarios).
    * El guardián `api` usa el driver `token` y también se conecta al proveedor `users`, pero en lugar de almacenar sesiones, usa tokens de autenticación.
4. **Proveedores de Usuarios**:
   * Los guardianes se configuran con un **proveedor**, que indica cómo obtener y validar los usuarios. Normalmente, el proveedor es la tabla de usuarios de la base de datos, aunque Laravel permite otros proveedores personalizados.

## **¿Para qué se utiliza el guardián en Laravel?**

El guardián de autenticación permite:

* Mantener la sesión de un usuario cuando inicia sesión.
* Definir quién está autenticado y sus permisos en el sistema.
* Controlar el acceso a ciertas rutas y recursos dependiendo de si el usuario está autenticado o no.

####
