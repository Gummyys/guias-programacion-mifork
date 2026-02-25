<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Excepciones". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos, Encapsulación.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# TEMA 3. Excepciones

#### 1. Empecemos un tema sobre control de errores en lenguajes de programación, con algo básico. En C, donde no existen las excepciones, pongamos un ejemplo de una raíz que toma número flotante positivo. Queremos controlar el error si la función recibe un número negativo. El usuario debe ser informado pero desde fuera de la función `raiz` ¿Cómo indicamos ese error?. Enumera dos opciones diferentes de diseñar, poniendo un ejemplo de código de cada una.

***

## ✅ **1. Opción 1: Usar un valor especial de retorno + una variable externa para indicar el error**

En C es típico devolver un valor “sentinela” (por ejemplo `-1.0`) y que la función establezca una **variable global** o **una variable pasada por referencia** que indique si hubo error.

### ✔️ Ejemplo en C usando un parámetro por referencia para señalar el error

```c
#include <stdio.h>
#include <math.h>

double raiz(double x, int *error) {
    if (x < 0) {
        *error = 1;      // indicamos error
        return -1.0;     // valor sentinela
    }
    *error = 0;          // sin error
    return sqrt(x);
}

int main() {
    int err;
    double r = raiz(-9, &err);

    if (err) {
        printf("Error: número negativo\n");
    } else {
        printf("Resultado: %f\n", r);
    }
}
```

**Ventaja:** sencillo.  
**Desventaja:** el valor devuelto puede confundirse con un resultado válido.

***

## ✅ **Opción 2: Devolver el resultado por referencia y usar el valor de retorno como código de error**

Aquí **la función no devuelve el resultado directamente**, sino que escribe el resultado en una variable que recibe por referencia.  
El valor de retorno (`int`) se usa para indicar si hubo error o no.

### ✔️ Ejemplo en C devolviendo código de error

```c
#include <stdio.h>
#include <math.h>

int raiz(double x, double *resultado) {
    if (x < 0) {
        return -1;   // código de error
    }

    *resultado = sqrt(x);
    return 0;        // éxito
}

int main() {
    double r;
    int code = raiz(-9, &r);

    if (code != 0) {
        printf("Error: número negativo\n");
    } else {
        printf("Resultado: %f\n", r);
    }
}
```

**Ventaja:** los códigos de error son claros y no hay ambigüedad sobre el valor del resultado.  
**Desventaja:** obliga a trabajar siempre con punteros.

***

# 🧩 Resumen

| Opción                                            | Mecanismo                            | Qué devuelve la función | Cómo avisa del error |
| ------------------------------------------------- | ------------------------------------ | ----------------------- | -------------------- |
| **1. Valor especial + flag externo**              | Devuelve resultado o valor sentinela | `double`                | Parámetro `error`    |
| **2. Código de error + resultado por referencia** | Devuelve estado                      | `int`                   | Valor de retorno     |

***
***

# 2.1 ✅ ¿Qué es una *excepción*?

Una **excepción** es un mecanismo que permite **detectar y gestionar situaciones anómalas** (errores) que ocurren durante la ejecución de un programa.  
Cuando una operación no puede completarse correctamente (por ejemplo, dividir entre cero, acceder fuera de un array o intentar abrir un fichero inexistente), se **lanza una excepción**.

La excepción **interrumpe el flujo normal del programa** y transfiere el control a un bloque preparado para manejar ese problema.

***

# 2.2 🎯 ¿Para qué las usa un programador?

Los programadores utilizan las excepciones para lograr dos objetivos fundamentales:

***

## ✔️ 1. **Cuando implementa funciones**

Para **informar automáticamente al exterior** de que ocurrió un error, sin depender de valores especiales de retorno (como en C).  
Esto permite separar la *lógica normal* de la *lógica de error*.

### Ejemplo en Java (función que lanza una excepción)

```java
public static double raiz(double x) throws IllegalArgumentException {
    if (x < 0) {
        throw new IllegalArgumentException("El número no puede ser negativo.");
    }
    return Math.sqrt(x);
}
```

***

