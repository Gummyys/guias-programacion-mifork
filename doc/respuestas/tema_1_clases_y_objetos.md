<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Clases y Objetos". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: ninguno.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->

# TEMA 1. Clases y objetos

# 1. Las cuatro características básicas de la Programación Orientada a Objetos (POO)

1.  **Encapsulamiento**
    *   Consiste en **ocultar los detalles internos** de un objeto y exponer solo lo necesario.
    *   Protege los datos y evita modificaciones indebidas, normalmente mediante **atributos privados** y **métodos públicos**.

2.  **Abstracción**
    *   Permite **simplificar la complejidad** mostrando solo las características esenciales de un objeto.
    *   Se centra en *qué hace* un objeto, no en *cómo lo hace*.

3.  **Herencia**
    *   Permite que una clase (subclase) **herede atributos y métodos** de otra clase (superclase).
    *   Facilita la reutilización de código y la creación de jerarquías lógicas.

4.  **Polimorfismo**
    *   Permite que **un mismo método** tenga **distintos comportamientos** según el objeto que lo utilice.
    *   Se aplica mediante *sobrecarga* (mismo nombre, distintos parámetros) y *sobrescritura* (la subclase redefine el método de la superclase).

***
***

# 2. Lenguajes populares que permitan la programación orientada a objetos

**Cuatro lenguajes populares** que permiten la programación orientada a objetos:

1.  **C++**  
    Ampliamente usado en sistemas, videojuegos y aplicaciones de alto rendimiento. Soporta POO de forma completa.

2.  **Java**  
    Uno de los lenguajes más extendidos en empresas. Su diseño está fuertemente basado en la POO.

3.  **Python**  
    Aunque es multiparadigma, ofrece un modelo de objetos muy flexible y sencillo de usar.

4.  **C#**  
    Desarrollado por Microsoft, usado en aplicaciones de escritorio, web, móviles y videojuegos (Unity). Totalmente orientado a objetos.

***
***

# 3. Paradigmas anteriores a la POO

## ¿Qué es la **programación estructurada**?

La **programación estructurada** es un paradigma que surgió para mejorar el desorden y la complejidad del código “espagueti” típico de los primeros programas llenos de saltos `goto`.  
Su idea principal es **organizar el programa en estructuras de control bien definidas**, sin saltos arbitrarios.

Se basa en **tres tipos básicos de estructuras**:

1.  **Secuencia**: instrucciones ejecutadas una detrás de otra.
2.  **Selección**: decidir entre varias alternativas (por ejemplo, `if`, `switch`).
3.  **Iteración**: repetir acciones (`for`, `while`).

Con estas tres estructuras se puede escribir cualquier programa sin necesidad de usar `goto`, lo que hace el código:

*   Más **legible**
*   Más **fácil de depurar**
*   Más **mantenible**

***

## ¿Qué es la **programación modular**?

La **programación modular** es una evolución natural de la programación estructurada.  
Su objetivo es **dividir un programa grande en partes más pequeñas llamadas módulos**, cada una con una función muy concreta.

Un **módulo** es un bloque de código que:

*   Realiza una tarea específica
*   Es independiente del resto lo máximo posible
*   Tiene una **interfaz bien definida** (p. ej., funciones públicas)
*   Oculta sus detalles internos (idea que luego heredará la POO como *encapsulamiento*)

### Ventajas clave:

*   Facilita el **mantenimiento** de grandes programas
*   Permite **reutilizar** módulos en otros proyectos
*   Divide el trabajo entre varios programadores
*   Reduce los errores al trabajar con piezas más pequeñas y controladas

***

## Relación entre ambas

*   La **programación estructurada** organiza la lógica interna del código.
*   La **programación modular** organiza el **proyecto completo** en bloques grandes y bien definidos.

Juntas crearon la base conceptual de lo que luego evolucionó en la **Programación Orientada a Objetos**, donde los módulos ya no son simples funciones o archivos, sino **objetos**.

***
***

# 4. Elementos que definen a un objeto en programación orientada a objetos

En programación orientada a objetos, **un objeto** se define por **tres elementos fundamentales**:

## 1. **Atributos (o propiedades)**

Son los **datos** que describen el estado del objeto.  
Representan *características* del objeto en la vida real.

Ejemplo:  
Un objeto `Coche` puede tener atributos como:

*   `color`
*   `marca`
*   `velocidad`

## 2. **Métodos (o comportamientos)**

