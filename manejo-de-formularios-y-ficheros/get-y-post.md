# GET y POST

## Introducción a los métodos POST y GET en aplicaciones web

Cuando desarrollamos aplicaciones web, una de las tareas más comunes es interactuar con los usuarios a través de formularios. Imagina que en una página web, el usuario introduce su nombre, dirección de correo, o cualquier tipo de dato. Estos datos deben enviarse al servidor para ser procesados y almacenados. Aquí es donde entran en juego dos métodos importantes: **GET** y **POST**.

### **1. ¿Qué son los métodos GET y POST?**

Son dos maneras de enviar datos desde el navegador del usuario (el cliente) al servidor, utilizando el protocolo HTTP (el lenguaje en el que el navegador y el servidor se comunican). Piensa en ellos como dos formas diferentes de enviar una carta a una dirección:

* **GET**: Es como escribir la carta directamente en la dirección del sobre, visible para todos. Los datos viajan en la URL (dirección web) y son visibles.
* **POST**: Es como escribir la carta dentro de un sobre cerrado. Los datos viajan en el cuerpo del mensaje y no se ven en la URL.

### **2. Método GET**

* **Cómo funciona**: Cuando se utiliza GET, los datos que envía el formulario viajan en la propia URL. Ejemplo de URL con GET:\
  `https://ejemplo.com/buscar?nombre=Sergio&edad=30`
* **Cuándo usarlo**: Se utiliza generalmente cuando los datos no son sensibles y no son muy grandes, como cuando haces una búsqueda en Google.
* **Características**:
  * Los datos se ven en la barra de direcciones.
  * Es fácil compartir una URL con otra persona.
  * Está limitado en la cantidad de datos que puede enviar.

### **3. Método POST**

* **Cómo funciona**: A diferencia de GET, con POST los datos no viajan en la URL, sino en el cuerpo del mensaje que se envía al servidor. Ejemplo:
  * No verías los datos en la URL.\
    `https://ejemplo.com/enviar-datos`
* **Cuándo usarlo**: Se utiliza cuando los datos son más grandes o sensibles, como cuando introduces tu contraseña o realizas un registro en una página.
* **Características**:
  * Los datos no son visibles en la URL.
  * No tiene límite en la cantidad de datos que puedes enviar.
  * Es más seguro para información confidencial, aunque no totalmente.

### **4. Diferencias clave**

| Característica  | GET                                   | POST                                              |
| --------------- | ------------------------------------- | ------------------------------------------------- |
| **Visibilidad** | Datos visibles en la URL              | Datos ocultos en el cuerpo de la solicitud        |
| **Seguridad**   | Menos seguro (los datos son visibles) | Más seguro (datos no visibles en la URL)          |
| **Tamaño**      | Limitado (la URL tiene un límite)     | Sin límite importante                             |
| **Uso típico**  | Consultas, búsqueda de información    | Formularios de registro, envío de datos sensibles |

### **5. Ejemplo práctico**

Imagina un formulario en una página de inicio de sesión:

* Con **GET**, podrías ver algo así en la URL:\
  `https://ejemplo.com/login?usuario=Sergio&password=1234`\
  (¡No sería seguro porque la contraseña es visible en la URL!)
* Con **POST**, la URL sería simplemente:\
  `https://ejemplo.com/login`, pero los datos (usuario y contraseña) viajarían ocultos.
