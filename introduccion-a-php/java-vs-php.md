# Java vs PHP

### 🧩 1. diferencias generales entre PHP y Java

**Objetivo**: Entender en qué contextos se usan ambos lenguajes y cómo se ejecutan.

#### 📌 PHP:

* Es un lenguaje de scripting diseñado específicamente para desarrollo web.
* Se ejecuta en el servidor y se incrusta fácilmente en HTML.
* Es interpretado: el código se analiza y ejecuta línea por línea cada vez que se carga la página.
* No necesita compilarse.

#### 📌 Java:

* Es un lenguaje de propósito general, fuertemente orientado a objetos.
* El código se compila a bytecode, que se ejecuta en la Máquina Virtual de Java (JVM).
* Se usa en muchas áreas: web, escritorio, móviles (Android), sistemas empresariales.

#### Ejemplo simple:

**PHP**

```php
phpCopiarEditar<?php
echo "Hola mundo";
?>
```

**Java**

```java
javaCopiarEditarpublic class Main {
    public static void main(String[] args) {
        System.out.println("Hola mundo");
    }
}
```

**Comparación**:

* En PHP, puedes escribir una línea de código dentro de un archivo `.php` y ejecutarla directamente en el navegador.
* En Java, necesitas compilar (`javac Main.java`) y luego ejecutar (`java Main`).

***

### 💾 2. declaración de variables y tipos

**PHP**:

* Usa tipado débil y dinámico. Las variables no requieren declarar el tipo.
* Todas las variables comienzan con `$`.
* El tipo puede cambiar en tiempo de ejecución.

**Java**:

* Tipado fuerte y estático. Cada variable necesita tener un tipo declarado.
* No se puede cambiar el tipo de una variable después de declararlo.

#### Ejemplo:

**PHP**

```php
phpCopiarEditar<?php
$nombre = "Ana";  // string
$edad = 30;       // integer
$activo = true;   // boolean
?>
```

**Java**

```java
javaCopiarEditarString nombre = "Ana";
int edad = 30;
boolean activo = true;
```

**Consecuencia práctica**:

* PHP es más permisivo, pero eso puede llevar a errores difíciles de detectar si no se controla bien el tipo de datos.
* Java te obliga a ser explícito, lo que previene errores, pero también hace que el código sea más verboso.

***

### 🔁 3. estructuras de control

Ambos lenguajes comparten las estructuras básicas: `if`, `else`, `while`, `for`, `switch`.

#### Ejemplo: bucle `for`

**PHP**

```php
phpCopiarEditar<?php
for ($i = 0; $i < 5; $i++) {
    echo "Valor: $i\n";
}
?>
```

**Java**

```java
javaCopiarEditarfor (int i = 0; i < 5; i++) {
    System.out.println("Valor: " + i);
}
```

**Explicación**:

* La lógica es la misma.
* En PHP puedes interpolar variables directamente dentro de strings con comillas dobles (`" "`).
* PHP usa `echo` o `print`, mientras que Java usa `System.out.println()`.

***

### 🧰 4. funciones y métodos

**PHP**:

* Las funciones se definen con `function`.
* Pueden estar dentro o fuera de una clase.

**Java**:

* Las funciones siempre están dentro de una clase.
* Se usan los modificadores de acceso (`public`, `private`) y el tipo de retorno.

#### Ejemplo:

**PHP**

```php
phpCopiarEditar<?php
function saludar($nombre) {
    return "Hola, $nombre";
}
echo saludar("Noa");
?>
```

**Java**

```java
javaCopiarEditarpublic class Saludador {
    public static String saludar(String nombre) {
        return "Hola, " + nombre;
    }
}
```

**Explicación**:

* En PHP es más flexible y rápido crear funciones sueltas.
* Java fuerza una estructura más formal y organizada desde el inicio.

***

### 🧱 5. programación orientada a objetos

**Objetivo**: Mostrar similitudes estructurales y diferencias de sintaxis entre ambos lenguajes en POO.

#### 📦 5.1. definición de clases y objetos

**PHP**

```php
phpCopiarEditar<?php
class Persona {
    private $nombre;

    public function __construct($nombre) {
        $this->nombre = $nombre;
    }

    public function saludar() {
        echo "Hola, soy $this->nombre\n";
    }
}
?>
```

**Java**

```java
javaCopiarEditarpublic class Persona {
    private String nombre;

    public Persona(String nombre) {
        this.nombre = nombre;
    }

    public void saludar() {
        System.out.println("Hola, soy " + nombre);
    }
}
```

**Similitudes**:

* Ambos lenguajes usan clases, constructores, visibilidad (`private`, `public`) y métodos.

**Diferencias**:

* PHP usa `$this->` para acceder a propiedades y métodos del objeto.
* Java usa `this.`.
* En PHP todo comienza con `$`, tanto variables como propiedades.

***

#### 👨‍👩‍👦 5.2. herencia

**PHP**

```php
phpCopiarEditar<?php
class Estudiante extends Persona {
    private $curso;

    public function __construct($nombre, $curso) {
        parent::__construct($nombre);
        $this->curso = $curso;
    }
}
?>
```

**Java**

```java
javaCopiarEditarpublic class Estudiante extends Persona {
    private int curso;

    public Estudiante(String nombre, int curso) {
        super(nombre);
        this.curso = curso;
    }
}
```

**Claves**:

* Ambos lenguajes usan `extends` para la herencia simple.
* `super` (Java) y `parent::` (PHP) permiten llamar al constructor de la clase base.

***

#### 🔧 5.3. interfaces

**PHP**

```php
phpCopiarEditar<?php
interface Enviable {
    public function enviar();
}
?>
```

**Java**

```java
javaCopiarEditarpublic interface Enviable {
    void enviar();
}
```

Ambos lenguajes usan interfaces para definir contratos que deben implementar las clases. PHP también permite usar "traits", que no existen en Java.

***

### 🔍 6. otras diferencias importantes

| Concepto                | PHP                                   | Java                             |
| ----------------------- | ------------------------------------- | -------------------------------- |
| Manejo de errores       | `try/catch`, pero más permisivo       | `try/catch`, muy estricto        |
| Ambientes de desarrollo | Apache/Nginx + PHP (XAMPP, Laragon…)  | IDE (Eclipse, IntelliJ) + JDK    |
| Archivos                | `.php` (pueden mezclarse con HTML)    | `.java` → `.class` → ejecutables |
| Ejecución web           | Ideal para scripts embebidos en HTML  | Necesita frameworks como Spring  |
| Comunidad web           | Muy extensa, ideal para principiantes | Muy extendida en la industria    |

***

### 🎓 actividad final sugerida (si hay tiempo)

Mostrarles este script y pedir que lo comparen mentalmente con Java:

```php
phpCopiarEditar<?php
class Producto {
    public $nombre;
    public $precio;

    public function __construct($nombre, $precio) {
        $this->nombre = $nombre;
        $this->precio = $precio;
    }

    public function mostrar() {
        echo "$this->nombre cuesta $this->precio €\n";
    }
}

$p = new Producto("Ratón inalámbrico", 19.99);
$p->mostrar();
?>
```

***

### 🧠 Resumen

* PHP y Java son potentes pero diferentes: uno es ligero y flexible, el otro es más estructurado y robusto.
* Entender sus diferencias te permite elegir mejor la herramienta para cada proyecto.
* Ambos permiten POO, pero la implementación varía en rigor, sintaxis y contexto de uso.