Son las **acciones** que el objeto puede realizar o las operaciones que puede ejecutar.  
Definen cómo interactúa el objeto con el exterior y consigo mismo.

Ejemplo:  
El objeto `Coche` puede tener métodos como:

*   `acelerar()`
*   `frenar()`
*   `tocarClaxon()`

## 3. **Identidad**

Es lo que **distingue un objeto de otro**, aunque tengan los mismos atributos.  
Dos objetos pueden tener propiedades idénticas, pero siguen siendo instancias distintas.

Ejemplo:  
Dos coches rojos de la misma marca, modelo y velocidad siguen siendo **dos coches diferentes**, no el mismo objeto.

***
***

# 5. **Clase, objeto e instancia: diferencias y aclaraciones**

## **¿Qué es una *clase*?**

Una **clase** es un *modelo* o *plantilla* que define qué atributos y métodos tendrán sus objetos.  
Es una descripción general, **no ocupa memoria** hasta que se crean objetos.

Ejemplo sencillo en C++:

```cpp
class Coche {
public:
    string color;
    void arrancar() { /* ... */ }
};
```

La clase dice *qué es* un coche y *qué puede hacer*.

***

## **¿Es lo mismo una clase que un objeto?**

**No. Son cosas distintas:**

*   La **clase** es el *concepto*, el plano, la definición.
*   El **objeto** es el *resultado real* creado a partir de esa clase.

Analogía:

*   Clase = plano de una casa
*   Objeto = casa construida a partir del plano

En programación:

```cpp
Coche miCoche;  // ← Esto es un objeto
```

***

## **¿Qué es una instancia?**

Una **instancia** es simplemente **un objeto creado a partir de una clase**.

Así que:

*   “Objeto” e “instancia” suelen referirse a *lo mismo*.
*   Se dice que un objeto es *una instancia de la clase X*.

Ejemplo:

```cpp
Coche coche1;  // coche1 es una instancia de Coche
Coche coche2;  // coche2 es otra instancia distinta
```

***

## **¿Todos los lenguajes orientados a objetos manejan el concepto de clase?**

**No.**  
Muchos sí, pero **no todos los lenguajes orientados a objetos usan clases**.

### ✔ Lenguajes con clases (clásicos)

*   C++
*   Java
*   C#
*   Python (sí tiene clases, aunque sea multiparadigma)

### ✔ Lenguajes orientados a objetos *sin* clases (basados en prototipos)

*   **JavaScript**
*   **Lua**

Estos lenguajes están basados en **objetos prototípicos**, donde no hay clases formales:  
los objetos se crean copiando otros objetos (los prototipos).

JavaScript, por ejemplo, tiene hoy una sintaxis de “clase”, pero *por debajo* sigue funcionando con prototipos.

***

## Resumen rápido

| Concepto                              | Qué es                                                            |
| ------------------------------------- | ----------------------------------------------------------------- |
| **Clase**                             | Modelo o plantilla que define atributos y métodos.                |
| **Objeto**                            | Entidad real creada a partir de una clase; tiene estado propio.   |
| **Instancia**                         | Sinónimo práctico de objeto; objeto creado a partir de una clase. |
| **¿Todos los lenguajes usan clases?** | No. Algunos usan prototipos (JavaScript, Lua).                    |

***
***

# 6.1. **¿Dónde se almacenan en memoria los objetos?**

La respuesta depende del **lenguaje de programación**, pero en general:

## ✔ En la mayoría de lenguajes orientados a objetos (como **Java**):

Los **objetos se almacenan en el *heap***.

### 🧠 ¿Por qué en el *heap*?

*   El *heap* es la zona de memoria destinada a datos que **pueden cambiar de tamaño** y **viven más tiempo**.
*   Los objetos se crean en tiempo de ejecución con `new`, así que necesitan esta flexibilidad.

Ejemplo en Java:

```java
Persona p = new Persona(); // el objeto Persona está en el heap
```

La **referencia** `p` se guarda en la **pila (stack)**, pero  
**el objeto real está en el *heap***.

***

# ✔ ¿Es igual en todos los lenguajes?

## **No. Cambia según el lenguaje.**

### 🔹 **Java, C#, Python**

→ **Los objetos viven en el *heap***.  
La gestión de memoria se realiza automáticamente mediante **recolección de basura**.

### 🔹 **C++**

En C++ los objetos pueden almacenarse en varios lugares:

*   En el **stack**
    ```cpp
    Coche c;   // objeto en stack
    ```

