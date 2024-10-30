# GitHub Flow

**GitHub Flow** es un flujo de trabajo sencillo, ideal para proyectos en equipo donde cada integrante trabaja en distintas funcionalidades o correcciones sin afectar al trabajo de los demás. Siguiendo estos pasos, podrán colaborar de forma ordenada, revisando y discutiendo los cambios antes de integrarlos al proyecto principal.

Entre sus ventajas destacamos las siguientes:

1. **Simplicidad**: Solo requiere una rama principal (`main`) y ramas de características o correcciones de bugs (`feature` o `bugfix`), lo cual facilita su comprensión y uso.
2. **Trabajo independiente**: Cada desarrollador puede crear su propia rama para desarrollar una nueva funcionalidad o solucionar un bug. Esto permite que trabajen de forma paralela sin interferir en el trabajo de los demás.
3. **Proceso de Integración**: Una vez que un alumno completa su trabajo, puede crear un pull request para revisar y discutir el código antes de fusionarlo en la rama principal, promoviendo buenas prácticas de revisión.
4. **Fácil de Escalar**: Si deseas implementar un entorno de integración continua, GitHub Flow se adapta muy bien, lo que facilita futuras implementaciones y pruebas automáticas.

A continuación detallamos los pasos que seguiremos en nuestros desarrollos para implementar GitHub Flow.

### Paso 1: Crear una nueva rama

1. Antes de empezar a trabajar en una nueva funcionalidad, corrección o mejora, **crea una nueva rama** desde la rama `main`.
2.  Usa una convención de nombres clara y descriptiva. Por ejemplo:

    * Para una nueva funcionalidad: `feature/nombre-descriptivo`
    * Para corregir un error: `bugfix/descripcion-error`
    * Para mejorar el rendimiento o la experiencia: `improvement/nombre-mejora`
    * Para tareas de mantenimiento: `chore/nombre-tarea`

    **Ejemplos**:

    * `feature/autenticacion-usuarios`
    * `bugfix/error-login`
    * `improvement/optimizar-consultas`
    * `chore/actualizar-librerias`

### Sugerencias prácticas para nombrar las ramas

* **Usa guiones**: Emplea guiones (`-`) para separar palabras en lugar de espacios.
* **Sé breve y claro**: El nombre de la rama debe describir en pocas palabras el propósito del trabajo.
* **Mantén la consistencia**: Todos deben seguir el mismo formato de nombres para evitar confusiones.

### Paso 2: Hacer cambios en la rama nueva

1. Trabaja en la nueva rama y realiza tus cambios de manera independiente.
2. Asegúrate de probar el código localmente antes de pasar al siguiente paso.
3. Realiza commits frecuentemente para documentar el avance de tu trabajo.

### Paso 3: Crear un pull request

Cuando hayas terminado tus cambios en la rama, crea un **pull request**. Este es el proceso de proponer tus cambios para que el resto del equipo pueda revisarlos y discutirlos.

1. Ve a la plataforma GitHub y selecciona **Pull Request**.
2. Escribe una **descripción clara** del cambio realizado y su propósito.
3. Los compañeros o el profesorado pueden **revisar y comentar** tu código en el pull request.

### Paso 4: Revisar, comentar y ajustar el pull request

1. **Revisión del Código**: Los miembros del equipo revisan el pull request y dejan comentarios si es necesario.
2. **Realizar Ajustes**: Si recibes comentarios, puedes hacer ajustes adicionales en la misma rama y los cambios se reflejarán automáticamente en el pull request.
3. **Aprobación**: Una vez que todos estén de acuerdo, el pull request se aprueba para integrarse en `main`.

### Paso 5: Fusionar (Merge) los cambios en la rama `main`

1. Tras la aprobación, fusiona la rama en `main`.
2. **Elimina la rama** que ya no necesites, ya que el cambio ha sido integrado.

**GitHub Flow** ayuda a que el equipo trabaje de forma organizada y evite que el código en `main` se vea afectado por cambios no revisados.&#x20;

## Uso de etiquetas

En GitHub Flow, el uso de **etiquetas (tags)** no es un requisito formal, pero vamos a incluirlas para llevar un registro claro de las versiones del proyecto, especialmente cuando alcancemos hitos importantes o se desea tener puntos de referencia en el tiempo. Podrían ser útiles en los sisguientes casos:

1. **Etiquetas para versiones de lanzamiento**:
   * Crearemos etiquetas en la rama `main` cada vez que se alcance una nueva versión (Por ejemplo`v1.0`, `v1.1`, etc.). Esto ayuda a marcar el código estable y preparado para producción, facilitando un punto de retorno en caso de futuros cambios o ajustes.
2. **Etiquetas de hitos importantes**:
   * Podemos emplear etiquetas para marcar momentos específicos del desarrollo, como la finalización de la administración de usuarios o la implementación de una corrección importante.
   * Estas etiquetas permiten al equipo referenciar el estado del proyecto en puntos específicos, facilitando la organización y el control de versiones.
3. **Etiqueta de última versión estable**:
   * Para un flujo continuo de desarrollo, puede ser útil etiquetar la última versión estable en `main`. Así, cualquier persona del equipo sabe exactamente qué versión está completamente probada y aprobada.

Aunque GitHub Flow no incluye etiquetas de manera estricta, usarlas en estos momentos puede mejorar la trazabilidad y el control del proyecto.
