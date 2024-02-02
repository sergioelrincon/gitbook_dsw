# Routing

Laravel routing es un mecanismo usado para enrutar todas las peticiones que llegan a nuestrea aplicación a métodos o funciones específicas que las tratarán convenientemente. Las rutas de Laravel aceptan una URI y un _closure_. Los _closure_ son una versión de PHP de lo que sería una función anónima. Un _closure_ es una función que puedes pasar como un objeto, asignar a una variable, o pasar como un parámetro a otra función o método.

Las rutas Laravel se definen en los _route files_ localizados en la carpeta _routes_.

* El fichero _routes/web.php_ define rutas a la interfaz web de la aplicación.
* El fichero _routes/api.php_ define rutas a tu API (si dispones de una). Se utilizan en arquitecturas orientadas a servicio o REST APIs.

El contenido por defecto de _routes/web.php_ es el siguiente:

```
Route::get('/', function () {
    return view('welcome');
});
```

Lo cual indica que cuando se acceda a la URL raíz de nuestra aplicación, se mostrará la vista _resources/views/welcome.blade.php_. \
\
[_view()_](https://laravel.com/docs/9.x/helpers#method-view) es un helper que devuelve una instancia de una vista.

A continuación se muestran otras formas de definir rutas en Laravel:

```
Route::get('/', function () {
    $viewData = [];
    $viewData["title"] = "Página principal - Tienda online";
    return view('home.index')->with("viewData", $viewData);
});

Route::get('/contacto', function () {
    $dato1 = "texto1";
    $dato2 = "texto2";
    return view('home.contacto')
        ->with("dato1", $dato1)
        ->with("dato2", $dato2);
});

Route::get('/about', 'App\Http\Controllers\HomeController@about')->name("home.about");
```

* La primera conecta la URI "/" con una _closure_ que devuelve una vista (home.index). Además, se le pasa la variable _viewData_ a la vista _home.index_ mediante el encadenamiento del [método _with_](https://laravel.com/docs/10.x/views#passing-data-to-views)&#x20;
* La última ruta conecta la URL "/about" con el método _about_ de la clase _HomeController_, alojado en la carpeta /App/Http/Controllers". Además, [definimos un nombre personalizado de ruta](https://laravel.com/docs/10.x/routing#named-routes) mediante el encadenamiento del método _name_ en la definición de la ruta.&#x20;

También podemos utilizar la siguiente sintaxis para relacionar URI y controlador:

`Route::get('/user', [UserController::class, 'index']);`

Las rutas también pueden incluir parámetros:

```
Route::get('/cliente/{id}', 'App\Http\Controllers\CustomerController@show');
```

Esta ruta será la encargada de gestionar peticiones del tipo "/cliente/1", por ejemplo. En este caso, al método "ver" de "CustomerController" se le enviará por parámetro el campo "$id". Su declaración deberá realizarse de la siguiente forma:

```
...
public function show($id) {
...
```

A través del comando `php artisan route:list` puedo consultar todas las rutas creadas en nuestra aplicación.

### Rutas GET

Son las rutas mostradas en el ejemplo anterior. Se utilizan para solicitar datos de un recurso específico. Por ejemplo, cuando un usuario accede a una página de nuestra aplicación, se realiza una petición GET. Estas rutas se definen con el método `get` y son las más comunes para cargar vistas o páginas.

### Rutas POST

Las rutas que utilizan el método POST se utilizan para enviar datos al servidor para crear un nuevo recurso. Por lo general, se utilizan en formularios cuando se envían datos al servidor, como la creación de un nuevo usuario o el envío de un formulario de contacto. Su formato sería el siguiente:

```
Route::post('/test/store', 'App\Http\Controllers\TestController@store')->name("test.store");
```

En este caso, el método "store" deberá definirse con un parámetro de tipo Request: `function store (Request $request)`. Dicho parámetro es un objeto que nos permitirá interactuar con la petición HTTP realizada por nuestra aplicación para acceder a las cookies, campos, ficheros, etc.

Nota: deberás incluir en el controlador la línea "use Illuminate\Http\Request;" para cargar la definición de la clase Request.

En el método "store" podremos establecer las reglas de validación de los campos recibidos. Podemos consultar información sobre las reglas de validación disponibles en [https://laravel.com/docs/10.x/validation#available-validation-rules](https://laravel.com/docs/10.x/validation#available-validation-rules). A continuación mostramos un ejemplo de validación:

```
$request->validate([  "name" => "required|max:255" ]);
```

Si la validación es exitosa el código se ejecutará correctamente. En caso contrario se generarán errores que se podrán consultar a través del objeto global "$errors". Si invocamos a `$errors->all()` podremos mostrar al usuario dichos errores.

Para crear nuevos registros a través del modelo deberemos crear un objeto de la clase del modelo correspondiente y asignarle valor a sus atributos. El valor que le debemos asignar lo obtenemos del objeto $request pasado por parámetro. Finalmente tendremos que invocar al método "save()" de dicho objeto para guardar los datos. Mostramos un ejemplo a continuación:

```
$newCar= new Car();  
$newCar->setBrand($request->input('brand'));  
$newCar->save();
```

Más información sobre el método _input_ en [https://laravel.com/docs/10.x/requests#retrieving-input](https://laravel.com/docs/10.x/requests#retrieving-input)

Para validaciones más complejas podemos hacer uso de los Form requests. Pueden consultar la documentación oficial en la [siguiente página de la documentación oficial de Laravel](https://laravel.com/docs/10.x/validation#form-request-validation).

También pueden encontrar más información sobre la personalización de los mensajes de error en la [siguiente página de la documentación oficial de Laravel](https://laravel.com/docs/10.x/validation#customizing-the-error-messages).

### Rutas DELETE

Las rutas que usan el método DELETE de HTTP se utilizan para eliminar un recurso específico. Si tenemos un registro en nuestra base de datos que deseamos permitir que los usuarios eliminen, usaríamos una ruta DELETE para manejar esa solicitud. A continuación mostramos un ejemplo:

```
Route::delete('/admin/products/{id}/delete', 'App\Http\Controllers\Admin\AdminProductController@delete')->name("admin.product.delete");
```

En este caso, la ruta tiene un parámetro ($id) que se corresponde con el identificador del registro que vamos a eliminar. Para que le llegue este parámetro a la ruta, el atributo "action" del formulario que enviará los datos debería incluir dicho parámetro. La sintaxis correcta sería la siguiente:

```
<form action="\{\{ route('admin.product.delete', $product->getId())\}\}" method="POST">
    @method('DELETE')
    <button>
        Eliminar
    </button>
</form>
```

Hay que prestar atención al uso de la directiva [`@method`](https://laravel.com/docs/9.x/blade#method-field). Es necesario incluirla para indicar que la ruta utiliza el método DELETE.

### Rutas PUT

Las rutas PUT las utilizaremos para realizar modificaciones en nuestro modelo. A continuación incluimos un ejemplo de una ruta de este tipo.

```
Route::put('/admin/products/{id}/update', 'App\Http\Controllers\Admin\AdminProductController@update')->name("admin.product.update");
```

En este caso el método "update" será el encargado de realizar la modificación correspondiente en el modelo.

Al igual que en el caso anterior, el formulario debe incluir la directiva [`@method`](https://laravel.com/docs/9.x/blade#method-field) para indicar que se va a utilizar el método PUT.

```
<form action="\{\{ route('admin.product.update', ['id'=> $viewData['product']->getId()]) \}\}" method="POST">
    @method('PUT')
    ...
</form>
```

###
