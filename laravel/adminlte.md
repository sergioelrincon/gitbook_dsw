# AdminLTE

## **¿Qué es AdminLTE?**

AdminLTE es una plantilla de administración basada en Bootstrap que facilita la creación de paneles de administración o interfaces de usuario para aplicaciones web. Ofrece una gran variedad de componentes de interfaz, como tablas, gráficos, formularios y widgets, que podemos integrar fácilmente en nuestras aplicaciones Laravel. Su diseño moderno y funcional nos permite tener una interfaz de administración atractiva sin necesidad de desarrollar elementos visuales desde cero.

## **¿Para qué sirve?**

AdminLTE nos permite agregar rápidamente una interfaz de administración completa y profesional en Laravel. Esto es ideal cuando necesitamos un panel de control para gestionar datos, reportes o cualquier funcionalidad administrativa. AdminLTE ahorra tiempo al evitar que diseñemos desde cero, permitiéndonos enfocarnos en la lógica de nuestra aplicación.

## **Instalación de AdminLTE en Laravel**

Para integrar AdminLTE en Laravel, seguiremos estos pasos básicos:

1.  **Instalación del paquete de AdminLTE**

    Primero, instalamos el paquete que nos proporciona la plantilla de AdminLTE. Usamos el siguiente comando en la consola:

    ```bash
    composer require jeroennoten/laravel-adminlte
    ```
2.  **Publicar los recursos**

    Ahora que tenemos el paquete instalado, publicamos los archivos de configuración y vistas. Esto nos permitirá personalizar AdminLTE en nuestro proyecto:

    ```bash
    php artisan adminlte:install
    ```
3.  **Configuración del archivo de configuración `config/adminlte.php`**

    Después de instalarlo, podemos personalizar AdminLTE en el archivo `config/adminlte.php`. Aquí configuramos el título, el logo, el menú, y otros elementos de la interfaz.
4.  **Creación de vistas con la plantilla AdminLTE**

    Podemos crear vistas que extiendan la plantilla principal de AdminLTE. Para ello, editamos nuestras vistas Blade y usamos la plantilla `adminlte::page`:

    ```php
    @extends('adminlte::page')
    ```

    Dentro de esta plantilla, podemos colocar nuestros propios contenidos y aprovechar los componentes que AdminLTE ofrece, como formularios, tablas, y gráficos.
5.  **Personalización del menú**

    Configuramos el menú de navegación en `config/adminlte.php`, añadiendo enlaces a las diferentes secciones de nuestra aplicación. Esto permite que nuestro panel de administración sea intuitivo y fácil de navegar.

## Documentación oficial

[https://github.com/jeroennoten/Laravel-AdminLTE/wiki/](https://github.com/jeroennoten/Laravel-AdminLTE/wiki/)

