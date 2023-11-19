# Manejo de sesiones y cookies

## Recursos

* [Password hash online generator](https://phppasswordhash.com)
* [EditThisCookie](https://chrome.google.com/webstore/detail/editthiscookie/fngmhnnpilhplaeedifhccceomclgfbg?hl=es)

## Sesiones

* Autenticación
  * [password\_hash()](https://www.php.net/manual/es/function.password-hash): Genera un hash del texto pasado por parámetro.
  * [password\_verify()](https://www.php.net/manual/es/function.password-verify.php): Comprueba si una contraseña coincide con un hash.
* [session\_start()](https://www.php.net/manual/es/function.session-start): Inicia o reanuda una sesión.
* [$\_SESSION\[\]](https://www.php.net/manual/es/reserved.variables.session):  Variable superglobal en la que se almacenan las variables de sesión.
* [session\_unset()](https://www.php.net/manual/es/function.session-unset.php): Elimina todas las variables de sesión.
* [session\_destroy()](https://www.php.net/manual/es/function.session-destroy.php): Elimina una sesión.

## Cookies

* [setcookie()](https://www.php.net/manual/es/function.setcookie.php): Define o edita una cookie
  * name
  * value
  * expires
  * path
* [$\_COOKIE](https://www.php.net/manual/es/reserved.variables.cookies): Array superglobal donde se almacenan las cookies
