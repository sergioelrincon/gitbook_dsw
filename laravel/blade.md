# Blade

Es el motor de plantillas de Laravel. Las plantillas Blade utilizan la extensión ".blade.php" y se almacenan en "resources/views". En los ficheros blade tendremos una mezcla de código HTML junto con elementos y directivas Blade.

Puedes encontrar la documentación oficial de Blade en el [siguiente enlace](https://laravel.com/docs/10.x/blade).

### Directivas Blade

Las [_directivas Blade_](https://laravel.com/docs/10.x/blade#blade-directives) se podrían considerar una especie de atajos a estructuras de control comunes en PHP, como sentencias condicionales o bucles. Por ejemplo:

```
@if ($records > 0)
    I have records!
@else
    I don't have any records!
@endif
```

en lugar de:

```
<?php if($records > 0) { ?>  
    I have records!  
<?php } else { ?>  
    I don't have any records!  
<?php } ?>
```

Mediante el uso de un motor de plantillas **evitamos utilizar sintaxis PHP o etiquetas PHP en nuestros ficheros de vistas**. En su lugar deberíamos usar **directivas** o **helpers**. La ventaja es que los motores de plantillas limitan el número de funcionalidades disponibles en las vistas y de esta forma se aseguran de que no hacemos _locuras_ en las vistas. Es recomendable que si no encontramos una directiva o helper para una funcionalidad que necesitemos implementar en una vista es, posiblemente, porque dicha funcionalidad no debería estar implementada en la vista. Quizás debería estarlo en un controlador o en otro fichero.

#### Directiva _extends_

Se utiliza en las vistas para cargar otras vistas. Por ejemplo, para cargar una plantilla que contenga el menú principal que se podría incluir en el encabezado de todas nuestras páginas.

```
@extends('layout.app')
```

Esa línea cargaría el contenido de './views/layout/app.blade.php'. Destaca el hecho de que en esta directiva las carpetas se separan de los ficheros utilizando el carácter "." en lugar de "/". Además, parte de la ruta es implícita como se puede apreciar, y el sufijo del fichero se presupone que es ".blade.php".

#### Directiva _yield_

Sirve para declarar una especie de marcador/contenedor en una vista para posteriormente inyectarle contenido desde las vistas padre. Para esto último se utiliza la directiva @section. Requiere dos parámetros. El primero es el identificador del marcador y el segundo (opcional) es un valor por defecto que se inyectará en caso de que la vista no incluya código para dicho marcador.

En la vista hija incluiríamos:

```
<h1>@yield('titulo')</h1>
```

Y en la vista principal incluiríamos:

```
@section('titulo')
    Página principal
@endsection
```

#### Directiva _route_

Devuelve la URL a la que hace referencia el primer parámetro. Previamente debe estar definido el nombre de la ruta.

```
<a href="{{ route('product.show' }}">...</a>
```

Si la ruta tiene un parámetro, la forma correcta de pasárselo es la siguiente:

```
<a href="{{ route('product.show', ['id'=> $product["id"]]) }}">
```

Puedes encontrar más información sobre route en la [documentación oficial](https://laravel.com/docs/10.x/routing#generating-urls-to-named-routes).

#### Directiva CSRF

La directiva `@csrf` en Laravel es una forma corta de incluir un token CSRF (Cross-Site Request Forgery) en los formularios HTML. Este token es una medida de seguridad importante en aplicaciones web para prevenir ataques de tipo CSRF.

En un ataque CSRF, un atacante podría engañar a los usuarios de la aplicación para que realicen acciones no intencionadas en un sitio web. Al incluir un token CSRF en tus formularios, Laravel se asegura de que cada solicitud que modifica datos proviene realmente del usuario de la aplicación y no de un tercero.

Cuando utilizas la directiva @csrf en un formulario, Laravel genera automáticamente un campo oculto con un token único para ese usuario. Cuando el formulario se envía, el token se envía junto con los demás datos del formulario. Luego, Laravel verifica este token en el servidor para asegurarse de que la solicitud es legítima.

Si el token no está presente o no coincide, Laravel rechazará la solicitud, protegiendo así la aplicación contra ataques CSRF. Es una práctica recomendada y muy importante incluir esta directiva en todos tus formularios HTML que realicen cambios en los datos del servidor (como inserciones, actualizaciones o eliminaciones). Se debe incluir dentro del formulario HTML, en la vista correspondiente.

Más información, en la [documentación oficial](https://laravel.com/docs/9.x/blade#csrf-field).

#### Directivas de autenticación

Permiten mostrar código en las vistas en función de si el usuario está o no autenticado.

```
@auth
    // The user is authenticated...
@endauth

@guest
    // The user is not authenticated...
@endguest
```

### Dobles llaves \{{...\}}

Blade ofrece una sintaxis sencilla y potente para combinar código PHP con HTML de forma elegante y limpia. Uno de los elementos clave de Blade son las dobles llaves `{{ ... }}`, que se utilizan para mostrar datos en las vistas.

Las dobles llaves `{{ ... }}` se utilizan para **imprimir el valor de una variable o una expresión** en la vista. Al hacerlo, Blade aplica automáticamente **escape de entidades HTML** para proteger contra ataques XSS (Cross-Site Scripting), asegurando que el contenido mostrado es seguro.

**Sintaxis básica:**

```blade
{{ $variable }}
```

### Helpers

Los _helpers_ son funciones que se pueden usar dentro de los scripts de Laravel. Para invocar a _helpers_ en una vista, hay que incluirlos entre dobles llaves.

Por ejemplo,

```
{{ now() }}
```

[Este helper](https://laravel.com/docs/10.x/helpers#method-now) muestra la fecha y hora actuales.

Otro ejemplo lo tenemos en el helper [_asset_](https://laravel.com/docs/9.x/helpers#method-asset), que genera una URL usando el esquema actual de la petición (HTTP o HTTPS).

Puedes encontrar más información sobre helpers en [https://laravel.com/docs/10.x/helpers](https://laravel.com/docs/10.x/helpers)

### Variables

#### Variable $errors

Laravel proporciona una variable $errors que está disponible en todas las vistas. Esta variable contiene los mensajes de error generados durante la validación de datos en una solicitud HTTP, generalmente al procesar formularios. Esto permite que los desarrolladores muestren mensajes de error específicos a los usuarios, indicando qué campos no cumplieron con las reglas de validación.

Mediante el método $errors->any() se puede consultar si existe algún error, y en caso afirmativo, se pueden recorrer todos los errores mendiante el método $errors->all(), que devuelve un array con los mensajes de cada uno de los errores, [tal y como se explica en la documentación oficial](https://laravel.com/docs/10.x/validation#quick-displaying-the-validation-errors).