## ✔️ 2. **Cuando llama a funciones**

Para poder **manejar el error de manera controlada**, evitando que el programa se detenga abruptamente.

### Ejemplo en Java (manejo de la excepción)

```java
try {
    double r = raiz(-9);
    System.out.println("Resultado: " + r);
} catch (IllegalArgumentException e) {
    System.out.println("Error al calcular: " + e.getMessage());
}
```

De esta manera, el programador:

*   Evita que el programa falle inesperadamente.
*   Puede mostrar mensajes útiles al usuario.
*   Mantiene el código más limpio y ordenado.

***

# 🧩 Resumen breve

| Aspecto                  | Explicación                                                                                  |
| ------------------------ | -------------------------------------------------------------------------------------------- |
| **Qué es una excepción** | Un mecanismo para señalar errores durante la ejecución.                                      |
| **Para qué sirven**      | Para detener el flujo normal e informar de un problema.                                      |
| **Por qué se usan**      | Separan la lógica normal de la gestión de errores y permiten manejar fallos de forma segura. |

***
***

### **3.** Reescribe el mismo ejemplo de raiz, pero en Java, metiendo ese método en una clase `Calculadora` y llama a dicho método desde el método `main`, mostrando cómo se puede controlar desde fuera.

***

## ✅ Clase `Calculadora` con el método `raiz`

```java
public class Calculadora {

    public static double raiz(double x) throws IllegalArgumentException {
        if (x < 0) {
            throw new IllegalArgumentException("El número no puede ser negativo.");
        }
        return Math.sqrt(x);
    }
}
```

***

## ✅ Clase principal con `main` llamando a `Calculadora.raiz`

```java
public class Main {
    public static void main(String[] args) {

        try {
            double resultado = Calculadora.raiz(-9);
            System.out.println("Resultado: " + resultado);

        } catch (IllegalArgumentException e) {
            System.out.println("Error al calcular la raíz: " + e.getMessage());
        }

        System.out.println("Programa terminado.");
    }
}
```

***

# 🧩 Explicación breve

1.  **La clase `Calculadora`** define el método `raiz`, que:
    *   Comprueba si el número es negativo.
    *   En caso de error, **lanza una excepción** (`IllegalArgumentException`).
    *   Si es válido, devuelve la raíz cuadrada.

2.  **El método `main`**:
    *   Llama a `Calculadora.raiz(...)`.
    *   Usa un bloque `try/catch` para **capturar y manejar** la excepción.
    *   El programa continúa funcionando sin cortarse abruptamente.

***
***

# 4.1 ✅ ¿Qué es *"lanzar"* una excepción?

**Lanzar una excepción** significa **interrumpir el flujo normal del programa** y crear un objeto de tipo excepción que indica que ha ocurrido un error.

En tu método:

```java
throw new IllegalArgumentException("El número no puede ser negativo.");
```

Aquí:

*   El programa **detiene** la ejecución normal del método `raiz`.
*   Se crea una excepción `IllegalArgumentException`.
*   Esa excepción “salta” hacia arriba buscando alguien que la controle.

***

# 4.2 ✅ ¿Qué es *"controlar"* o *"capturar"* una excepción?

Controlar (o capturar) una excepción significa **interceptarla** usando un bloque `try/catch` y decidir qué hacer con ese error (mostrar un mensaje, recuperar el programa, etc.).

Ejemplo desde `main`:

```java
try {
    double r = Calculadora.raiz(-9);
    System.out.println("Resultado: " + r);

} catch (IllegalArgumentException e) {
    System.out.println("Error al calcular la raíz: " + e.getMessage());
}
```

Ahí el `catch` **controla** la excepción lanzada por `raiz`.

***

# 4.3 ✅ ¿Qué es que una excepción se *"propage"*?

Cuando un método **lanza** una excepción y **no la captura**, la excepción se envía automáticamente al **método que lo llamó**.

Si ese método tampoco la captura, sigue subiendo por la **pila de llamadas**, y así sucesivamente, hasta que:

*   alguien la capture, o
*   llegue al método `main` → si tampoco la captura, el programa termina con error.

***

