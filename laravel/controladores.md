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

### Pasar datos a las vistas

En Laravel, cuando renderizamos una vista con `view('nombre_de_la_vista', $datos)`, podemos pasar un segundo parámetro que es un array de datos que queremos que la vista utilice.

Si no pasamos los datos necesarios, la vista no sabrá nada sobre las variables definidas en el controlador y, por lo tanto, no podrá utilizarlas.

Hay que recordar que en el patrón MVC (Modelo-Vista-Controlador), el controlador prepara los datos que la vista necesita para presentarlos al usuario.

#### **Ventajas de Usar `compact()`**

* **Código más limpio y conciso**:
  * Si tienes varias variables que quieres pasar a la vista, `compact()` te permite hacerlo de forma sencilla sin tener que escribir un array asociativo manualmente.
  *   Por ejemplo:

      ```php
      $name = 'Juan';
      $age = 25;
      $city = 'Madrid';

      return view('profile', compact('name', 'age', 'city'));
      ```
* **Evita errores tipográficos**:
  * Al usar `compact()`, nos aseguramos de que las claves del array asociativo coinciden exactamente con los nombres de las variables, reduciendo el riesgo de errores por nombres mal escritos.

#### **Alternativas a `compact()`**

*   **Pasar un array asociativo manualmente**:

    ```php
    return view('doubt_form', ['modules' => $modules]);
    ```
*   **Usar el método `with()` de la vista**:

    ```php
    return view('doubt_form')->with('modules', $modules);
    ```

    * Aunque es válido, puede ser menos práctico si necesitas pasar múltiples variables.

### Respuesta a una solicitud POST en el controlador

Cuando un usuario envía un formulario (solicitud POST), el navegador espera una respuesta del servidor. En este caso, lo ideal es redirigir a otra ruta usando redirect().&#x20;

```php
phpCopiar códigoreturn redirect()->route('doubt.form')->with('success', 'Su duda ha sido enviada correctamente.');
```

De esta forma:

* El servidor responde con una redirección a una ruta específica.
* El navegador realiza una nueva solicitud GET a esa ruta.
* Si el usuario refresca la página, solo recarga la página actual (la ruta redirigida), sin reenviar los datos del formulario.
* **Patrón PRG (Post/Redirect/Get)**: Este es un patrón de diseño que ayuda a evitar el reenvío de formularios al separar la solicitud POST del usuario y la página que ve después.

Por otro lado:

* **`with('success', 'Mensaje')`**:
  * Permite pasar datos de la sesión de una solicitud a otra.
  * En la vista, podemos acceder a estos mensajes utilizando `session('success')`.
* **Beneficio**: Podemos informar al usuario sobre el resultado de su acción sin exponer datos sensibles.

### Validación de datos de formularios

Cuando utilizamos el método `$request->validate()` en un controlador para validar los datos de una solicitud, Laravel verifica los datos según las reglas proporcionadas.

```php
   public function submitForm(Request $request)
   {
       $validatedData = $request->validate([
           'email' => 'required|email',
           'module' => 'required',
           // otras reglas...
       ]);

       // Si la validación falla, Laravel redirige automáticamente y pasa los errores
   }
```

Si la validación falla, Laravel automáticamente redirige al usuario de vuelta a la página anterior (normalmente el formulario) y **almacena los errores en la sesión**.

La variable `$errors` se comparte automáticamente con todas las vistas. Esto significa que en cualquier vista renderizada después de una validación fallida, `$errors` estará disponible para mostrar los mensajes de error.

En las plantillas Blade, puedes utilizar la variable `$errors` para mostrar mensajes de error al usuario. Aquí hay algunas formas comunes de hacerlo:

1.  **Verificar si hay errores**:

    ```blade
    @if ($errors->any())
        <div style="color: red;">
            <ul>
                @foreach ($errors->all() as $error)
                    <li>{{ $error }}</li>
                @endforeach
            </ul>
        </div>
    @endif
    ```

    * **$errors->any()**: Verifica si hay algún error.
    * **$errors->all()**: Devuelve todos los mensajes de error en un array.
2.  **Mostrar mensajes de error por campo**:

    Si deseas mostrar mensajes de error específicos junto a cada campo del formulario:

    ```blade
    <label for="email">Correo:</label><br>
    <input type="email" id="email" name="email" value="{{ old('email') }}"><br>
    @if ($errors->has('email'))
        <span style="color: red;">{{ $errors->first('email') }}</span><br>
    @endif
    ```

    * **$errors->has('email')**: Comprueba si hay errores para el campo 'email'.
    *   **$errors->first('email')**: Obtiene el primer mensaje de error para 'email'. Un solo campo puede tener varios mensajes de error asociados si no cumple con múltiples reglas de validación. Cuando defines reglas de validación para un campo, puedes especificar varias reglas que el campo debe cumplir.  Si deseas mostrar **todos los mensajes de error** para un campo, puedes usar `$errors->get('campo')`, que devuelve un array con todos los mensajes.

        **Ejemplo**:

        ```blade
        @if ($errors->has('email'))
            <ul>
                @foreach ($errors->get('email') as $error)
                    <li>{{ $error }}</li>
                @endforeach
            </ul>
        @endif
        ```
    * **$errors->old('email'):** Para que los usuarios no tengan que volver a ingresar todos los datos en caso de error, puedes utilizar la función `old()` en los campos del formulario

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
