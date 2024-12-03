# Validación de formularios

## Cómo validar los campos de un formulario en el controlador antes de procesarlos

Cuando utilizamos el método `$request->validate()` en un controlador para validar los datos de una solicitud, Laravel verifica los datos según las reglas proporcionadas.

Copiar

```
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

### **Verificar si hay errores**:

Copiar

```
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

### **Mostrar mensajes de error por campo**:

Si deseas mostrar mensajes de error específicos junto a cada campo del formulario:

Copiar

```
<label for="email">Correo:</label><br>
<input type="email" id="email" name="email" value="{{ old('email') }}"><br>
@if ($errors->has('email'))
    <span style="color: red;">{{ $errors->first('email') }}</span><br>
@endif
```

* **$errors->has('email')**: Comprueba si hay errores para el campo 'email'.
*   **$errors->first('email')**: Obtiene el primer mensaje de error para 'email'. Un solo campo puede tener varios mensajes de error asociados si no cumple con múltiples reglas de validación. Cuando defines reglas de validación para un campo, puedes especificar varias reglas que el campo debe cumplir. Si deseas mostrar **todos los mensajes de error** para un campo, puedes usar `$errors->get('campo')`, que devuelve un array con todos los mensajes.

    **Ejemplo**:

    Copiar

    ```
    @if ($errors->has('email'))
        <ul>
            @foreach ($errors->get('email') as $error)
                <li>{{ $error }}</li>
            @endforeach
        </ul>
    @endif
    ```
* **$errors->old('email'):** Para que los usuarios no tengan que volver a ingresar todos los datos en caso de error, puedes utilizar la función `old()` en los campos del formulario

Puedes consultar las reglas de validación que puedes utilizar [en la web oficial de Laravel.](https://laravel.com/docs/11.x/validation#rule-regex)

## Personalización de mensajes de error en Laravel

Cuando utilizamos el método `$request->validate()` para validar formularios, Laravel genera mensajes de error predeterminados para las reglas de validación. Sin embargo, podemos personalizar estos mensajes para adaptarlos mejor a nuestro proyecto. A continuación, explicaremos cómo hacerlo.

### **Definir mensajes personalizados en el método de validación**

Podemos pasar un tercer argumento al método `$request->validate()`, que será un array con los mensajes de error personalizados. Este array debe usar el formato `campo.regla` como clave y el mensaje personalizado como valor.

Ejemplo:

```php
public function submitForm(Request $request)
{
    $validatedData = $request->validate(
        [
            'email' => 'required|email',
            'module' => 'required',
        ],
        [
            'email.required' => 'El campo correo electrónico es obligatorio.',
            'email.email' => 'El formato del correo electrónico no es válido.',
            'module.required' => 'Debe seleccionar un módulo.',
        ]
    );

    // Continuar con el procesamiento de datos...
}
```

En este ejemplo:

* `email.required`: Personaliza el mensaje de error para la regla `required` del campo `email`.
* `email.email`: Personaliza el mensaje de error para la regla `email` del campo `email`.
* `module.required`: Personaliza el mensaje de error para la regla `required` del campo `module`.

***

### **Usar el archivo de configuración de validaciones**

Para proyectos grandes o mensajes reutilizables, podemos gestionar los mensajes personalizados en un archivo de idioma dedicado. Laravel incluye un archivo `validation.php` en el directorio `resources/lang/es` (o cualquier idioma configurado).

Pasos:

1. Navegamos a `resources/lang/es/validation.php`.
2. En este archivo, podemos añadir mensajes personalizados en la sección `custom`.

Ejemplo de configuración:

```php
'custom' => [
    'email' => [
        'required' => 'El campo correo electrónico es obligatorio.',
        'email' => 'Introduce un correo electrónico válido.',
    ],
    'module' => [
        'required' => 'Es necesario seleccionar un módulo.',
    ],
],
```

En las reglas de validación del controlador, Laravel utilizará automáticamente estos mensajes.

***

### **Mensajes genéricos personalizados para reglas específicas**

Si deseamos personalizar mensajes genéricos para una regla, independientemente del campo, podemos definirlos en la sección `attributes` de `validation.php`.

Ejemplo:

```php
'attributes' => [
    'required' => 'El campo :attribute es obligatorio.',
],
```

Aquí, `:attribute` será reemplazado dinámicamente por el nombre del campo. Para traducir los nombres de los campos, podemos añadirlos en el mismo archivo:

```php
'attributes' => [
    'email' => 'correo electrónico',
    'module' => 'módulo',
],
```

***

### **Mostrar los mensajes personalizados en la vista**

Los mensajes personalizados estarán disponibles en la variable `$errors` de las vistas, como en el caso de los mensajes predeterminados.

Ejemplo en Blade:

```blade
@if ($errors->has('email'))
    <span style="color: red;">{{ $errors->first('email') }}</span>
@endif
```