# 4.4 🧱 ¿Qué ocurre con las funciones en la **pila de llamadas** durante la propagación?

Imagina este flujo:

    main → A → B → Calculadora.raiz

Y `raiz(-9)` lanza una excepción.  
Lo que ocurre es:

1.  **`raiz` se interrumpe** inmediatamente (no sigue ejecutando nada después del `throw`).
2.  La excepción sube a **B**.
    *   Si B no tiene `try/catch` → **se termina B** automáticamente.
3.  La excepción sube a **A**.
    *   Si A no tiene `try/catch` → **se termina A**.
4.  Llega a **main**.
    *   Si `main` tiene un `catch`, la controla.
    *   Si no lo tiene, el programa finaliza con error.

👉 **Cada función que no controla la excepción queda abortada**, como si nunca hubiera terminado normalmente.

***

# 4.5 🚫 ¿Las funciones que no controlan la excepción se reanudan después?

**No. Nunca.**

Una vez que una función se ve interrumpida por una excepción y **no la captura**, esa función:

*   **Termina abruptamente**.
*   **No vuelve a continuar** desde donde se lanzó la excepción.
*   **No ejecuta código que viniera después del punto del error** (aunque tuviera más instrucciones).

La única parte que sí se garantiza que se ejecuta es un posible bloque `finally`.

***

# 🧩 Ejemplo completo con flujo explicado

```java
public class Calculadora {

    public static double raiz(double x) throws IllegalArgumentException {
        if (x < 0) {
            throw new IllegalArgumentException("El número no puede ser negativo.");
        }
        return Math.sqrt(x);
    }
}
```

```java
public class Main {

    public static void main(String[] args) {
        System.out.println("Inicio");

        try {
            double r = Calculadora.raiz(-9);  // ← aquí se lanza la excepción
            System.out.println("Resultado: " + r); // ← ESTO NO SE EJECUTA

        } catch (IllegalArgumentException e) {
            System.out.println("Error capturado: " + e.getMessage());
        }

        System.out.println("Fin del programa");
    }
}
```

### Flujo real:

1.  `main` llama a `raiz(-9)`.
2.  `raiz` lanza la excepción.
3.  `main` **captura** la excepción.
4.  El mensaje del `catch` se muestra.
5.  El programa **continúa con normalidad**.

***

# 📌 Resumen muy breve (ideal para examen)

*   **Lanzar** una excepción → interrumpir el método y notificar un error.
*   **Capturar** una excepción → manejar el error con `try/catch`.
*   **Propagar** una excepción → la excepción sube por la pila si no se captura.
*   Métodos por los que pasa la excepción → **se abortan**, no se reanudan.
*   Solo se ejecuta el código que esté en un bloque `finally` si existe.

***
***

# 5. ✅ Ventajas de la *propagación natural* de las excepciones en Java (frente a C)

En C, el programador debe **propagar manualmente** el error devolviendo códigos especiales o usando punteros/variables externas.  
En Java, la propagación es **automática**: si un método no captura una excepción, esta sube sola por la pila de llamadas (*stack*).

Esto aporta varias ventajas importantes:

***

# ✔️ 1. **Menos código repetitivo**

En C, cada función debe comprobar explícitamente códigos de error devueltos por otras funciones:

```c
int code = funcionA();
if (code != 0) return code;
```

Este patrón debe repetirse en todos los niveles.  
En Java, si no capturas la excepción, **simplemente se propaga sola**, sin escribir nada.

***

# ✔️ 2. **La lógica normal del programa queda más limpia**

El código en C mezcla:

*   lógica normal
*   comprobación de errores
*   propagación manual del error

En Java, el método solo se ocupa de su tarea:

```java
return Math.sqrt(x);
```

Y si algo falla:

```java
throw new IllegalArgumentException();
```

La propagación ya la hace el sistema automáticamente, manteniendo el código **más limpio y legible**.

***

# ✔️ 3. **Es imposible “olvidarse” de pasar el error hacia arriba**

En C, un programador puede cometer errores como:

*   no comprobar el valor devuelto
*   no propagarlo correctamente
*   devolver valores incorrectos

