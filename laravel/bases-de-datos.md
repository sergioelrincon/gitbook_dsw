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

### Seeders

Un **seeder** en Laravel es una clase que se utiliza para poblar la base de datos con datos iniciales o de prueba. Es particularmente útil cuando estás desarrollando una aplicación y necesitas un conjunto de datos consistente para probar funcionalidades sin tener que ingresar manualmente la información cada vez.

#### ¿Cómo funcionan los seeders en Laravel?

1.  **Creación de seeders**: Los seeders se crean utilizando el comando Artisan de Laravel. Un seeder es básicamente una clase que tiene un método `run()` en el que defines qué datos quieres insertar en la base de datos.

    Para crear un seeder, usas el siguiente comando:

    ```bash
    php artisan make:seeder NombreDelSeeder
    ```

    Esto creará un archivo en la carpeta `database/seeders`.
2.  **Definición de datos**: Dentro del método `run()` del seeder, puedes usar los métodos de los modelos de Laravel, como `DB::table()` o el uso de los modelos directamente, para insertar los datos en la base de datos. Un ejemplo sencillo de un seeder sería:

    ```php
    <?php

    namespace Database\Seeders;

    use Illuminate\Database\Seeder;
    use Illuminate\Support\Facades\DB;

    class UsersTableSeeder extends Seeder
    {
        public function run()
        {
            DB::table('users')->insert([
                'name' => 'John Doe',
                'email' => 'johndoe@example.com',
                'password' => bcrypt('password'),
            ]);
        }
    }
    ```

    En este ejemplo, el seeder está insertando un usuario en la tabla `users`.
3.  **Ejecución de seeders**: Una vez que hayas creado y configurado tu seeder, puedes ejecutarlo usando el siguiente comando:

    ```bash
    php artisan db:seed --class=UsersTableSeeder
    ```

    También puedes ejecutar todos los seeders a la vez (si has configurado varios en el archivo `DatabaseSeeder`):

    ```bash
    php artisan db:seed
    ```
4.  **Uso de Factories**: Laravel también ofrece una manera más avanzada de poblar la base de datos mediante el uso de **factories**. Los factories permiten generar datos aleatorios para poblar la base de datos con ejemplos de registros. Puedes combinarlos con los seeders para generar múltiples registros de manera automática y con datos variados. Un ejemplo sería:

    ```php
    public function run()
    {
        \App\Models\User::factory(10)->create();
    }
    ```

    Este código creará 10 usuarios aleatorios usando el factory del modelo `User`. Por lo tanto, es fundamental crear previamente el modelo antes de utilizar los Factories.

#### Resumen del flujo de trabajo:

1. Creas un seeder con `php artisan make:seeder`.
2. Definir los datos que quieres insertar en el método `run()`.
3. Ejecutas el seeder con `php artisan db:seed` o `php artisan db:seed --class=NombreDelSeeder`.
4. Opcionalmente, puedes combinar seeders con factories para generar datos de prueba automáticamente.



