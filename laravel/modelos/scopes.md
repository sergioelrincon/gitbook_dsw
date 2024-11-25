# Scopes

Los **scopes** en Laravel son una forma de definir consultas reutilizables para los modelos. Nos permiten encapsular una lógica de consulta específica dentro del modelo para facilitar la reutilización y mantener el código limpio y ordenado. Los scopes son especialmente útiles para situaciones en las que necesitamos aplicar ciertas condiciones a nuestras consultas de manera frecuente.

## Cómo crear un scope

Un scope se define como un método en el modelo y su nombre debe empezar con el prefijo `scope`. De este modo, Laravel sabe que el método es un scope. Sin embargo, cuando se llama al scope, no es necesario utilizar el prefijo `scope`.

Vamos a ver cómo crear un scope en el modelo `User` para buscar usuarios por nombre.

### Ejemplo: Scope para buscar usuarios por nombre

1. Abre el archivo del modelo `User.php`, ubicado en la carpeta `app/Models`.
2. Agrega el siguiente método:

```php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class User extends Model
{
    // Definimos el scope para buscar usuarios por nombre
    public function scopeWhereName($query, $name)
    {
        return $query->where('name', 'like', '%' . $name . '%');
    }
}
```



* **Nombre del método**: `scopeWhereName`
  * Laravel sabe que este método es un scope porque empieza con `scope`.
  * Cuando se llame desde una consulta, solo se utilizará la parte `WhereName`.
* **Argumentos**:
  * `$query`: es el objeto de la consulta actual y se pasa automáticamente.
  * `$name`: es el parámetro que usaremos para buscar usuarios por nombre.
* **Cuerpo del método**:
  * Utiliza el método `where` para buscar los usuarios cuyo campo `name` contenga el valor de `$name`. Utilizamos el operador `like` con `%` para hacer una búsqueda parcial.

## Cómo usar el scope

Una vez definido el scope, podemos utilizarlo en nuestras consultas de forma sencilla:

```php
use App\Models\User;

// Buscar usuarios cuyo nombre contenga la palabra "Sergio"
$users = User::whereName('Sergio')->get();
```

Esto generará una consulta para buscar todos los usuarios cuyo campo `name` contenga la palabra `"Sergio"`.

## Ventajas de los scopes

* **Reutilización**: Puedes reutilizar este scope en cualquier parte de tu aplicación donde necesites buscar usuarios por nombre.
* **Legibilidad**: Hace que el código sea más legible y expresivo, especialmente cuando tienes consultas complejas.

En este ejemplo, el scope `whereName` nos permite escribir consultas más limpias y reutilizables para buscar usuarios por nombre en cualquier parte del proyecto.

## Uso de varios scopes en la misma consulta

Puedes usar varios scopes en la misma consulta en Laravel. Esto te permite encadenar diferentes condiciones de manera limpia y reutilizable, haciendo las consultas más expresivas y fáciles de mantener.

Cada scope se aplica en orden al resultado de la consulta, lo cual es especialmente útil para filtrar datos con distintas condiciones. Veamos un ejemplo para ilustrar cómo hacerlo.

### Ejemplo usando varios scopes en el modelo `User`

Supongamos que además del scope `whereName`, quieres definir otro scope para buscar usuarios activos, llamado `active`. Primero, definimos este nuevo scope en el modelo `User`.

```php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class User extends Model
{
    // Scope para buscar usuarios por nombre
    public function scopeWhereName($query, $name)
    {
        return $query->where('name', 'like', '%' . $name . '%');
    }

    // Scope para buscar usuarios que estén activos
    public function scopeActive($query)
    {
        return $query->where('status', '=', 'active');
    }
}
```

En este ejemplo, hemos añadido un segundo scope llamado `active`, que filtra a los usuarios cuyo estado (`status`) sea `'active'`.

### Usando ambos scopes en la misma consulta

Ahora podemos encadenar ambos scopes para obtener usuarios activos cuyo nombre contenga un valor específico:

```php
use App\Models\User;

// Buscar usuarios activos cuyo nombre contenga "Sergio"
$users = User::whereName('Sergio')->active()->get();
```

* Primero, usamos el scope `whereName('Sergio')` para aplicar un filtro que busque usuarios cuyo campo `name` contenga la palabra `"Sergio"`.
* Luego, encadenamos el scope `active()` para filtrar únicamente los usuarios que están activos (`status` igual a `'active'`).
* El resultado es una consulta que combina ambas condiciones.