En Java, si un método no controla la excepción, el sistema **siempre la propaga automáticamente** por la pila de llamadas.  
No hay riesgo de que el error “desaparezca”.

***

# ✔️ 4. **Los métodos intermedios no se ejecutan parcialmente**

En C, si no controlas bien los códigos de error, puede ocurrir:

*   se ejecuta parte del método
*   luego se detecta el error
*   pero ya se han modificado datos o recursos

Java, en cambio:

*   **interrumpe** el método en el punto exacto del error
*   **descarta** automáticamente todos los métodos intermedios
*   garantiza que no continúa ningún método que no deba

Esto evita muchos errores lógicos.

***

# ✔️ 5. **La pila se desenrolla automáticamente y se liberan los recursos**

En C, liberar recursos (memoria, ficheros…) depende del programador y es fácil olvidarse de hacerlo en caso de error.  
En Java:

*   la propagación *desenrolla* la pila
*   se ejecutan automáticamente los bloques `finally`
*   se asegura una limpieza ordenada del estado

***

# ✔️ 6. **Las excepciones llevan información detallada**

Una excepción en Java incluye:

*   tipo de error
*   mensaje
*   *stack trace*

Un simple código de error en C no contiene esta información; hay que construirla manualmente.

***

# ✔️ 7. **Simplifica el análisis del flujo del programa**

La lógica de “quién maneja el error” es clara:

*   Si un método no captura una excepción, **sube automáticamente**.

Esto hace mucho más fácil razonar sobre el comportamiento del programa ante fallos.

***

# 🧩 Ejemplo aplicado al caso de `Calculadora.raiz()`

En C, cada función que llamase a `raiz()` tendría que comprobar el error y reenviarlo manualmente.

En Java:

```java
public static double raiz(double x) {
    if (x < 0) {
        throw new IllegalArgumentException("Número negativo");
    }
    return Math.sqrt(x);
}
```

Si `main()` no la captura, sube.  
Si otra función llamó a `main()`, sube más.  
Todo ocurre **sin escribir ni una línea extra**.

***

# 📌 Resumen breve

La propagación natural de excepciones en Java es mejor que el manejo manual de errores en C porque:

*   elimina código repetitivo
*   evita errores humanos
*   limpia y separa la lógica normal del código de error
*   asegura una gestión ordenada de recursos
*   aporta información rica del fallo
*   aborta automáticamente funciones intermedias sin dejarlas en estados inconsistentes

***
***

# 6.1 ✅ ¿En orientación a objetos, las excepciones suelen ser objetos?

**Sí.**  
En los lenguajes orientados a objetos (como Java), **todas las excepciones son objetos** que heredan de la clase base `Throwable`.

Ejemplo rápido:

```java
try {
    int x = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println(e.getClass());  // ← es un objeto real
}
```

Las excepciones **no son simples códigos numéricos** (como en C), sino instancias de clases con atributos, métodos y herencia.

***

# 6.2 🎯 ¿Qué ventajas aporta esto en términos de encapsulación?

Al ser objetos, las excepciones:

### ✔️ 1. **Pueden encapsular información útil**

Una excepción puede incluir:

*   un mensaje descriptivo
*   la causa de otro error interno
*   datos adicionales
*   un *stack trace* automático

Todo esto está **empaquetado dentro del propio objeto**, lo cual mejora muchísimo la capacidad de diagnóstico.

```java
throw new IllegalArgumentException("Valor fuera de rango");
```

Este objeto guarda:

*   tipo de error
*   mensaje
*   pila de llamadas

En C, toda esta información debería construirse manualmente.

***

### ✔️ 2. **Permiten agrupar errores por jerarquías**

Java usa herencia para clasificar las excepciones:

    Throwable
     ├── Exception
     │     ├── IOException
     │     ├── ArithmeticException
     │     └── … 
     └── Error

Esto facilita:

*   capturar tipos concretos
*   o capturar familias enteras de errores
*   o diferenciar entre errores recuperables y no recuperables

***

### ✔️ 3. **Se separa claramente la lógica del error**

