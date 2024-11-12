# Personalización del idioma

Para configurar el idioma en un proyecto Laravel y utilizar el archivo `es.json` para las traducciones en español, seguiremos estos pasos:

1. **Creamos la carpeta donde se alojarán los archivos de traducción de de Laravel**\
   Primero, creamos manualmente la carpeta `resources/lang/`
2.  **Crear el archivo `es.json` para traducciones personalizadas**\
    En `resources/lang/`, creamos un archivo llamado `es.json`. Este archivo nos permitirá almacenar nuestras traducciones en formato JSON. Podemos añadir las claves y valores que necesitamos traducir. Por ejemplo:

    ```json
    {
      "Welcome": "Bienvenido",
      "Login": "Iniciar sesión",
      "Logout": "Cerrar sesión"
    }
    ```

    Cada clave representa un texto que se traducirá al español.
3.  **Configurar el idioma predeterminado en Laravel**\
    Vamos al fichero `.env` y cambiamos la opción `LOCALE` de `en` a `es`, de modo que el español sea el idioma predeterminado de nuestra aplicación:

    ```php
    APP_LOCALE=es
    ```
4.  **Usar las traducciones en nuestras vistas**\
    Para utilizar las traducciones en nuestras vistas, empleamos el helper `__('clave')` o el método `@lang('clave')` de Blade. Laravel buscará la clave en el archivo `es.json` si el idioma configurado es el español.

    Ejemplo en una vista Blade:

    ```blade
    <h1>{{ __('Welcome') }}</h1>
    <a href="{{ route('login') }}">{{ __('Login') }}</a>
    ```

    Con esto, los textos se mostrarán en español usando las traducciones definidas en el archivo `es.json`.

Siguiendo estos pasos, tendremos nuestro proyecto Laravel configurado para usar el idioma español de manera eficaz.
