# Introducción

## ¿Qué es Laravel?

Laravel es un framework que nos proporciona un conjunto de herramientas y recursos que nos facilitan la creación aplicaciones web en PHP.

El objetivo de Laravel es conseguir que la implementación de aplicaciones sea un proceso sencillo para el desarrollador, sin por ello sacrificar funcionalidades.

_Happy developers make the best code"_ (https://laravel.com/docs/4.2/introduction)

## MVC

MVC (Modelo-Vista-Controlador) es el patrón de arquitectura de software que sigue Laravel. Permite separar las funcionalidades de cada parte del código. Enfatiza la separación de la lógica de programación respecto a la presentación. Esto hará que el código esté más ordenado y sea más fácil de mantener.

* **Modelo:** encargado de todas las interacciones con la base de datos (obtener, consultar, actualizar, eliminar...). No muestra la información. De ello se encarga la vista. El modelo no actualiza la información directamente; es el controlador quien decide cuándo llamarlo.
* **Vista:** se encarga de todo lo que se ve en pantalla. Laravel tiene un template engine llamado _Blade_ que muestra los datos. El modelo consulta la BD, pero el controlador decide qué vista hay que llamar y qué datos presentar.
* **Controlador:** comunica modelo y vista. Antes de que el modelo consulte la BD, el controlador es el encargado de llamar a un modelo específico. Una vez consultado el modelo, el controlador recibe la información, llama a la vista y le pasa la información.

Un concepto muy importante en Laravel es el de **Router**. El router (/routes/web.php) es el encargado de registrar todas las URL o endpoints que va a soportar nuestra aplicación. Asociado a cada ruta existe un controlador que sabe qué modelo debe llamarse y qué vista mostrar cuando el usuario visita dicha ruta o endpoint.

![mvc](img/mvc.png)

## Instalación del entorno de trabajo

### Windows

* Instalar Composer ([https://getcomposer.org/doc/00-intro.md#using-the-installer](https://getcomposer.org/doc/00-intro.md#using-the-installer))\
  Composer es un gestor de dependencias para PHP. Es una herramienta que facilita la instalación y actualización de las bibliotecas y paquetes que necesita un proyecto PHP, de manera que se evite tener que hacer todo manualmente. Laravel, como muchos frameworks, tiene varias dependencias (bibliotecas de código que necesita para funcionar), y Composer se encarga de descargarlas e instalarlas automáticamente. De esta forma, no tenemos que preocuparnos por buscar, descargar y configurar cada uno de esos componentes, ya que Composer hace el trabajo por nosotros.&#x20;
  * Comprobar la instalación mediante la ejecución de `composer --version`
*   Crear un nuevo proyecto Laravel:

    ```
    composer create-project laravel/laravel <nombredelaaplicacion>
    ```
* Acceder a ella a través de http://127.0.0.1/\<nombredelaaplicacion>

![localhost](img/localhost.png)



## Artisan

_Artisan_ es el nombre del CLI que incluye Laravel. Permite crear migraciones, controladores, modelos, policies y mucho más.

Se puede invocar, desde el directorio de la aplicación, mediante el comando `php artisan...`

## Estructura de carpetas de Laravel

De momento, destacamos los siguientes directorios/ficheros de la estructura de un proyecto Laravel:

* **./app/Http/Controllers**: aquí alojaremos nuestros controladores.
* **./app/Models**: en esta carpeta estarán nuestros modelos.
* **./database/migration**: definiremos las migraciones (definiciones del esquema de la base de datos) en esta carpeta
* **./public**: contendrá imágenes, hojas de estilo y código Javascript. La parte pública que ve el usuario. También se aloja en esta carpeta el fichero _index.php_, que es el punto de entrada a la aplicación.
* **./resources/views**: carpeta donde se alojan las vistas.
* **./routes**: carpeta donde están las rutas. Entre otros ficheros, destacamos _web.php_ que es el que define las rutas de la interfaz web.
* **./storage**: donde se suben los ficheros generados por el usuario.
* **./vendor**: donde se colocan las dependencias de composer.
* **./env**: contiene parámetros de configuración que pueden variar en función de dónde se esté ejecutando la aplicación (nombre de la base de datos, usuario y contraseña, etc.).

## Git

Por defecto, al crear un proyecto Laravel, se genera un fichero ".gitignore" que incluye una serie de ficheros y carpetas específicos de cada usuario, que no se deberían subir a un repositorio Git. Esos directorios y ficheros son imprescindibles para ejecutar la aplicación Laravel. Para generarlos, después de hacer un clon del repositorio, deberemos ejecutar los siguientes comandos dentro de la carpeta del proyecto:

* composer install
* cp .env.example .env
* php artisan key:generate
* touch database/database.sqlite
* php artisan migrate

## Extensiones para Visual Studio Code

Te recomiendo instalar "Laravel Blade Snippets", "Laravel Snippets", "Laravel goto view" y "Laravel Extra Intellisense".&#x20;

## Varios

* `\{\{ \}\}`: Lo podemos encontrar en ficheros Blade. Procesa lo que está en el interior como código PHP, para mostrar el resultado. Es como hacer un echo. Por ejemplo, `{{1+1}}` mostraría 2. También se utilizan para invocar helpers. Y para mostrar información pasada a la vista.
