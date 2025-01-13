# Modelos

En Laravel la interacción con la base de datos se lleva a cabo a través de un _object-relational mapper_ denominado **Eloquent**. Cuando usamos Eloquent, cada tabla de nuestra base de datos tiene un modelo correspondiente que se utiliza para interactuar con la tabla. Eloquent nos permitirá también insertar, actualizar y borrar registros.

Los modelos en Laravel están alojados en "app/Http/Models".

Para crear un modelo tenemos que ejecutar:

```
php artisan make:model Product
```

Consideraciones importantes respecto al modelo:

* Eloquent asume que cada modelo está asociado a una tabla que tiene una clave primaria denominada "id". Por lo tanto, en todas nuestras migraciones usaremos el método "id" que crea dicho campo.
* Eloquent asume que el modelo "Client" guarda sus registros en una table denominada "Clients". Esto funciona correctamente con los nombres de las tablas en inglés, pero en español puede generar algún problema. Posteriormente veremos cómo resolverlo. Más información sobre los nombres de las tablas en el [siguiente enlace](https://laravel.com/docs/10.x/eloquent#table-names).
* Por defecto, Eloquent espera que estén creados los campos "created\_at" y "updated\_at". Por lo tanto, en todas nuestras migraciones utilizaremos el método "timestamps()" visto anteriormente.

Eloquent proporciona a nuestros modelos los siguientes métodos:

* Product::**all**(): devuelve todos los productos.
* Product::**pluck**("name", "id"): extrae una lista de valores de una columna específica. En el primer argumento indicamos la columna cuyos valores queremos extraer. El segundo, la columna que se usará como clave en el array resultante.&#x20;
* Product::**find**(1): devuelve el producto con id=1.
* Product::**findOrFail**(1): igual que el anterior pero devuelve una excepción si no encuentra el registro.
* Product::**create**(\['name' => 'TV', ...]): crea un nuevo registro en la base de datos.
* Product::**destroy**(1): elimina el registro con id=1.

El siguiente ejemplo muestra cómo podemos acceder al resultado de uno de los métodos anteriores:

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

## Relaciones

Pueden encontrar información sobre las relaciones en Laravel [en la documentación oficial](https://laravel.com/docs/11.x/eloquent-relationships).
