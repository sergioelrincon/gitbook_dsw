# Modelos

En Laravel la interacción con la base de datos se lleva a cabo a través de un _object-relational mapper_ denominado **Eloquent**. Cuando usamos Eloquent, cada tabla de nuestra base de datos tiene un modelo correspondiente que se utiliza para interactuar con la tabla. Eloquent nos permitirá también insertar, actualizar y borrar registros.

Los modelos en Laravel están alojados en "app/Http/Models".

Para crear un modelo tenemos que ejecutar:

```
php artisan make:model Product
```

Consideraciones importantes respecto al modelo:

* Eloquent asume que cada modelo está asociado a una tabla que tiene una clave primaria denominada "id". Por lo tanto, en todas nuestras migraciones usaremos el método "id" que crea dicho campo.
* Eloquent asume que el modelo "Cliente" guarda sus registros en una table denominada "Clientes". Esto se aplica a todos los modelos. Más información sobre los nombres de las tablas en [el siguiente enlace](https://laravel.com/docs/8.x/eloquent#table-names).
* Por defecto, Eloquent espera que estén creados los campos "created\_at" y "updated\_at". Por lo tanto, en todas nuestras migraciones utilizaremos el método "timestamps()" visto anteriormente.

Eloquent proporciona a nuestros modelos los siguientes métodos:

* Product::all(): devuelve todos los productos.
* Product::find(1): devuelve el producto con id=1.
* Product::findOrFail(1): igual que el anterior pero devuelve una excepción si no encuentra el registro.
* Product::create(\['name' => 'TV', ...]): crea un nuevo registro en la base de datos.
* Product::destroy(1): elimina el registro con id=1.

El siguiente ejemplo muestra cómo podemos acceder al restultado de uno de los métodos anteriores:

```
$product = Product::findOrFail(1);  
echo $product->name; # prints the product’s name  
echo $product["name"]; # prints the product’s name
```

Eloquent almacena los atributos del modelo en un atributo de la clase (un array) denominado `$attributes`.

Para utilizar un modelo determinado en nuestros controladores deberemos insertar la siguiente línea de código al comienzo del fichero correspondiente:

```
use App\Models\Product;
```

## La clase _Storage_

Laravel proporciona una capa de abstracción del sistema de ficheros que permite trabajar de forma muy sencilla con sistemas de ficheros locales, SFTP y Amazon S3.

Esto lo consigue mediante el uso de una clase denominada [Storage](https://laravel.com/api/9.x/Illuminate/Support/Facades/Storage.html). Esta clase contiene una serie de métodos que permiten la creación, borrado y movimiento de ficheros y directorios. También permite la definición del tipo de almacenamiento que vamos a utilizar (por ejemplo, el sistema de ficheros local).

Para utilizar esta clase en nuestro fichero de código, deberemos incluir esta línea al comienzo del mismo:

```
use Illuminate\Support\Facades\Storage;
```

En nuestro caso, vamos a utilizar el "disco público" ([public disk](https://laravel.com/docs/9.x/filesystem#the-public-disk)). Este repositorio utiliza la carpeta "/storage/app/public" y se utiliza para almacenar ficheros que serán accesibles desde la web.

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
