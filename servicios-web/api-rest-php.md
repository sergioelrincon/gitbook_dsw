# API REST PHP

## Ejemplo de API REST con PHP

A continuación se muestra el código que podemos incluir en un PHP de ejemplo para definir la lógica que permite manejar diferentes métodos HTTP y realizar operaciones CRUD mediante una API REST.

```php

<?php
// Supongamos que esta es nuestra "base de datos" de usuarios
$usuarios = [
    ['id' => 1, 'nombre' => 'Juan', 'edad' => 30],
    ['id' => 2, 'nombre' => 'Ana', 'edad' => 25],
    // Agrega más usuarios según sea necesario
];

// Obtener el método HTTP de la solicitud
$metodo = $_SERVER['REQUEST_METHOD'];

header('Content-Type: application/json');

switch ($metodo) {
    case 'GET':
        // Devuelve la lista de usuarios
        echo json_encode($usuarios);
        break;
    
    case 'POST':
        // Simula la creación de un usuario (aquí deberías procesar datos del cuerpo de la solicitud)
        echo json_encode(['mensaje' => 'Usuario creado (simulado)']);
        break;
    
    case 'PUT':
        // Simula la actualización de un usuario (procesar datos y encontrar el usuario por ID)
        echo json_encode(['mensaje' => 'Usuario actualizado (simulado)']);
        break;
    
    case 'DELETE':
        // Simula la eliminación de un usuario (encontrar el usuario por ID y eliminarlo)
        echo json_encode(['mensaje' => 'Usuario eliminado (simulado)']);
        break;
    
    default:
        header("HTTP/1.1 405 Method Not Allowed");
        echo json_encode(['mensaje' => 'Método no permitido']);
        break;
}
?>

```

* **GET:** Retorna todos los usuarios. En un caso real, aquí se consultarían los datos de una base de datos.
* **POST:** Simula la creación de un nuevo usuario. Deberíamos recoger los datos enviados (usualmente en formato JSON) desde el cuerpo de la solicitud y procesarlos adecuadamente.
* **PUT:** Simula la actualización de un usuario existente. Necesitarías identificar el usuario a actualizar a partir de la ID enviada y luego procesar los datos del cuerpo de la solicitud para actualizar el usuario.
* **DELETE:** Simula la eliminación de un usuario. Igual que con PUT, necesitarías identificar cuál usuario eliminar.

A continuación se muestra cómo podríamos recoger los datos enviados en formato JSON para el caso de la petición POST:

```php

...
case 'POST':
    // Recoger datos JSON del cuerpo de la solicitud
    $contenido = file_get_contents('php://input');
    $usuario = json_decode($contenido, true); // Convertir JSON a array asociativo

    if (is_null($usuario)) {
        echo json_encode(['mensaje' => 'El cuerpo de la solicitud no es válido']);
        break;
    }

    // Validamos y almacenamos el usuario en la base de datos
    // Por simplicidad, solo vamos a simular que lo hemos creado y devolver lo que se nos envió
    $usuario['id'] = rand(100, 999); // Simular un ID generado
    echo json_encode(['mensaje' => 'Usuario creado', 'usuario' => $usuario]);
    break;
...

```

* **file\_get\_contents('php://input'):** Esta función de PHP lee la entrada de la solicitud. En el contexto de una solicitud POST que envía datos JSON, esto te permitirá acceder al cuerpo de la solicitud.
* **json\_decode($contenido, true):** Esto convierte la cadena JSON del cuerpo de la solicitud en un array asociativo de PHP. Pasar `true` como segundo argumento hace que `json_decode` devuelva un array asociativo en lugar de un objeto.
* **Validación y almacenamiento:** En un caso de uso real, aquí es donde validaríamos los datos recibidos para asegurarnos de que cumplen con los requisitos de tu aplicación y luego los insertaríamos en una base de datos.&#x20;
* **Simulación de creación:** Se simula la asignación de un ID al usuario "creado" y se devuelve el usuario junto con un mensaje de éxito.

