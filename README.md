# **Programacion Orientada a Objetos**

- [**Programacion Orientada a Objetos**](#programacion-orientada-a-objetos)
  - [**Objetos**](#objetos)
  - [**Bloques de construcción de POO**](#bloques-de-construcción-de-poo)
    - [**Encapsulamiento:**](#encapsulamiento)
      - [Tell, dont ask](#tell-dont-ask)
    - [**Relaciones entre Objetos:**](#relaciones-entre-objetos)
      - [**Dendencia y Asociacion:**](#dendencia-y-asociacion)
      - [**Relaciones entre clases:**](#relaciones-entre-clases)
        - [**Herencia:**](#herencia)
        - [**Clases Abstractas:**](#clases-abstractas)
        - [**Metodo Abstracto:**](#metodo-abstracto)
  - [Diseño por Contrato](#diseño-por-contrato)
    - [Firmas de Metodos](#firmas-de-metodos)
    - [Precondiciones](#precondiciones)
      - [Excepciones](#excepciones)
    - [Postcondiciones](#postcondiciones)
    - [Invariantes](#invariantes)
    - [El procedimiento del diseño por contrato](#el-procedimiento-del-diseño-por-contrato)
  - [SOLID](#solid)
  - [Implementaciones de POO](#implementaciones-de-poo)
    - [Implementacion de Herencia:](#implementacion-de-herencia)
    - [Implementacion de Metodos y Clases Abstractas](#implementacion-de-metodos-y-clases-abstractas)
    - [Implementacion de Testing](#implementacion-de-testing)
      - [SUnit](#sunit)

La programación orientada a objetos (POO) es un paradigma de programación que se basa en el concepto de clases y objetos . Se utiliza para estructurar un programa de software en piezas simples y reutilizables de planos de código (generalmente llamadas clases), que se utilizan para crear instancias individuales de objetos.

La POO plantea los siguientes 3 pasos para resolver un problema:

1. Encontrar objetos.
    1. Seria encontrar las entidades del domino, una buena idea es empezar por los sustantivos que surgen del propio enunciado del problema  
2. Determinar cómo deben interactuar los objetos.
3. Implementar el comportamiento de los objetos.

## **Objetos**

Una entidad que existe en tiempo de ejecución y que tiene comportamiento. Son capaces de recibir y mandar mensajes.

Los objetos tienen:

- **Identidad:** es lo que distingue un objeto de otro.
- **Estado:** la situacion en que se encuntra un objeto. El estado de un objeto puede cambiar a traves del tiempo.
  - Los cambios de estado suelen ser por un mensaje recibido por el objeto
  - Generalmente privado, o salvo que se necesite que se pueda mediante un mensaje
- **Comportamiento:** El comportamiento de un objeto está compuesto por las respuestas a los mensajes que recibe un objeto, que a su vez pueden provocar:
  - Un cambio de estado en el objeto receptor del mensaje. 
  - La devolución del estado de un objeto, en su totalidad o parcialmente.
  - El envío de un mensaje desde el objeto receptor a otro objeto (delegación).

## **Bloques de construcción de POO**

- **Delegacion:** Cuando un objeto, para responder un mensaje, envía mensajesa otros objetos, decimos que delega ese comportamiento en otros objetos.
- **Mensaje:** cliente y receptor: Un mensaje es la interacción entre un objeto que pide un servicio y otro que lo brinda.
  - El objeto que envía el mensaje se llama **objeto cliente** y quien recibe el mensaje se llama
- **Metodo:** Llamamos método a la implementación de la respuesta de un objeto a un mensaje.
- **Atributo:** variable interna del objeto que sirve para almacenar parte del estado del mismo.

### **Encapsulamiento:**

Cada objeto es responsable de responder a los mensajes que recibe, sin que quien le envía el mensaje tenga que saber cómo lo hace. Esto es lo que llamamos encapsulamiento.

Las razones de ser del encapsulamiento son varias, entre ellas:

- Puede haber implementaciones alternativas para una misma operación. 
- En el futuro, podemos cambiar una implementación por otra, ambas correctas, sin afectar al cliente que utiliza el servicio.

#### Tell, dont ask

Un colorario del encapsulamiento que que implica que los objetos deben manejar su propio comportamiento, sin que nosotros manipulemos su estado desde afuera.

### **Relaciones entre Objetos:**

#### **Dendencia y Asociacion:**

Un objeto depende de otro cuando debe conocerlo para poder enviarle un mensaje.Todo objeto cliente depende de su servidor. La dependencia puede venir dada de tres maneras:

- Porque el objeto servidor se envía como argumento.
- Porque el objeto servidor se obtiene como respuesta al envío de un mensaje a otro objeto.
- Porque el objeto cliente tiene una referencia al servidor.

La asociacion es una forma de dependencia en la que el objeto cliente tiene almacenada una referencia al objeto servidor.

#### **Relaciones entre clases:**

En los lenguajes con clases, las relaciones entre objetos nos llevan a relaciones entre clases.

##### **Herencia:**

La herencia es una relación entre clases, por la cual se define que una clase puede ser un caso particular de otra. A la clase más general la llamamos madre y a la más patricular hija. Cuando hay herencia, todas las instancias de la clase hija son también instancias de la clase madre.

- **Programamos por diferencia:** cuando indicamos que parte de la implementación de un objeto está definida en otro objeto, y por lo tanto sólo implementamos las diferencias específicas.
- **Redefinicion:** Los lenguajes de programación que tienen clases y herencia, permiten volver a definir métodos que ya estuvieran definidos en la clase base en sus clases derivadas
  - La redefinición existe para definir un mismo comportamiento en una clase derivada, para el mismo mensaje de la clase base. Por lo tanto, la semántica o significado del mensaje se debe mantener. Si así no fuera, conviene definir un método diferente, con nombre diferente.

##### **Clases Abstractas:**

Una clase es abstracta cuando no puede tener instancias en forma directa, habitualmente debido a que sus clases descendientes cubren todos los casos posibles.

Cuando queramos indicar una clase que no es abstracta (que puede tener instancias) la llamaremos clase concreta.

##### **Metodo Abstracto:**

Un método es abstracto cuando no lo implementamos en una clase, pero sí deseamos que todas las clases descendientes puedan entender el mensaje.

Cuando queramos indicar un método que no es abstracto (que tiene implementación) lo llamaremos método concreto.

## Diseño por Contrato

La idea primigenia del diseño por contrato es, entonces, que un objeto servidor brinda servicios a objetos clientes sobre la base de un contrato que ambos se comprometen a cumplir.

Esta formado por cuatro elementos fundamentales:

- firmas de métodos.
- precondiciones.
- postcondiciones.
- invariantes.

### Firmas de Metodos

Las firmas de los métodos son las que determinan cómo hacer para pedirles servicios a los objetos.

Al conjunto de las firmas de métodos se lo suele llamar interfaz o protocolo del objeto, porque es lo que permite saber qué servicios expone y cómo dialogar con él. **No confundir con la implementacion de una Interfas**

### Precondiciones

Las precondiciones expresan en qué estado debe estar el medio ambiente antes de que un objeto cliente le envíe un mensaje a un receptor.

Si una precondición no se cumple, el que no está cumpliendo el contrato es el cliente. Por lo tanto, el objeto receptor del mensaje, lo único que puede hacer es avisarle de ese incumplimiento al cliente y no seguir con la ejecución del método. Habitualmente, los lenguajes de POO tienen un mecanismo llamado excepciones.

#### Excepciones

Una excepción es un objeto que se usa para comunicar una situación excepcional desde un entorno que la detecta al ámbito desde el cual fue invocado.

Notemos que hablamos de excepciones cuando el problema no se puede resolver en un determinado contexto. La idea es que cuando surge una excepción no hay forma de continuar y se debe elevar la misma a un contexto de nivel superior para que resuelva el inconveniente

### Postcondiciones

En términos estrictos, el conjunto de postcondiciones expresa el estado en que debe quedar el medio como consecuencia de la ejecución de un método. En términos operativos, es la respuesta ante la recepción del mensaje.

El cumplimiento de las postcondiciones es responsabilidad del receptor. Si una postcondición no se cumple se debe a que el método está mal programado por quien deba implementar el objeto receptor. Por lo tanto, el cumplimiento de una postcondición se debe chequear con una Prueba Unitaria

### Invariantes

Los invariantes son condiciones que debe cumplir un objeto durante toda su existencia.

El cumplimiento de los invariantes es responsabilidad de todos los métodos de un objeto, desde su creación. De alguna manera, pueden considerarse precondiciones y postcondiciones de todos los métodos.

En general, suelen expresarse en forma de precondiciones o postcondiciones.

### El procedimiento del diseño por contrato

![Pasos deDiseño por Contrato](./Images/DisenioPorContratoDiagrama.png)

## SOLID

## Implementaciones de POO

### Implementacion de Herencia:

En smalltalk:

```smalltalk
    Error subclass: #ValorInvalido
```

En Java:

```java
    class ValorInvalido extends RuntimeException { } 
```

### Implementacion de Metodos y Clases Abstractas

En Java, la declaración de un método como abstracto que hace añadiendo la palabra abstract en su firma, y cerrando con un punto y coma en vez de un bloque de código. He aquí un ejemplo: 

```java
    public abstract void extraer (int monto); 
```

Una clase que tiene algún método abstracto debe ser abstracta, por lo que hay que agregar la palabra abstract en su encabezado, como en el ejemplo:

```java
public abstract class Cuenta { 
 … 
}
```

En Smalltalk, un método abstracto se implementa enviando un mensaje que implica que las subclases deben implementarlo, como en el ejemplo: 

```smalltalk
  extraer: monto 
    self subclassResponsibility. 
```

### Implementacion de Testing

#### SUnit

La idea de SUnit es simple, y se basa en las siguientes premisas:

- Para escribir una clase de pruebas, debemos hacer que la misma derive de la clase TestCase.
- Cada método de prueba debe poder tener cualquier nombre, a condición de que empiece con la palabra test.
- Al escribir cada método, nos podemos ayudar con el comportamiento provisto en TestCase, que incluye algunos métodos de nombres assert, deny, should, etc.
- SUnit se ocupa de que todos los métodos test escritos hasta el momento en una clase derivada de TestCase se puedan ejecutar a la vez.

**Ejemplo:**

Al trabajar con SUnit, lo que debemos hacer es escribir una clase de pruebas, que llamaremos PruebasCuentas, derivada de la clase TestCase.

```smalltalk
    TestCase subclass: #PruebasX
```

Con todo esto definimos los métodos de la clase PruebasX:

```smalltalk
    test01SumarUnoMasUnoDaDos
        self assert: (1+1) equals: 2
```

```smalltalk
    test02UnoMasUnoNoDaTres
        self deny: (1+1=3)
```

```smalltalk
    test03DividirPorCeroDebeLanzarExcepcion
        self should: [1/0] raise: ZeroDivide
```

Diagrama de como Funciona:

![Diagrama de Clase de SUnit](./Images/ClassDiagramPruebasSUnit.png)

![Diagrama de Secuencia de ejecucion de Pruebas SUnit](./Images/SeqDiagramDeEjecucionDePruebasSUnit.png)
