# Request

En Laravel, `UserRequest` normalmente se refiere a un tipo de **form request**, una clase utilizada para validar y autorizar datos entrantes a un controlador. En lugar de manejar la validación directamente en el controlador, las clases de request permiten centralizar y organizar la lógica de validación.

Las clases `UserRequest` (o cualquier `*Request`) se generan usando el comando de Artisan:

```bash
php artisan make:request UserRequest
```

Este comando creará una clase en el directorio `app/Http/Requests` con el nombre especificado, en este caso `UserRequest`. Esta clase contiene dos métodos importantes:

1. **`authorize()`**: Determina si el usuario está autorizado a realizar esta petición. Puedes implementar lógica para comprobar permisos o roles, devolviendo `true` si el usuario tiene permisos y `false` en caso contrario.
2. **`rules()`**: Define las reglas de validación para los datos de la petición. Estas reglas aseguran que los datos proporcionados sean correctos antes de ser procesados por el controlador.

Por ejemplo, si deseas validar los datos para crear o actualizar un usuario, podrías definir las reglas de la siguiente forma:

```php
namespace App\Http\Requests;

use Illuminate\Foundation\Http\FormRequest;

class UserRequest extends FormRequest
{
    public function authorize()
    {
        // Aquí podrías implementar la lógica para autorizar la petición
        return true;
    }

    public function rules()
    {
        return [
            'name' => 'required|string|max:255',
            'email' => 'required|email|unique:users,email,' . $this->user,
            'password' => 'required|string|min:8|confirmed',
        ];
    }
}
```

En este ejemplo:

* El campo `name` es obligatorio (`required`), debe ser una cadena (`string`) y tener un máximo de 255 caracteres.
* El campo `email` también es obligatorio, debe tener un formato de correo electrónico (`email`) y ser único en la tabla `users` (`unique:users,email`). Se usa `$this->user` para permitir la actualización de un usuario específico sin conflictos.
* El campo `password` debe ser una cadena (`string`), con un mínimo de 8 caracteres (`min:8`) y debe coincidir con el campo de confirmación (`confirmed`).

Los mensajes personalizados también los puedes incluir en el nuevo request. Para ello debes definir un nuevo método denominado "messages()":

```php

    public function messages(): array
    {
        return [
            'name.required' => 'El nombre es obligatorio',
            'email.required' => 'El correo es obligatorio',
            'email.email' => 'El correo debe ser válido',
        ];
    }

```

Luego, puedes inyectar esta clase `UserRequest` directamente en el método del controlador en lugar de usar la clase general `Request`:

```php
use App\Http\Requests\UserRequest;

class UserController extends Controller
{
    public function store(UserRequest $request)
    {
        // Aquí ya puedes asumir que los datos han sido validados
        $data = $request->validated();
        User::create($data);

        return redirect()->route('users.index')->with('success', 'Usuario creado exitosamente');
    }
}
```

La ventaja de usar `UserRequest` es que ayuda a mantener los controladores limpios, facilita la reutilización de la lógica de validación y asegura que las validaciones se mantengan consistentes y centralizadas.