#### Ejemplo de invocación a una API REST&#x20;

Para invocar una API REST y realizar una consulta (por ejemplo, obtener datos utilizando el método `GET`), podemos utilizar varias herramientas y lenguajes de programación. Vamos a ver cómo hacerlo utilizando PHP con `cURL`, que es una biblioteca disponible en PHP para realizar solicitudes a URLs.

Vamos a suponer que deseamos consultar una API para obtener información sobre usuarios. Aquí tenemos un ejemplo de cómo podrías hacer una solicitud `GET` para obtener datos de una API:

```php

<?php

// URL de la API que deseamos consultar
$url = 'http://tuapi.com/api/usuarios';

// Inicializamos cURL
$ch = curl_init($url);

// Configuramos opciones de cURL
// Retorna la respuesta en vez de mostrarla
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

// Ignora la verificación de SSL (no recomendado para producción)
curl_setopt($ch, CURLOPT_SSL_VERIFYHOST, false);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);

// Ejecuta la solicitud cURL
$respuesta = curl_exec($ch);

// Cierra la sesión cURL
curl_close($ch);

// Decodificamos la respuesta JSON
$datos = json_decode($respuesta, true);

// Verifica,ps si se recibieron datos
if ($datos) {
    // Procesa los datos
    print_r($datos);
} else {
    echo "No se pudo obtener datos de la API";
}

?>

```

* **curl\_init:** Esta función inicia una nueva sesión cURL con la URL de la API que deseamos consultar.
* **curl\_setopt:** Esta función establece opciones para la sesión cURL. `CURLOPT_RETURNTRANSFER` se configura como `true` para que `curl_exec()` retorne el resultado de la operación en lugar de mostrarlo directamente. Las opciones `CURLOPT_SSL_VERIFYHOST` y `CURLOPT_SSL_VERIFYPEER` se establecen como `false` para desactivar la verificación de SSL, útil para pruebas locales o cuando trabajas en un entorno que no tiene certificados SSL válidos, pero esto no se debe hacer en aplicaciones de producción debido a riesgos de seguridad.
* **curl\_exec:** Ejecutamos la sesión cURL configurada, haciendo la solicitud a la URL especificada y almacenando la respuesta.
* **curl\_close:** Cerramos la sesión cURL y libera los recursos.
* **json\_decode:** Convertimos la respuesta JSON en una estructura de datos de PHP (en este caso, un array asociativo, debido al segundo parámetro `true`).

## Implementar una API REST en Laravel

Para implementar una APIRest en Laravel, debemos tener en cuenta lo siguiente::

*   Definir las rutas de la API en /routes/api.php. Por ejemplo:

    ```
      Route::get('/player/', 'App\Http\Controllers\PlayerController@index');
    ```

    La ruta anterior será accesible desde 'http://localhost:8000/api/player/'
*   Controlar los errores para devolver la salida correcta en formato JSON. El mensaje de error se incluye en el campo "message". En este caso, el código del error sería el [500](https://developer.mozilla.org/es/docs/Web/HTTP/Status/500):

    ```
      try {
          $players = Player::all();
      } catch (Exception $e) {
          return response()->json([
              'data' => [],
              'message'=>$e->getMessage()
          ], JsonResponse::HTTP_INTERNAL_SERVER_ERROR);
      }
    ```
*   Generar la salida correcta en formato JSON. Los datos se deben pasar en el campo "data". En este caso el código de a respuesta debe ser [200](https://developer.mozilla.org/es/docs/Web/HTTP/Status/200).

    ```
      return response()->json([
          'data' => $players,
          'message' => 'Succeed'
      ], JsonResponse::HTTP_OK);
    ```

Para que funcione el código anterior es necesario incluir las siguientes sentencias "use" en el controlador:

```
use App\Models\Post;
use Exception;
use Illuminate\Http\JsonResponse;
```
