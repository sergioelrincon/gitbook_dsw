# Almacenamiento de contraseñas

#### Almacenamiento de contraseñas con `bcrypt` en Laravel

En Laravel, para almacenar de forma segura las contraseñas de los usuarios, utilizamos la función `bcrypt()`. Esta función se encarga de aplicar un proceso de encriptación que hace que las contraseñas no se almacenen en texto plano en la base de datos, sino que se conviertan en un "hash" (un valor irreconocible). Este es un aspecto fundamental para la seguridad de las aplicaciones web, ya que si alguien lograra acceder a la base de datos, no podría obtener las contraseñas originales.

El uso de `bcrypt()` es muy sencillo. En general, podemos aplicarlo directamente al guardar el usuario, como en el siguiente ejemplo:

```php
use App\Models\User;
use Illuminate\Http\Request;

public function register(Request $request)
{
    $validatedData = $request->validate([
        'name' => 'required|string|max:255',
        'email' => 'required|string|email|max:255|unique:users',
        'password' => 'required|string|min:8|confirmed',
    ]);

    $user = User::create([
        'name' => $validatedData['name'],
        'email' => $validatedData['email'],
        'password' => bcrypt($validatedData['password']),
    ]);

    // Aquí podríamos redirigir o realizar alguna acción después del registro
}
```

En este ejemplo, al crear un nuevo usuario con el método `User::create()`, utilizamos `bcrypt($validatedData['password'])` para encriptar la contraseña antes de almacenarla en la base de datos.

