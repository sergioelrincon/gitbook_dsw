# Manejo de formularios

## Contenidos

### Variables superglobales utilizadAs para recibir los datos de los formularios

* [$\_GET](https://www.php.net/manual/es/reserved.variables.get)
* [$\_POST](https://www.php.net/manual/en/reserved.variables.post)
* [$\_REQUEST](https://www.php.net/manual/es/reserved.variables.request.php)
* [GET vs POST](https://www.w3schools.com/php/php\_forms.asp)

### Funciones que nos pueden ayudar a validar los campos de un formulario

* [isset()](https://www.php.net/manual/es/function.isset) - Nos permite comprobar si un campo se ha enviado
* [empty()](https://www.php.net/manual/es/function.empty) - Comprueba si una variable está vacía
* [filter\_var() ](https://www.php.net/manual/es/function.filter-var.php)- Filtra una variable a partir de un filtro especificado
  * [Filtros de validación](https://www.php.net/manual/es/filter.filters.validate.php)
* [htmlspecialchars()](https://www.php.net/manual/es/function.htmlspecialchars) - Convierte caracteres especiales a entidades HTML. Es decir, reemplaza "<" y ">". Esto impide que se inyecte código HTML o Javascript en formularios, lo cual permitiría ejecutar código malicioso en el navegador del cliente, o interferir con el código HTML de la página.
* [preg\_match()](https://www.php.net/manual/es/function.preg-match.php) - Compara una cadena determinada con una expresión regular
  * [Patrones de expresiones regulares](https://www.php.net/manual/es/reference.pcre.pattern.syntax.php)
  * [Herramienta para crear y probar expresiones regulares](https://regex101.com)
