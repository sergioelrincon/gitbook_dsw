# Laravel Debugbar

## Introducción

Laravel Debugbar es una herramienta muy útil que añade una barra de depuración en la parte inferior de las páginas de nuestra aplicación Laravel. Esta barra nos permite ver información detallada sobre el rendimiento de nuestra aplicación, consultas SQL, rutas, variables, excepciones, entre otros elementos. Resulta especialmente útil durante el desarrollo, ya que facilita la identificación de errores y la optimización del código.

## **Instalación de Laravel Debugbar**

1.  **Instalación vía Composer**\
    En la terminal, dentro de la carpeta del proyecto Laravel, ejecutamos el siguiente comando para instalar Laravel Debugbar:

    ```bash
    composer require barryvdh/laravel-debugbar --dev
    ```

    La opción `--dev` asegura que el paquete solo se instale en el entorno de desarrollo y no en producción.
2.  **Publicación de la configuración (Opcional)**\
    Una vez instalado, podemos publicar el archivo de configuración de Debugbar para ajustarlo a nuestras necesidades:

    ```bash
    php artisan vendor:publish --provider="Barryvdh\Debugbar\ServiceProvider"
    ```

    Esto generará un archivo `debugbar.php` en la carpeta `config`, donde podemos ajustar configuraciones como activar o desactivar Debugbar en determinados entornos.
3. **Verificación**\
   Ahora, al cargar cualquier página de nuestra aplicación en el navegador, deberíamos ver la barra de depuración en la parte inferior. Si no se muestra, es posible que necesitemos activar el modo de depuración en Laravel (`APP_DEBUG=true` en el archivo `.env`).

## **Uso Básico**

La barra de depuración nos ofrece pestañas donde podemos ver:

* **Tiempo de carga**: Nos muestra el tiempo de carga de la página y cada consulta realizada.
* **Consultas SQL**: Permite ver todas las consultas que Laravel ha ejecutado en la página actual.
* **Rutas**: Visualiza las rutas activas y la información de la ruta actual.
* **Excepciones y Errores**: Muestra errores y excepciones que puedan estar afectando al funcionamiento.

