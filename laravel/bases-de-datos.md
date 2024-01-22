# Bases de datos

Laravel soporta 4 sistemas gestores de base de datos: MySQL, PostgreSQL, SQLite y SQL Server.

### Migraciones

Las migraciones de Laravel nos proporcionan una especie de "control de versiones" para nuestra base de datos. A través de ellas podremos crear y modificar las diferentes tablas que la conforman.

Para crear una migración en Laravel tenemos que ejecutar:

```
php artisan make:migration create_products_table
```

El comando anterior creará una migración de la tabla de horarios en la carpeta "database/migrations". Cada migración tiene asociada un timestamp que permite determinar su orden.

El fichero generado contendrá una clase con dos métodos: "up" y "down". El método "up" se usará para añadir nuevas tablas, columnas o índices a nuestra base de datos. El comando "down" hace lo contrario.

El método "up" que se genera tiene, por defecto, el siguiente código:

```
Schema::create('products', function (Blueprint $table) {
    $table->id();
    $table->timestamps();
});
```

Nosotros deberíamos editar dicho método, mantener los campos actuales y añadir las columnas correctas junto a su tipo siguiendo el formato:

```
$table-><tipo>("<nombredelcampo>");
```

Por ejemplo:

```
$table->string("username");
```

El método "timestamps" creará las columnas "created\_at" y "updated\_at".

Podemos conocer todos los tipos de campos en [https://laravel.com/docs/10.x/migrations#available-column-types](https://laravel.com/docs/10.x/migrations#available-column-types)

### Configuración de la BD a través del fichero .env

Para ejecutar las migraciones tenemos que modificar el fichero .env alojado en la carpeta principal del proyecto. En él debemos especificar el nombre de la BD, el usuario y la contraseña.

Para ejecutar las migraciones debemos lanzar el siguiente comando:

```
php artisan migrate
```
