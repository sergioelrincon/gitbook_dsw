# Controladores

Podemos crear un controlador con:

```
php artisan make:controller <nombredelcontrolador>
```

Esto creará un controlador en la carpeta "/Http/Controllers". Dicho controlador consistirá en una clase con una serie de métodos que tendremos que definir nosotros. Dichos métodos se invocarán desde el router. En dichos métodos se cargarán las vistas y se invocarán a los modelos correspondientes. A continuación se muestra un ejemplo de un route:

```
Route::get('/crear-cuenta', [RegisterController::class, 'index']);
```

y de su asociado:

```
class RegisterController extends Controller
{
    public function index() {
        return view('auth.register');
    }
}
```

Los controladores nos ayudan a tener el código mejor organizado y separar la funcionalidad de las aplicaciones.

### Denominación de los métodos de los controladores que manejan los diferentes tipos de rutas

Laravel adopta una convención de nomenclatura para los métodos de los controladores que manejan las diferentes rutas, especialmente cuando se utiliza el enrutamiento de recursos. Esta convención es parte de lo que hace a Laravel tan atractivo, ya que proporciona una estructura clara y consistente para el desarrollo de aplicaciones.

A continuación se incluye una lista de las acciones CRUD, los métodos HTTP correspondientes, y los nombres de métodos convencionales en los controladores:

* **index**: Muestra una lista de todos los recursos. Utilizado con rutas GET.
* **create**: Muestra un formulario para crear un nuevo recurso. Utilizado con rutas GET.
* **store**: Guarda un nuevo recurso en la base de datos. Utilizado con rutas POST.
* **show**: Muestra un recurso específico. Utilizado con rutas GET.
* **edit**: Muestra un formulario para editar un recurso existente. Utilizado con rutas GET.
* **update**: Actualiza un recurso en la base de datos. Utilizado con rutas PUT/PATCH.
* **destroy**: Elimina un recurso específico de la base de datos. Utilizado con rutas DELETE.

Para obtener información detallada sobre las convenciones de nomenclatura de los métodos en los controladores de recursos de Laravel, podemos consultar [la siguiente página](https://laravel.com/docs/10.x/controllers#actions-handled-by-resource-controllers) de la documentación oficial de Laravel.

Si creamos el controlador con el siguiente comando, Laravel creará todos estos métodos en el controlador:

`php artisan make:controller NombreDelControlador --resource`
