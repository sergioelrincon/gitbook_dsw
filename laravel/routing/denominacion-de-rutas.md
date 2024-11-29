# Denominación de rutas

## Convención para definir rutas personalizadas en Laravel

En Laravel, las rutas son un componente esencial para dirigir las solicitudes de los usuarios a las acciones correspondientes en los controladores. Seguir una convención para denominarlas  garantizará que nuestras rutas sean claras, consistentes y alineadas con las mejores prácticas del framework.

A continuación, detallamos las convenciones que utilizaremos:

***

## **Rutas para operaciones CRUD**

Cuando trabajemos con una entidad (como "posts", "users", o "products"), cada acción se asociará con un verbo HTTP, una URI y una acción en el controlador. Las rutas personalizadas deben definirse de la siguiente manera:

| **Verbo HTTP** | **URI**                | **Acción en el controlador** | **Descripción**                              |
| -------------- | ---------------------- | ---------------------------- | -------------------------------------------- |
| `GET`          | `/resources`           | `index`                      | Mostrar un listado de recursos               |
| `GET`          | `/resources/create`    | `create`                     | Mostrar un formulario para crear un recurso  |
| `POST`         | `/resources`           | `store`                      | Almacenar un nuevo recurso                   |
| `GET`          | `/resources/{id}`      | `show`                       | Mostrar un recurso específico                |
| `GET`          | `/resources/{id}/edit` | `edit`                       | Mostrar un formulario para editar un recurso |
| `PUT/PATCH`    | `/resources/{id}`      | `update`                     | Actualizar un recurso específico             |
| `DELETE`       | `/resources/{id}`      | `destroy`                    | Eliminar un recurso específico               |

***

## **Ejemplo: Definir rutas personalizadas para "posts"**

Supongamos que queremos gestionar un sistema de publicaciones (posts). Así deberíamos definir las rutas en el archivo `routes/web.php`:

```php
use App\Http\Controllers\PostController;

Route::get('/posts', [PostController::class, 'index'])->name('posts.index');       // Listar todos los posts
Route::get('/posts/create', [PostController::class, 'create'])->name('posts.create'); // Formulario para crear un post
Route::post('/posts', [PostController::class, 'store'])->name('posts.store');     // Guardar un nuevo post
Route::get('/posts/{id}', [PostController::class, 'show'])->name('posts.show');   // Mostrar un post específico
Route::get('/posts/{id}/edit', [PostController::class, 'edit'])->name('posts.edit'); // Formulario para editar un post
Route::put('/posts/{id}', [PostController::class, 'update'])->name('posts.update'); // Actualizar un post específico
Route::delete('/posts/{id}', [PostController::class, 'destroy'])->name('posts.destroy'); // Eliminar un post
```

***

## **Detalles importantes**

1. **Consistencia en los nombres de las rutas (`name`)**:
   * Al definir las rutas, asignamos un nombre que sigue el formato `recurso.acción` (por ejemplo, `posts.index`, `posts.create`). Estos nombres permiten referirnos a las rutas dinámicamente en las vistas o controladores sin depender de la URI exacta.
2. **Uso de parámetros**:
   * Cuando una ruta requiere identificar un recurso específico (como un post), utilizamos un parámetro en la URI. Por ejemplo, en la ruta `/posts/{id}`, `{id}` representa el identificador único del recurso.
3. **Buena práctica: generar URLs dinámicas**:
   *   En nuestras vistas Blade, siempre generaremos las URLs de manera dinámica utilizando el helper `route`:

       ```blade
       <a href="{{ route('posts.index') }}">Ver todos los posts</a>
       ```
4. **Separación de lógica**:
   * Cada acción se asocia con un método específico del controlador (por ejemplo, `index`, `create`, `store`). Esto nos ayuda a mantener el código organizado y fácil de mantener.

***

## **Ventajas de seguir estas convenciones**

* Facilita la transición a `Route::resource` en el futuro, ya que las rutas personalizadas seguirán el mismo estándar.
* Mejora la legibilidad y consistencia en todo el proyecto.
* Permite a otros desarrolladores comprender rápidamente la estructura de las rutas y las acciones asociadas.

