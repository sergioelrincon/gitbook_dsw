# API REST

## ¿Qué es una API REST?

Una API REST (Interfaz de Programación de Aplicaciones Representational State Transfer) es un tipo específico de servicio web que sigue los principios del estilo arquitectónico REST. Las API REST utilizan métodos HTTP estándar (como GET, POST, PUT, DELETE) para facilitar la comunicación entre sistemas en la web, haciendo uso de formatos de mensajes ligeros como JSON o XML para el intercambio de datos..

Es importante conocer la relación entre los conceptos API REST y servicio web. Todas las API REST son servicios web, pero no todos los servicios web son API REST. Los servicios web son un concepto general para las funciones de red que se exponen a través de Internet para permitir la interacción entre diferentes sistemas de software. Las API REST son una categorización dentro de este concepto amplio, específicamente aquellas que siguen los principios REST.

API REST nos proporciona interfaz de aplicaciones para transferir datos.

![Diagrama APIRest](img/DiagramaAPIRest.png)

El término **API RESTful** hace referencia a una API REST que, además de lo anterior, nos permite crear nuevos registros, modificar los existentes o eliminarlos.

![Diagrama APIRest](img/DiagramaAPIRestFul.png)

## Características

* Desarrolladas por programadores, para programadores.
* Pueden ser públicas o privadas.
* Pueden ser gratuitas o de pago.
* Algunas API están protegidas por token de seguridad.
* Diferentes lenguajes permiten su implementación: PHP y sus diferentes frameworks, NodeJS, etc.
* Es fundamental elaborar documentación que permita conocer su uso al programador que la vaya a utilizar.

## Tipos de autorizaciones

* **OAUTH**: "Open Authorization". Es un estándar abierto que permite flujos simples de autorización para sitios web o aplicaciones informáticas. Es una simple combinación de caracteres que se comvierte en una contraseña. Implica pasar en el encabezado el campo "Authorization" con el valor correspondiente
* **OAUTH 2**: Es un flujo de autorización específico encapsulado en un token portador (bearer token) y se genera con la combinación de unas credenciales que le suministra la empresa al cliente llamadas CLIENT ID y SECRET KEY. En algunas ocasiones usan el encriptado md5() o base64\_encode() para combinar las credenciales del cliente y generar el Token. Un ejemplo lo tenemos en Udemy.
* **API KEY**: Es un identificador que sirve como el medio de autenticación de un usuario para el uso de los servicios proporcionados de una API REST. Este valor es único y el cliente debe solicitarlo al proveedor de la API. Un ejemplo lo tenemos en ExchangeRateAPI

La autenticación puede ser:

* Por cabecera (Headers): Se da cuando el token de autorización debe ser pasado de forma oculta por cabeceras HTTP.
* Por URL

## Campo STATUS - Respuestas API

Dentro de una respuesta de una API debe existir un campo "STATUS" con un código que indique el resultado de la operación. Podemos encontrar los códigos HTTP estándar en la siguiente URL: https://developer.mozilla.org/es/docs/Web/HTTP/Status

Los más utilizados son:

* 200 - Consulta correcta.
* 201 - Actualización de datos correcta.
* 404 - Recurso no encontrado.
* 500 - Error interno en el servidor.
