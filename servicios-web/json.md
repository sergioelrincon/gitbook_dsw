# JSON

## Formato JSON

JSON (JavaScript Object Notation) es un formato ligero de intercambio de datos, fácil de leer y escribir para humanos, y simple de analizar y generar para las máquinas. Deriva de la notación de objeto en JavaScript, pero es independiente del lenguaje, lo que significa que muchos lenguajes de programación modernos soportan JSON con poca o ninguna modificación necesaria. Esto ha contribuido a su popularidad como el formato de datos de elección para las API RESTful.

### Estructura de JSON

JSON está construido sobre dos estructuras:

1. **Una colección de pares de nombre/valor:** En varios lenguajes, esto se realiza mediante un objeto, registro, estructura, diccionario, tabla hash, lista con clave o un arreglo asociativo.
2. **Una lista ordenada de valores:** En la mayoría de los lenguajes, esto se realiza mediante un array, vector, lista o secuencia.

Los datos en JSON se presentan en pares de nombre/valor, donde el nombre (clave) es un string y el valor puede ser un string, número, objeto JSON, array, booleano (true/false) o null. Los objetos y array en JSON pueden anidarse, permitiendo estructuras de datos complejas.

A continuación se muestra un ejemplo básico de JSON:

```json
{
  "nombre": "Juan",
  "edad": 30,
  "esEstudiante": false,
  "hobbies": ["fútbol", "pintura"],
  "direccion": {
    "calle": "Avda. Pintor Felo Monzón",
    "numero": 123,
    "ciudad": "Las Palmas de Gran Canaria"
  }
}
```

En el contexto de las API RESTful, JSON se utiliza como el medio para serializar y transmitir datos estructurados a través de la red. La simplicidad y facilidad de uso de JSON han llevado a su adopción generalizada en la implementación de API RESTful para:

* **Enviar solicitudes al servidor:** Los clientes pueden enviar datos al servidor en formato JSON, especialmente útil para crear o actualizar recursos.
* **Recibir respuestas del servidor:** Las API RESTful envían respuestas al cliente en formato JSON, lo que permite una fácil manipulación y presentación de los datos en el lado del cliente.

### Ventajas de JSON

* **Ligereza:** JSON es menos verboso que otros formatos de intercambio de datos, como XML, lo que resulta en un menor uso de ancho de banda.
* **Facilidad de uso:** JSON es fácilmente legible por humanos y puede ser interpretado por la mayoría de los lenguajes de programación sin necesidad de bibliotecas externas.
* **Rendimiento:** La simplicidad de JSON permite un análisis y generación rápidos, lo que es crucial para el rendimiento de las aplicaciones web y móviles.

La combinación de estas características hace de JSON una elección popular para el desarrollo de API RESTful, facilitando la interacción eficiente entre clientes y servidores en el ecosistema de aplicaciones modernas.

### JSON en PHP

Manejar datos JSON en PHP es bastante sencillo gracias a las funciones integradas que ofrece PHP para codificar y decodificar datos JSON. Estas funciones te permiten convertir entre representaciones JSON y estructuras de datos de PHP, como arrays y objetos.

#### Decodificar JSON

Para convertir una cadena JSON en una estructura de datos de PHP, puedes usar la función `json_decode()`. Esta función toma una cadena JSON y la convierte en un objeto PHP por defecto, aunque puedes optar por convertirla en un array asociativo pasando `true` como segundo argumento.

```php

$json = '{"nombre": "Juan", "edad": 30}';
$objeto = json_decode($json);
// Acceder a las propiedades como objeto
echo $objeto->nombre; // Salida: Juan

// Convertir en un array asociativo
$array = json_decode($json, true);
// Acceder a los valores como array
echo $array['nombre']; // Salida: Juan

```

#### Codificar JSON

Para convertir una estructura de datos de PHP (como un array o un objeto) en una cadena JSON, podemos usar la función `json_encode()`. Esta función toma un array o objeto de PHP y lo convierte en una cadena JSON.

```php

$array = ['nombre' => 'Juan', 'edad' => 30];
$json = json_encode($array);
echo $json; // Salida: {"nombre":"Juan","edad":30}

```