La excepción lleva **su propia información**, no hace falta mezclarla con:

*   variables auxiliares
*   valores de retorno especiales
*   constantes mágicas

La lógica del programa queda más limpia (más encapsulación).

***

# 6.3 🧩 ¿Podemos crear excepciones personalizadas?

**Sí. Por supuesto.**  
Es una de las grandes ventajas.  
En Java, simplemente se crea una clase que herede de `Exception` o `RuntimeException`.

***

## **✔️ Ejemplo de excepción personalizada en Java**

```java
public class NumeroNegativoException extends Exception {

    public NumeroNegativoException(String mensaje) {
        super(mensaje);
    }
}
```

Y usarla en tu `Calculadora`:

```java
public class Calculadora {

    public static double raiz(double x) throws NumeroNegativoException {
        if (x < 0) {
            throw new NumeroNegativoException("El número no puede ser negativo.");
        }
        return Math.sqrt(x);
    }
}
```

Y controlarla desde `main`:

```java
public class Main {
    public static void main(String[] args) {

        try {
            double r = Calculadora.raiz(-5);
            System.out.println("Raíz = " + r);

        } catch (NumeroNegativoException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

***

# 📌 Resumen para examen

*   En POO, **las excepciones son objetos**.
*   Esto permite **encapsular** información del error dentro del propio objeto.
*   Gracias a esto, el código queda más limpio, claro y orientado a objetos.
*   Sí, se pueden crear **excepciones personalizadas** mediante herencia.

***
***

# 7. ✅ ¿Qué información esencial lleva *cualquier* objeto excepción en Java?

Todo objeto excepción en Java contiene **al menos tres elementos fundamentales**, que resultan extremadamente útiles cuando llegan al manejador (`catch`):

***

## ✔️ 1. **El tipo de excepción (la clase concreta)**

Ejemplos:

*   `IllegalArgumentException`
*   `NullPointerException`
*   `IOException`

Esto permite saber **qué tipo exacto de error ha ocurrido**, no solo un número genérico como en C.  
El tipo ya indica la *naturaleza* del problema.

***

## ✔️ 2. **Un mensaje descriptivo del error**

Cada excepción puede llevar un mensaje explicando qué ha pasado, por ejemplo:

```java
throw new IllegalArgumentException("El número no puede ser negativo");
```

En C tendrías que devolver un código y luego, fuera, convertirlo manualmente a un mensaje.  
En Java, el objeto excepción *ya encapsula el mensaje*.

***

## ✔️ 3. **El *stack trace* (la traza de llamadas)**

Este es el elemento clave que marca una gran diferencia frente a C.

El *stack trace* contiene:

*   qué métodos estaban en ejecución
*   en qué orden
*   en qué línea exacta del código ocurrió el error

Por ejemplo:

    java.lang.IllegalArgumentException: El número no puede ser negativo
        at Calculadora.raiz(Calculadora.java:7)
        at Main.main(Main.java:5)

Esto es **oro puro** al depurar y entender el fallo.

***

# 🧩 Comparación directa con C

| Lenguaje | ¿Qué información envía una función con error?              | ¿Ventajas / Desventajas?                                                           |
| -------- | ---------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| **C**    | Un número o código manual (ej. `-1`)                       | Muy pobre; no incluye tipo de error ni mensaje ni contexto.                        |
| **Java** | Un **objeto excepción** con: tipo, mensaje y *stack trace* | Encapsula toda la información relevante; muy útil para depurar y manejar el error. |

***

# 📌 Resumen para examen

La información esencial que trae cualquier objeto excepción en Java y que es muy útil al llegar al manejador es:

1.  **El tipo de la excepción** (la clase concreta del error).
2.  **Un mensaje descriptivo** del problema.
3.  **La traza de la pila de llamadas (*stack trace*)**, que indica dónde se produjo el error y cómo llegó hasta allí.

***
***

# 8.1 ✅ ¿Se pueden tener **más de un bloque `catch`** en Java?

**Sí.**  
Un bloque `try` puede ir seguido de **varios bloques `catch`**, cada uno destinado a capturar un tipo distinto de excepción.

Ejemplo:

```java
try {
    // código que puede lanzar varias excepciones
} catch (IOException e) {
    // manejo específico de IOException
} catch (NumberFormatException e) {
    // manejo específico de NumberFormatException
} catch (Exception e) {
    // manejo genérico
}
```

***

# 8.2 ✅ ¿Cuántos bloques `catch` se ejecutan?

**Solo se ejecuta UNO.**

Cuando ocurre una excepción:

1.  Java busca el **primer `catch` cuyo tipo coincida** con la excepción lanzada.
2.  Ejecuta **únicamente ese `catch`**.
3.  Los demás `catch` son **ignorados**.

Nunca se ejecutan dos `catch` para la misma excepción.

Esto se debe a que el manejo de excepciones debe ser **determinista**: una excepción tiene **un único manejador**.

***

# 🧩 Ejemplo aplicado

```java
try {
    double x = Calculadora.raiz(-5);
} catch (NumeroNegativoException e) {
    System.out.println("Error: número negativo");
} catch (Exception e) {
    System.out.println("Otro tipo de error");
}
```

Si `raiz(-5)` lanza `NumeroNegativoException`:

*   Se ejecuta **solo** el primer `catch`.
*   El segundo `catch` se **ignora**, aunque también podría capturarla (porque una excepción personalizada normalmente hereda de `Exception`).

***

# 📌 Resumen breve para examen

*   ✔️ **Sí**, en Java se pueden tener varios bloques `catch`.
*   ✔️ **Se ejecuta solo uno**: el primero cuyo tipo coincida con la excepción lanzada.
*   ✔️ La búsqueda es **de arriba hacia abajo**.

***
***

## 9. Si las excepciones producen rupturas en el código llamador, ¿cómo podemos garantizar que se ejecuta siempre finalmente un código necesario para cierre de ficheros, liberacion de recursos, antes de que continúe propagándose la excepción? Pon un ejemplo en Java con `finally`, tanto con `catch` como sin él.

### Respuesta


## 10. En Java, el bloque `finally` puede ir sin `catch`? ¿Se ejecuta siempre tanto si ocurre como si no ocurre una excepción? ¿Y si hay un `return` en medio del `try`?

### Respuesta


## 11. En Java, qué son las excepciones **"controladas"** y las **"no controladas"**? ¿Qué papel juega `RuntimeException`? Pon un ejemplo de excepciones típicas controladas y no controladas que incluso nosotros mismos podríamos usar. Haz dos listas con 3 o 4 ejemplos de situación donde se suele preferir una excepción controlada y donde se suele preferir una excepción no controlada.

### Respuesta


## 12. ¿Qué es y para qué se usa `throws`? ¿Por qué es alternativa a capturar una excepción controlada?

### Respuesta


## 13. Pon un ejemplo en Java de firma de método que incluya `throws`, de una función que abre un fichero pero que declara que no le interesa menejar la excepción de si el fichero no existe, sino que se propague hacia arriba. Eso sí, acuérdate del `finally`.

### Respuesta


## 14. ¿Podemos poner en `throws` excepciones no controladas, como `RuntimeException`? ¿Debería el método llamador entonces poner `try-catch` en ese caso? ¿Qué sentido tendría?

### Respuesta


## 15. ¿Cuándo se recomienda usar excepciones controladas, como `IOException`, y cuándo no controladas como `IllegalArgumentException`? ¿Existen en todos los lenguajes ambas opciones? En los que sólo existe una opción, ¿cuál es la más habitual?

### Respuesta


## 16. ¿Tiene sentido lanzar excepciones dentro del `catch`? ¿Se puede relanzar la misma excepción capturada? ¿Cuándo tendría sentido hacer esto último? Pon ejemplos de ambos casos.

### Respuesta


## 17. ¿En qué consiste que una excepción sea la **"causa"** de otra excepción? Pon un ejemplo en Java, donde capturemos una excepción de bajo nivel y la encapsulemos en otra personalizada de alto nivel. Cuando una excepción sale por pantalla y tiene una causa, ¿se ve?

### Respuesta

