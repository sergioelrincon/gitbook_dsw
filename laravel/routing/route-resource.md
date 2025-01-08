# Route::resource

En Laravel, las rutas que definen métodos y controladores vinculados no se crean de manera explícita cuando se usa `Route::resource`. Esto se debe a que `Route::resource` es una forma abreviada de registrar todas las rutas estándar para las operaciones CRUD (Create, Read, Update, Delete) de un controlador. Este método sigue un patrón predefinido que asocia las rutas con métodos específicos del controlador.

Al usar `Route::resource`, Laravel automáticamente asocia las rutas con los métodos convencionales del controlador correspondiente. A continuación, se muestra un ejemplo de las rutas que se generan y los métodos que se esperan en un posible controlador:

#### Rutas generadas por `Route::resource`

Para `Route::resource('users', UserController::class);`(definido así en el fichero web.php), se generan automáticamente las siguientes rutas:

| Método HTTP | URL                | Nombre de la ruta | Método del controlador |
| ----------- | ------------------ | ----------------- | ---------------------- |
| GET         | /users             | users.index       | `index()`              |
| GET         | /users/create      | users.create      | `create()`             |
| POST        | /users             | users.store       | `store()`              |
| GET         | /users/{user}      | users.show        | `show($id)`            |
| GET         | /users/{user}/edit | users.edit        | `edit($id)`            |
| PUT/PATCH   | /users/{user}      | users.update      | `update($id)`          |
| DELETE      | /users/{user}      | users.destroy     | `destroy($id)`         |

#### ¿Por qué no se ven explícitas?

Laravel asume que tu controlador implementará los métodos correspondientes (`index`, `create`, `store`, `show`, `edit`, `update`, y `destroy`). Si el controlador no tiene alguno de estos métodos, Laravel generará un error solo cuando intentes acceder a la ruta asociada a dicho método.

#### ¿Qué hacer si necesitas métodos o rutas personalizados?

Si necesitas definir rutas o métodos adicionales que no están en este esquema, debes hacerlo de forma explícita, como en el ejemplo comentado:

```php
Route::delete('instructions/{instruction}/delete-audio', [InstructionController::class, 'deleteAudio'])->name('instructions.delete-audio');
```

Esto indica que estás utilizando una ruta personalizada para un método adicional (`deleteAudio`) en el `InstructionController`.

####