*   En el **heap** (si usas `new`)
    ```cpp
    Coche* c = new Coche();  // objeto en heap
    ```

*   Incluso en zonas especiales como **memoria estática**.

***

# 6.2. **¿Qué es la recolección de basura (garbage collection)?**

La **recolección de basura** es un proceso automático que:

### ✔ Libera memoria ocupada por objetos que **ya no se están usando**

Es decir, por objetos que **no tienen referencias** apuntando hacia ellos.

### ✔ ¿Qué ventajas tiene?

*   Evita fugas de memoria (*memory leaks*)
*   Facilita el trabajo del programador
*   Hace el programa más seguro y estable

### ✔ ¿Qué lenguajes la usan?

*   Java
*   C#
*   Python
*   Kotlin

### ✔ ¿Qué lenguajes *no la usan*?

*   **C y C++** → El programador debe liberar la memoria manualmente con `delete` o `free`.

***

# 🟦 Resumen claro

| Concepto                              | Explicación                                               |
| ------------------------------------- | --------------------------------------------------------- |
| **Dónde están los objetos (Java)**    | En el *heap*                                              |
| **Dónde está la referencia**          | En el *stack*                                             |
| **¿Es igual en todos los lenguajes?** | No; depende del lenguaje                                  |
| **Recolección de basura**             | Sistema automático que libera memoria de objetos sin usar |

***
***

# 7.1. **¿Qué es un método?**

Un **método** es una función que pertenece a una **clase** y define una **acción** o **comportamiento** que los objetos de esa clase pueden realizar.

En otras palabras:  
➡️ **Un método es lo que un objeto *puede hacer*.**

### Ejemplo en Java:

```java
class Coche {
    void arrancar() {
        System.out.println("El coche está arrancando...");
    }
}
```

`arrancar()` es un **método** de la clase `Coche`.

***

# 7.2. **¿Qué es la *sobrecarga de métodos*?**

La **sobrecarga de métodos (method overloading)** ocurre cuando **varios métodos tienen el mismo nombre**, pero **diferentes parámetros**.

Los métodos sobrecargados se diferencian por:

*   número de parámetros
*   tipo de parámetros
*   orden de parámetros

👉 **No se diferencian por el tipo de retorno.**

### Ejemplo en Java de sobrecarga:

```java
class Calculadora {
    int sumar(int a, int b) {
        return a + b;
    }

    double sumar(double a, double b) {
        return a + b;
    }

    int sumar(int a, int b, int c) {
        return a + b + c;
    }
}
```

Aquí tenemos **tres métodos llamados `sumar`**, pero cada uno funciona con parámetros distintos.  
Esto es **sobrecarga**.

***

## Resumen rápido

| Concepto                  | Explicación                                                           |
| ------------------------- | --------------------------------------------------------------------- |
| **Método**                | Acción o comportamiento de un objeto.                                 |
| **Sobrecarga de métodos** | Varios métodos con el mismo nombre pero distinta lista de parámetros. |

***
***

## 8. Ejemplo mínimo de clase en Java, que se llame Punto, con dos atributos, x e y, con un método que se llame `calculaDistanciaAOrigen`, que calcule la distancia a la posición 0,0. Por sencillez, los atributos deben tener visibilidad por defecto. Crea además un ejemplo de uso con una instancia y uso del método

# Clase `Punto` y ejemplo de uso

### ✔ Requisitos cumplidos:

*   Nombre de la clase: **Punto**
*   Dos atributos: **x** e **y**
*   Visibilidad **por defecto** (es decir, *package-private*)
*   Método `calculaDistanciaAOrigen()`
*   Ejemplo de creación de un objeto y llamada al método

***

## 📌 Código de la clase `Punto`

```java
class Punto {
    int x;  // visibilidad por defecto
    int y;  // visibilidad por defecto

    double calculaDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }
}
```

***

## 📌 Ejemplo de uso

```java
public class Main {
    public static void main(String[] args) {
        Punto p = new Punto();
        
        p.x = 3;
        p.y = 4;

        double distancia = p.calculaDistanciaAOrigen();
        System.out.println("Distancia al origen: " + distancia);
    }
}
```

***

### ✔ ¿Qué imprimirá?

Como `(3,4)` forma el típico triángulo pitagórico:

    Distancia al origen: 5.0

***
***

# 9. Punto de entrada, `static` y `final` en Java

## ✔ ¿Cuál es el **punto de entrada** de un programa en Java?

En Java, **todo programa comienza ejecutando el método `main`** con esta firma exacta:

