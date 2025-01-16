# Paginación y filtrado

### ¿Qué es la paginación en Laravel?

La paginación consiste en mostrar los datos en bloques (páginas), de manera que no carguemos todos los registros de golpe. Laravel proporciona métodos muy sencillos (`paginate()`) para manejar la paginación sin tener que escribir manualmente la lógica de cuántos registros se deben mostrar, en qué página estamos, etc.

#### ¿Por qué usar paginación?

* **Rendimiento**: evita procesar y mostrar una cantidad enorme de datos de una sola vez.
* **Mejor experiencia de usuario**: facilita la navegación por el listado de registros.

***

### ¿Qué es la búsqueda o filtrado?

Cuando hablamos de filtrado o búsqueda en este contexto, nos referimos a la posibilidad de enviar parámetros de búsqueda (por ejemplo, por _nombre_ o por _email_) al controlador para que devuelva sólo los resultados que coincidan con esos criterios.

***

### ¿Qué son los _scopes_ en un modelo de Laravel?

Los _scopes_ (o _local scopes_) son métodos que definimos en el modelo para encapsular y reutilizar partes de la consulta (_query_) de Eloquent. Tienen una nomenclatura especial:

* Empiezan con la palabra **scope** y luego el nombre que queramos (ej: `scopeFilterByName`).
* Se usan en la consulta de Eloquent sin la palabra “scope”: `User::filterByName($name)`.

Por ejemplo, si tenemos este _scope_ en el modelo `User`:

```php
public function scopeFilterByName(Builder $query, $name)
{
    return $query->where('name', 'like', "%{$name}%");
}
```

Entonces podemos hacer:

```php
$users = User::filterByName('Carlos')->get();
```

en lugar de escribir manualmente la condición:

```php
$users = User::where('name', 'like', '%Carlos%')->get();
```

De esta manera, nuestros controladores se vuelven más limpios, y la lógica de filtrado se mantiene cerca del modelo.

***

### Implementación paso a paso

Para que tu proyecto use las plantillas de paginación y puedas personalizarlas, necesitas “publicar” los archivos de paginación que vienen en el _core_ de Laravel. Esto se hace con el comando:

```bash
php artisan vendor:publish --tag=laravel-pagination
```

Este comando hace lo siguiente:

* Copia las **plantillas de paginación** por defecto de Laravel hacia la carpeta `resources/views/vendor/pagination`.
* Te permite **editar** y **personalizar** el diseño de la paginación sin afectar los archivos originales que vienen con Laravel.

Por ejemplo, si ejecutas ese comando, podrás encontrar (o crear) un archivo como `resources/views/vendor/pagination/bootstrap-4.blade.php`, donde Laravel define la apariencia de los enlaces de paginación (botones “Anterior”, “Siguiente”, etc.). Después, cuando llamas a:

```php
{{ $users->links('vendor.pagination.bootstrap-4') }}
```

Laravel usará tu plantilla publicada en lugar de la predeterminada. Así, si quieres cambiar etiquetas HTML, clases de CSS, íconos, o cualquier otro detalle, podrás hacerlo libremente en esa carpeta.

#### El modelo (User.php)

En tu modelo `User`, defines los _scopes_ que te permiten filtrar los resultados por nombre o por email. También puedes definir un _scope_ para ordenar por un campo, etc.

```php
// Scope para ordenar por un campo en un sentido determinado
public function scopeOrderByField(Builder $query, $field, $direction = 'asc')
{
    return $query->orderBy($field, $direction);
}

// Scope para filtrar por nombre
public function scopeFilterByName(Builder $query, $name)
{
    return $query->where('name', 'like', "%{$name}%");
    
    return $query;
}

// Scope para filtrar por email
public function scopeFilterByEmail(Builder $query, $email)
{
    return $query->where('email', 'like', "%{$email}%");
    
    return $query;
}
```

***

#### El controlador

Supongamos que en tu controlador `UserController` tienes un método `index()` que listará a los usuarios. Para manejar la paginación y la búsqueda, podemos hacer algo así:

```php
public function index(Request $request)
{
    // 1. Controlar cuántos registros mostramos por página.
    //    Aquí asumimos que $allowedPerPage es un array como [2, 25, 50, 100].
    //    Si el valor que viene por el request no está en ese array, por defecto usamos 2.
    $perPage = in_array($request->input('per_page'), $this->allowedPerPage) 
        ? $request->input('per_page') 
        : 2;

    // 2. Construir la consulta con scopes (filtros).
    //    - filterByName: filtra por nombre (usando el parámetro 'search')
    //    - filterByEmail: filtra por email (usando el parámetro 'email', si existiera)
    //    - paginate: crea la paginación.
    $users = User::query()
        ->filterByName($request->get('search'))
        ->filterByEmail($request->get('email'))
        ->paginate($perPage);

    // 3. Retornar la vista, pasando la variable $users a la misma.
    return view('admin.users.index', compact('users'));
}
```

**Puntos clave:**

* `paginate($perPage)`: es el método de Laravel que se encarga de dividir los resultados en “páginas”.
* `$request->get('search')`: nos trae el valor que el usuario haya puesto en el campo de búsqueda del formulario (en la vista).

***

#### La vista (admin/users/index.blade.php)

En la vista, necesitamos un formulario para enviar los filtros de búsqueda y la cantidad de resultados por página. Observa que usamos método `GET` en el formulario para que los parámetros aparezcan en la URL y faciliten la paginación.

```html
<!-- Formulario de búsqueda y filtros -->
<form method="GET" action="{{ route('users.index') }}" class="mb-4 d-flex flex-wrap">
    <!-- Selector de cantidad de registros por página -->
    <select name="per_page" class="form-control mb-2 mr-2">
        <option value="2" {{ request('per_page') == 2 ? 'selected' : '' }}>Mostrar 2 registros</option>
        <option value="25" {{ request('per_page') == 25 ? 'selected' : '' }}>Mostrar 25 registros</option>
        <option value="50" {{ request('per_page') == 50 ? 'selected' : '' }}>Mostrar 50 registros</option>
        <option value="100" {{ request('per_page') == 100 ? 'selected' : '' }}>Mostrar 100 registros</option>
    </select> 

    <!-- Campo para buscar por nombre (y en este ejemplo también email) -->
    <input type="text" name="search" value="{{ request('search') }}" 
           placeholder="Buscar por nombre o email" class="form-control mb-2 mr-2">

    <!-- Botón para aplicar la búsqueda -->
    <button type="submit" class="btn btn-primary mb-2 mr-2">Buscar</button>

    <!-- Botón para limpiar la búsqueda y volver al listado completo -->
    <a href="{{ route('users.index') }}" class="btn btn-secondary mb-2">Limpiar</a>
</form>
```

> Observa que usamos `request('per_page')` o `request('search')` para mantener en los campos el valor que el usuario seleccionó o buscó, facilitando la experiencia de usuario.

**Mostrando la tabla con resultados**

```html
<!-- Tabla de usuarios -->
<table class="table table-bordered table-striped">
    <thead>
        <tr>
            <th>Nombre</th>
            <th>Email</th>
            <th>Acciones</th>
        </tr>
    </thead>
    <tbody>
        @foreach ($users as $user)
            <tr>
                <td>{{ $user->name }}</td>
                <td>{{ $user->email }}</td>
                <td>
                    <!-- Botones (ver, editar, eliminar) -->
                    <a href="{{ route('users.show', $user->id) }}" class="btn btn-sm btn-info" title="Ver">
                        <i class="fas fa-eye"></i>
                    </a>
                    <a href="{{ route('users.edit', $user->id) }}" class="btn btn-sm btn-warning" title="Editar">
                        <i class="fas fa-edit"></i>
                    </a>
                    <form action="{{ route('users.destroy', $user->id) }}" method="POST" style="display:inline;">
                        @csrf
                        @method('DELETE')
                        <button type="submit" class="btn btn-sm btn-danger delete-user" 
                                title="Eliminar" data-id="{{ $user->id }}">
                            <i class="fas fa-trash"></i>
                        </button>
                    </form>
                </td>
            </tr>
        @endforeach
    </tbody>
</table>
```

**Control de paginación y resumen de resultados**

```html
<!-- Paginación -->
<div class="mt-4">
    {{ $users->links("vendor.pagination.bootstrap-4") }}
</div>

<!-- Resumen de cuántos resultados se están mostrando -->
<div class="mt-4">
    {{ __('Showing') }} {{ $users->firstItem() }} 
    {{ __('to') }} {{ $users->lastItem() }} 
    {{ __('of') }} {{ $users->total() }} 
    {{ __('results') }}
</div>
```

El método `links()` genera los enlaces de paginación automáticamente (los típicos botones “Anterior”, “Siguiente”, etc.). Laravel detecta que la paginación se ha hecho con `paginate()` y genera esos enlaces basándose en la URL actual y los parámetros pasados por GET (por ejemplo, `search` y `per_page`).

El bloque de código de resumen de resultados sirve para mostrar un pequeño resumen de la paginación de los datos en pantalla. **Laravel**, al usar `paginate()`, devuelve un objeto de tipo `LengthAwarePaginator` que, además de la colección de datos (los usuarios), nos proporciona métodos útiles para indicar cuántos registros se muestran en cada página, cuál es el total, etc.

* **`$users->firstItem()`**: Indica el número del primer elemento que aparece en la página actual (por ejemplo, `1` en la primera página, `16` en la segunda si tuviéramos 15 por página, etc.).
* **`$users->lastItem()`**: Indica el número del último elemento de la página actual (por ejemplo, `15` en la primera página, `30` en la segunda, si tuviéramos 15 por página, etc.).
* **`$users->total()`**: Indica el número total de registros en la base de datos para la consulta que hemos paginado (por ejemplo, `50` si ese es el total de usuarios).

> **Ejemplo de uso**\
> Si estás en la primera página con 15 registros por página y hay 50 resultados totales, el resumen diría:\
> “Showing 1 to 15 of 50 results”.
>
> Si avanzas a la segunda página, indicará:\
> “Showing 16 to 30 of 50 results”, etc.

Además, notarás que el texto está envuelto en la función `__()`, que es la forma de _internacionalizar_ (i18n) los textos en Laravel. Esta función busca la traducción correspondiente en los archivos de idioma. De esta manera, puedes traducir la palabra “Showing”, “to”, “of”, etc., para diferentes idiomas si así lo deseas.

### Resumen

* **Paginación** con `paginate($perPage)` y visualización en la vista con `{{ $users->links() }}`.
* **Búsqueda** o **filtrado** a través de parámetros en el formulario (ejemplo: `name="search"`), que capturas en el controlador con `$request->get('search')`.
* **Scopes** en el modelo (`scopeFilterByName`, `scopeFilterByEmail`) para encapsular la lógica de filtrado y que el controlador quede limpio.

