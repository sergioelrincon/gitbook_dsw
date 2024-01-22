# Bases de datos

Laravel soporta ([actualmente](https://laravel.com/docs/10.x/database#introduction)) los siguientes sistemas gestores de bases de datos:

* MariaDB 10.10+
* MySQL 5.7+&#x20;
* PostgreSQL 11.0+&#x20;
* SQLite 3.8.8+&#x20;
* SQL Server 2017+&#x20;

### Migraciones

Las migraciones de Laravel nos proporcionan una especie de "control de versiones" para nuestra base de datos. A través de ellas podremos crear y modificar las diferentes tablas que la conforman.

Para crear una migración en Laravel tenemos que ejecutar:

```
php artisan make:migration create_users_table
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

Podemos conocer todos los tipos de campos en [https://laravel.com/docs/10.x/migrations#available-column-tfacaypes](https://laravel.com/docs/10.x/migrations#available-column-types)

Además de [crear tablas](https://laravel.com/docs/10.x/migrations#creating-tables), como en el ejemplo anterior, podemos [modificarlas ](https://laravel.com/docs/10.x/migrations#updating-tables)y [renombrarlas/borrarlas](https://laravel.com/docs/10.x/migrations#renaming-and-dropping-tables).&#x20;

### Configuración de la BD a través del fichero .env

Para ejecutar las migraciones tenemos que modificar el fichero .env alojado en la carpeta principal del proyecto. En él debemos especificar el nombre de la BD, el usuario y la contraseña.

### Ejecución de migraciones

Para ejecutar las migraciones debemos lanzar el siguiente comando:

```
php artisan migrate
```

Si quisiéramos revertir una migración anterior tendríamos que ejecutar:

`php artisan migrate:rollback`&#x20;

Esto afectaría al último lote de migraciones ejecutado. Por cada ejecución del comando anterior se deshace un nuevo lote.

Podemos consultar las migraciones que se han ejecutado consultando la tabla "migrations" de la base de datos.

Nunca deberíamos eliminar ni modificar ficheros de migraciones que se hayan ejecutado. En todo caso, deberíamos hacer un rollback del lote donde se haya ejecutado la migración y después modificaríamos/eliminaríamos el fichero.

Si quisiéramos borrar las tablas de todas las migraciones y ejecutarlas de nuevo, podríamos ejecutar el comando:

`php artisan migrate:fresh`

También podemos ejecutar un comando que invoca al método down() de todas las migraciones y posteriormente las ejecuta:

`php artisan migrate:refresn`

Sin embargo, este comando no nos resuelve el problema en todos los casos, dado que elimina todas las tablas y las crea nuevamente. Si queremos realizar una pequeña modificación lo más conveniente es utilizar este tipo de migraciones:

`php artisan make:migration add_campo_to_tabla_table`

En este caso, en el método up() crearemos el nuevo campo siguiendo la misma sintaxis, y en el método down() la eliminaremos con una invocación similar a esta:

`$table->dropColumn('columna');`

Podemos encontrar la documentación oficial sobre las modificaciones de campos en el [siguiente enlace](https://laravel.com/docs/10.x/migrations#column-modifiers).

