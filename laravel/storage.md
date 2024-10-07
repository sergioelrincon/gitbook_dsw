# Storage

## La clase _Storage_

Laravel proporciona una capa de abstracción del sistema de ficheros que permite trabajar de forma muy sencilla con sistemas de ficheros locales, SFTP y Amazon S3.

Esto lo consigue mediante el uso de una clase denominada [Storage](https://laravel.com/api/10.x/Illuminate/Support/Facades/Storage.html). Esta clase contiene una serie de métodos que permiten la creación, borrado y movimiento de ficheros y directorios. También permite la definición del tipo de almacenamiento que vamos a utilizar (por ejemplo, el sistema de ficheros local).

Para utilizar esta clase en nuestro fichero de código, deberemos incluir esta línea al comienzo del mismo:

```
use Illuminate\Support\Facades\Storage;
```

En nuestro caso, vamos a utilizar el "disco público" ([public disk](https://laravel.com/docs/10.x/filesystem#the-public-disk)). Este repositorio utiliza la carpeta "/storage/app/public" y se utiliza para almacenar ficheros que serán accesibles desde la web.

Si queremos almacenar en ese repositorio un fichero que hemos recibido a través de un formulario, lo podemos hacer mediante el método _put_:

```
Storage::disk('public')->put(  
    $imageName,  
    file_get_contents($request->file('nombredelcampo')->getRealPath())  
);
```

*   "public" hace referencia al repositorio indicado anteriormente.

    Para que la carpeta "/storage/app/public" sea accesible a través de la web, tenemos que ejecutar desde la línea de comandos `php artisan storage:link`. Este comando crea un enlace simbólico desde "public/storage" hacia "storage/app/public". A partir de ese momento podremos referenciar a los ficheros alojados en esa carpeta mediante `asset('storage/file.txt')`, por ejemplo.

    Esto es necesario porque cuando ejecutamos nuestra aplicación, los usuarios solo pueden acceder a los ficheros alojados en la carpeta "public/". El resto de carpetas no son accesibles.
* '$imageName' contiene una string con el nombre que se le dará al fichero al almacenarlo en el repositorio.
* [$request->file('nombredelcampo')](https://laravel.com/docs/9.x/requests#files): obtiene una instancia del fichero subido en un formulario.
* [$request->file('nombredelcampo')->getRealPath())](https://www.php.net/manual/en/splfileinfo.getrealpath.php): devuelve la ruta del fichero.

Relacionado con la clase _Storage_ y con la subida de ficheros a través de formularios también tenemos el siguiente método:

* [$request->file('nombredelcampo')->extension()](https://laravel.com/docs/9.x/requests#file-paths-extensions): devuelve la extensión del fichero enviado a través del formulario.
* [$request->hasFile('nombredelcampo')](https://laravel.com/docs/9.x/requests#retrieving-uploaded-files): Comprueba si nos ha llegado a través del envío de un formulario un fichero en un campo determinado.

**NOTA:** Recuerda que cuando enviamos un fichero a través de un formulario, debemos incluir el atributo [`enctype=multipart/form-data`](https://www.php.net/manual/es/features.file-upload.post-method.php) en la declaración de dicho formulario.

### El método storage\_path()

En Laravel, cuando necesitamos almacenar archivos en el sistema de archivos del servidor, es común utilizar el método `storage_path()` para obtener la ruta al directorio de almacenamiento.&#x20;

#### **¿Qué es `storage_path()`?**

* **Función de Ayuda de Laravel**:
  * `storage_path()` es una función de ayuda (helper) proporcionada por Laravel.
  * Devuelve la ruta absoluta al directorio `storage` de tu aplicación.
* **Uso Básico**:
  *   Sintaxis:

      ```php
      $ruta = storage_path($path = '');
      ```
  *   Si proporcionas un `$path`, se anexa al directorio `storage`. Por ejemplo:

      ```php
      $ruta = storage_path('app/doubts.csv');
      ```

      Esto dará como resultado la ruta completa al archivo `doubts.csv` dentro del subdirectorio `app` del directorio `storage`.

#### **¿Por qué usar `storage_path()`?**

* Las rutas de archivos pueden variar entre sistemas operativos (Windows, Linux, macOS). `storage_path()` garantiza que obtienes una ruta correcta independientemente del sistema donde se ejecute la aplicación.
* Si la estructura del proyecto cambia o si se configura una ruta de almacenamiento personalizada, `storage_path()` siempre apuntará al directorio correcto.
* Laravel organiza los archivos de la aplicación en directorios específicos para mantener una estructura clara.
* El directorio `storage` está destinado a archivos generados por la aplicación, como logs, cachés y archivos subidos.
* Almacenar archivos en `storage` sigue las convenciones de Laravel y facilita el mantenimiento y comprensión del código.
* Los archivos en el directorio `storage` no son accesibles directamente desde el navegador

***

#### **Ejemplo práctico**

Al almacenar el archivo:

```php
// Ruta del archivo CSV
$filePath = storage_path('app/doubts.csv');

// Abrir o crear el archivo
$file = fopen($filePath, 'a');

// Escribir los datos en el archivo
fputcsv($file, $data, ';', '"');

// Cerrar el archivo
fclose($file);
```

* **Lo que hace `storage_path('app/doubts.csv')`**:
  * Si tu aplicación está en `/var/www/html/mi_aplicacion`, entonces:
    * `storage_path()` devuelve `/var/www/html/mi_aplicacion/storage`.
    * Al pasar `'app/doubts.csv'`, obtienes `/var/www/html/mi_aplicacion/storage/app/doubts.csv`.
  * Esta ruta apunta al archivo `doubts.csv` dentro del directorio `storage/app`.

####