```java
public static void main(String[] args)
```

Este método es el punto de entrada porque la **JVM** lo busca explícitamente al iniciar el programa.

***

## ✔ ¿Qué es `static`?

La palabra clave **`static`** significa que un atributo o método **pertenece a la clase**, no a las instancias (objetos).

En otras palabras:  
➡️ Algo `static` existe incluso **sin crear objetos**.

Ejemplo:

```java
class Contador {
    static int total = 0;  // pertenece a la clase, no a objetos
}
```

Puedes acceder así:

```java
System.out.println(Contador.total);
```

***

## ✔ ¿Para qué se usa `static` en el método `main`?

El método `main` debe ser `static` porque:

*   La JVM necesita ejecutarlo **sin crear ningún objeto previamente**
*   Si fuese no estático, tendrías que instanciar una clase antes de poder llamar a `main`, lo cual es imposible sin que ya exista un punto de entrada

Por eso:

```java
public static void main(String[] args)
```

es obligatorio tal cual.

***

## ✔ ¿Sólo se usa `static` para el `main`?

No. `static` se usa para otras cosas, por ejemplo:

### 1️⃣ **Atributos de clase (variables estáticas)**

Compartidos por **todas** las instancias.

```java
static int contadorObjetos;
```

### 2️⃣ **Métodos de clase**

Métodos que se pueden llamar sin crear objetos.

```java
static void mostrarMensaje() {
    System.out.println("Hola");
}
```

### 3️⃣ **Bloques estáticos**

Se ejecutan una vez cuando se carga la clase.

```java
static {
    System.out.println("Cargando clase...");
}
```

### 4️⃣ **Clases internas estáticas**

```java
static class Nodo { }
```

***

## ✔ ¿Para qué se combina `static` con `final`?

La combinación **`static final`** se usa para crear **constantes**, es decir:

*   Son de la clase (no de los objetos)
*   No pueden cambiarse una vez asignadas

Ejemplo típico:

```java
static final double PI = 3.14159;
```

Esto sirve para valores constantes que deben ser accesibles desde cualquier parte del programa, y que no deben modificarse.

***

# 🟦 Resumen claro

| Concepto                     | Explicación                                            |
| ---------------------------- | ------------------------------------------------------ |
| **Punto de entrada de Java** | `public static void main(String[] args)`               |
| **static**                   | Pertenecen a la clase, no a los objetos                |
| **¿Solo para `main`?**       | No, también para atributos, métodos y bloques de clase |
| **static + final**           | Constantes de clase (no cambian jamás)                 |

***
***

## 10. Intenta ejecutar un poco de Java de forma básica, con los comandos `javac` y `java`. ¿Cómo podemos compilar el programa y ejecutarlo desde linea de comandos? ¿Java es compilado? ¿Qué es la **máquina virtual**? ¿Qué es el *byte-code* y los ficheros `.class`?

### Respuesta:


## 11. En el código anterior de la clase `Punto` ¿Qué es `new`? ¿Qué es un **constructor**? Pon un ejemplo de constructor en una clase `Empleado` que tenga DNI, nombre y apellidos

### Respuesta:


## 12. ¿Qué es la referencia `this`? ¿Se llama igual en todos los lenguajes? Pon un ejemplo del uso de `this` en la clase `Punto`

### Respuesta:


## 13. Añade ahora otro nuevo método que se llame `distanciaA`, que reciba un `Punto` como parámetro y calcule la distancia entre `this` y el punto proporcionado

### Respuesta:


## 14. El paso del `Punto` como parámetro a un método, es **por copia** o **por referencia**, es decir, si se cambia el valor de algún atributo del punto pasado como parámetro, dichos cambios afectan al objeto fuera del método? ¿Qué ocurre si en vez de un `Punto`, se recibiese un entero (`int`) y dicho entero se modificase dentro de la función? 

### Respuesta:


## 15. ¿Qué es el método `toString()` en Java? ¿Existe en otros lenguajes? Pon un ejemplo de `toString()` en la clase `Punto` en Java

### Respuesta:


## 16. Reflexiona: ¿una clase es como un `struct` en C? ¿Qué le falta al `struct` para ser como una clase y las variables de ese tipo ser instancias?


### Respuesta:


## 17. Quitemos un poco de magia a todo esto: ¿Como se podría “emular”, con `struct` en C, la clase `Punto`, con su función para calcular la distancia al origen? ¿Qué ha pasado con `this`?

### Respuesta:
