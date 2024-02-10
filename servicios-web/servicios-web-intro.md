# Introducción

## Introducción

Los servicios web son una **forma estandarizada de comunicación entre diferentes sistemas de software a través de la red, utilizando tecnologías web como HTTP**. Permiten que las aplicaciones se comuniquen entre sí y compartan datos y servicios entre ellas, independientemente de los detalles de implementación o las plataformas sobre las que se ejecutan. Los servicios web son fundamentales en el desarrollo de aplicaciones web modernas, ya que **facilitan la integración de sistemas heterogéneos** y contribuyen a la arquitectura de aplicaciones distribuidas.

Hay dos estilos principales de servicios web: SOAP (Simple Object Access Protocol) y REST (Representational State Transfer).

### SOAP

SOAP es un protocolo que define un conjunto de reglas para estructurar los mensajes que pueden ser intercambiados entre las aplicaciones. Los mensajes SOAP se envían generalmente sobre HTTP (aunque no exclusivamente) y **están formateados en XML**. SOAP es conocido por su rigidez y la extensividad de sus estándares, lo que lo hace adecuado para entornos empresariales donde se requiere un alto grado de formalidad en las comunicaciones. Sin embargo, en los últimos años REST ha ganado popularidad por su simplicidad y facilidad de uso en el desarrollo de aplicaciones web y móviles modernas.

### REST

REST, por otro lado, es un estilo arquitectónico que utiliza los métodos HTTP existentes (GET, POST, PUT, DELETE) para interactuar con los recursos representados, generalmente, en formatos como XML o **JSON**. REST es **más flexible y fácil de usar** que SOAP, lo que ha contribuido a su popularidad en el desarrollo de aplicaciones web y móviles.

### Importancia de los servicios web

En la actualidad los servicios web son cruciales en el desarrollo de aplicaciones web. Las razones principales son las siguientes:

* **Interoperabilidad:** Permiten que diferentes aplicaciones, desarrolladas en distintos lenguajes de programación y ejecutándose en diversas plataformas, interactúen entre sí.
* **Reutilización de funcionalidades:** Facilitan la reutilización de servicios existentes, permitiendo a los desarrolladores construir aplicaciones complejas más rápidamente.
* **Escalabilidad:** Al separar la lógica de la aplicación en servicios web, es más fácil escalar las aplicaciones según sea necesario.
* **Mantenibilidad:** Mejoran la mantenibilidad al permitir que los cambios se realicen en un servicio específico sin afectar a otros servicios o aplicaciones que lo consumen.

Laravel ofrece soporte para crear tanto clientes como servidores de servicios web RESTful de forma relativamente sencilla, aprovechando sus características como las rutas, los controladores, las respuestas JSON, etc.

## Ejemplos de API públicas

* [Repositorio GitHub con enlaces API públicas](https://github.com/public-apis/public-apis)
* [Disney API](https://disneyapi.dev)
  * [Documentación de la API](https://disneyapi.dev/docs).
  * URL base: https://api.disneyapi.dev
  * Endpoints:
    * /characters
    * /characters/{id}
    * /character?name=Mickey%20Mouse
* [ExchangeRate-API](https://app.exchangerate-api.com)
  * API Key 2dcd420c181a926a8c923203
  * Ejemplo GET: https://v6.exchangerate-api.com/v6/YOUR-API-KEY/pair/EUR/GBP
  * Ejemplos de uso: https://www.exchangerate-api.com/docs/pair-conversion-requests

## Software recomendado

* [JSONView](https://chrome.google.com/webstore/detail/jsonview/gmegofmjomhknnokphhckolhcffdaihd?hl=es): extensión de Chrome/Brave para visualizar las respuestas JSON de forma tabulada.
* [Postman](https://www.postman.com/): nos permite crear peticiones APIRestFul y visualizar los resultados. Se puede descargar desde [aquí](https://www.postman.com/downloads/).
