<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Encapsulación". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# **TEMA 2. Encapsulación**

# 1. Encapsulación y ocultación de información en POO

En **Programación Orientada a Objetos**, la **encapsulación** y la **ocultación de información** buscan:

## ✅ **Encapsulación**

Agrupar datos (*atributos*) y comportamientos (*métodos*) dentro de una misma unidad llamada **clase**, de manera que el objeto controle cómo se accede y modifica su estado interno.

## ✅ **Ocultación de información (information hiding)**

Restringir el acceso directo a los datos internos del objeto, exponiendo solo lo necesario a través de métodos públicos (getters, setters, operaciones).  
Esto permite **proteger el estado interno** del objeto frente a usos incorrectos o no deseados.

***

## **Ventajas de la ocultación de información**

1.  **Mayor seguridad y control**  
    Evita que otras partes del programa modifiquen los atributos de forma incorrecta.

2.  **Permite mantener invariantes internas**  
    El objeto puede validar los datos antes de aceptarlos.

3.  **Reduce el acoplamiento**  
    El exterior solo conoce la interfaz pública, no los detalles internos.

4.  **Facilita la modificación del código**  
    Los atributos internos pueden cambiar sin afectar a quienes usan la clase.

5.  **Mejor mantenimiento y legibilidad**  
    La interfaz pública suele ser más simple y clara que la implementación interna.

***
***

# **2. Interfaz pública de un objeto o clase en POO**

La **interfaz pública** es el **conjunto de métodos y atributos accesibles desde fuera de la clase**.  
Es decir, es *lo que un objeto ofrece al exterior* para que otros objetos o partes del programa interactúen con él.

Normalmente incluye:

*   Métodos públicos (`public`)
*   Atributos públicos (aunque en buen diseño suelen evitarse)
*   Constantes públicas
*   Cualquier elemento visible desde fuera de la clase

La interfaz pública define **qué puede hacer** un objeto, no **cómo lo hace** internamente.

***

## **Relación con la ocultación de información**

La **ocultación de información** consiste en mantener los detalles internos de la clase (atributos, lógica interna) **ocultos**, normalmente usando modificadores como `private` o `protected`.

Esto conecta directamente con la interfaz pública porque:

*   La **interfaz pública** expone **solo lo necesario** para usar el objeto.
*   La **ocultación** protege la implementación interna para que no pueda ser manipulada directamente.
*   Así, otros objetos solo pueden interactuar a través de la **interfaz pública**, no con los detalles internos.

### En otras palabras:

> **La interfaz pública es la puerta controlada de acceso;  
> la ocultación de información es la pared que protege todo lo que hay detrás.**

***
***

## 3. Brevemente: ¿Por qué hay que ser conscientes y diseñar con cuidado la **interfaz pública** de una clase? ¿Es fácil cambiarla?

### Respuesta


## 4. ¿Qué son las **invariantes de clase** y por qué la ocultación de información nos ayuda?

### Respuesta


## 5. Pon un ejemplo de una clase `Punto` en `Java`, con dos coordenadas, `x` e `y`, de tipo `double`, con un método `calcularDistanciaAOrigen`, y que haga uso de la ocultación de información. ¿Cuál es la interfaz pública de la clase `Punto`? ¿Qué significa `public` y `private`?

### Respuesta


## 6. En Java, ¿A quiénes se pueden aplicar los modificadores `public` o `private`?

### Respuesta


## 7. En POO, la visibilidad puede ser pública o privada, pero ¿existen más tipos de visibilidad? ¿Qué ocurre en Java? ¿Y en otros lenguajes?

### Respuesta


## 8. Responde: Los miembros de instancia privados de un objeto están ocultos para (a) otras clases o (b) otras instancias, aunque sean de la misma clase. Pon un ejemplo añadiendo un método `calcularDistanciaAPunto(Punto otro)` y explica la respuesta.

### Respuesta


## 9. ¿Qué son los métodos "getter" y "setter" en los lenguajes orientados a objetos?

### Respuesta


## 10. Cuando nos referimos a que la ocultación de información mejora la "seguridad" del programa, ¿nos referimos a que no pueda ser "hackeado"?

### Respuesta


## 11. ¿Qué diferencia hay entre **miembro de instancia** y **miembro de clase**? ¿Los miembros de clase también se pueden ocultar?

### Respuesta


## 12. Brevemente: ¿Tiene sentido que los constructores sean privados?

### Respuesta


## 13. ¿Cómo se indican los **miembros de clase** en Java? Pon un ejemplo, en la clase `Punto` definida anteriormente, para que incluya miembros de clase que permitan saber cuáles son los valores `x` e `y` máximos que se han establecido en todos los puntos que se hayan creado hasta el momento.

### Respuesta


## 14. Como sería un método factoría dentro de la clase `Punto` para construir un `Punto` a partir de dos coordenadas, pero que las redondee al entero más cercano. Escribe sólo el código del método, no toda la clase ¿Has usado `static`? 

### Respuesta


## 15. Cambia la implementación de `Punto`. En vez de dos `double`, emplea un array interno de dos posiciones, intentando no modificar la interfaz pública de la clase.

### Respuesta


## 16. Si un atributo va a tener un método "getter" y "setter" públicos, ¿no es mejor declararlo público? ¿Cuál es la convención más habitual sobre los atributos, que sean públicos o privados? ¿Tiene esto algo que ver con las "invariantes de clase"?

### Respuesta


## 17. ¿Qué significa que una clase sea **inmutable**? ¿qué es un método modificador? ¿Un método modificador es siempre un "setter"? ¿Tiene ventajas que una clase sea inmutable?

### Respuesta


## 18. ¿Es recomendable incluir métodos "setter" siempre y como convención?

### Respuesta


## 19. ¿La clase `String` en Java es mutable o inmutable? ¿Qué ocurre al concatenar dos cadenas? ¿Qué debemos hacer si vamos a hacer una operación que implique concatenar muchas veces para construir paso a paso una cadena muy larga?

### Respuesta


## 20. En POO ¿Cómo se comparan objetos de una misma clase? ¿Por su contenido o por su identidad? ¿Qué es el método equals en Java? ¿Qué hace por defecto? ¿Cómo se deben comparar dos cadenas en Java? 

### Respuesta


## 21. ¿Qué son las clases "wrapper" en un lenguaje de programación orientado a objetos? ¿Cómo se hace? ¿Es un proceso automático? ¿Qué ventajas tienen? ¿Todos los lenguajes orientados a objetos tienen tipos primitivos y necesitan wrappers? 

### Respuesta


## 22. ¿En POO qué es un **tipo de dato enumerado**? ¿En Java, un tipo de dato enumerado es una clase? ¿Qué ventajas tienen en términos de encapsulación los enumerados en Java?

### Respuesta


## 23. Crea un tipo enumerado en Java que se llame `Mes`, con doce posibles instancias y que además proporcione métodos para obtener cuántos días tiene ese mes, el ordinal de ese mes en el año (1-12), empleando atributos privados y constructores del tipo enumerado. Añade además cuatro métodos para devolver si ese mes tiene algunos días de invierno, primavera, verano u otoño, indicando con un booleano el hemisferio (norte o sur, parámetro `enHemisferioNorte`). Es decir: `esDePrimavera(boolean esHemisferioNorte)`, `esDeVerano(boolean esHemisferioNorte)`, `esDeOtoño(boolean esHemisferioNorte)`, `esDeInvierno(boolean esHemisferioNorte)`

### Respuesta