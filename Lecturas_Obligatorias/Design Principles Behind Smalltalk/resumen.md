# Resumen de Design Principles Behind Smalltalk

El propósito del proyecto Smalltalk es proveer soporte de computación al espíritu creativo que todos llevamos dentro. Esta enfocado en dos áreas principales de investigación: un lenguaje de descripción (lenguaje de programación) que sirve de interfaz entre los modelos en la mente humana y aquellos en el hardware, y un lenguaje de interacción (interfaz al usuario) que adapte el sistema de comunicación humano a la computadora. Nuestro trabajo ha seguido un ciclo de dos a cuatro años que se puede ver como paralelo al método científico:

- Construir un programa de aplicación dentro del sistema actual (hacer una observación)
- Basado en esta experiencia, rediseñar el lenguaje (construir una teoría)
- Construir un nuevo sistema basado en el nuevo diseño (hacer una predicción que puede ser corroborada)

> **Dominio Personal:** Si un sistema es para servir al espíritu creativo, debe ser completamente entendible para un individuo solitario.

El punto aquí es que el potencial humano se manifiesta en los individuos. Para efectivizar este potencial, debemos proveer un medio que pueda ser dominado completamente por un individuo. Cualquier barrera que exista entre el usuario y alguna parte del sistema será finalmente una barrera a la expresión creativa. Cualquier parte del sistema que no pueda ser cambiada, o que no es lo suficientemente general es probablemente un origen de impedimentos. Si una parte del sistema funciona de manera diferente del resto, esa parte requiere un esfuerzo adicional para controlarla. Esa complicación añadida puede afectar el resultado final, e inhibir futuros esfuerzos en esa área. Podemos entonces inferir un principio general de diseño:

> **Buen Diseño:** Un sistema debería ser construido con un mínimo conjunto de partes no modificables; esas partes debieran ser tan generales como sea posible; y todas las partes del sistema deberían estar mantenidas en un esquema uniforme.

## Lenguaje

Al diseñar un lenguaje para ser usado con computadoras, no es necesario mirar muy lejos para buscar indicaciones útiles. Todo lo que sabemos sobre cómo la gente piensa y se comunica es aplicable.

La comunicación entre dos personas (o entre una persona y una computadora) incluye comunicación en dos niveles. La comunicación explícita incluye la información que es transmitida en determinado mensaje. La comunicación implícita incluye las suposiciones relevantes comunes a los dos seres.

> **Propósito del lenguaje:** Proveer un esquema para la comunicación.

En la interacción humana, mucho de la comunicación real se realiza por referencias a un contexto compartido, y el lenguaje humano está construido sobre estas alusiones. Con las computadoras pasa lo mismo.

> **Alcance:** El diseño de un lenguaje para usar computadoras debe tratar con modelos internos, medios externos, y con la interacción entre ellos tanto en el humano como en la computadora.

Este hecho es responsable de la dificultad de enseñar Smalltalk a gente que ve a los lenguajes de computadora en un sentido más restringido. Smalltalk no es simplemente una mejor manera de organizar procedimientos o un técnica distinta para administración de memoria.

## Objetos que se Comunican

Acá es donde el acto de referenciar entra: podemos asociar un identificador único al objeto, y, desde ese momento, sólo el mencionar al identificador es necesario para referenciar al objeto original.

> **Objetos:** Un lenguaje de computación debe soportar el concepto de "objeto" y proveer una manera uniforme de referirse a los objetos de universo.

El administrador de almacenamiento de Smalltalk provee un modelo orientado a objetos de la memoria de todo el sistema. La referenciación uniforme se obtiene simplemente asociando un entero que no se repite a cada objeto del sistema. Esta uniformidad es importante porque significa que las variables en el sistema pueden indicar valores ampliamente variados y aún así ser implementadas como simples posiciones de memoria. Se crean objetos al evaluarse las expresiones, y pueden ser pasados de un lado a otro gracias a la referenciación uniforme, por eso no es necesaria una manera de almacenamiento en los procedimientos que los manipulan. Cuando todas las referencias a un objeto han desaparecido del sistema, el propio objeto se esfuma, y su espacio de almacenamiento es recuperado. Este comportamiento es esencial para soportar completamente la metáfora de objetos.

> **Administración del Almacenamiento:** Para ser auténticamente "Orientado a Objetos" un sistema debe proveer administración automática del almacenamiento.

Una manera de ver si un lenguaje está funcionando bien es ver si los programas parecen estar haciendo lo que hacen. Si están salpicados con instrucciones de administración del almacenamiento, entonces su modelo interno no está bien adaptado al del los humanos.

Cada objeto en Smalltalk tiene su propia vida. Esto sugiere un tercer principio para el diseño orientado a objetos:

> **Mensajes:** La computación debería ser vista como una capacidad intrínseca de los objetos que pueden ser invocados uniformemente enviándoles mensajes.

Así como los programas se ensucian si el almacenamiento de los objetos debe ser tratado explícitamente, el control en el sistema se vuelve complicado si debe ser tratado extrínsicamente.

Smalltalk provee una solución limpia: Envía el nombre de la operación deseada, juntamente con cualquier parámetro necesario, como un mensaje al número, entendiendo que el receptor es el que mejor sabe cómo realizar la operación deseada. La transmisión de mensajes es el único proceso que se hace afuera de los objetos y así es como debiera ser, ya que los mensajes viajan entre objetos. El principio de buen diseño puede ser reexpresado para lenguajes:

> **Metáfora Uniforme:** Un lenguaje debería ser diseñado alrededor de una metáfora poderosa que pueda ser aplicada uniformemente en todas las áreas.

Ejemplos de éxitos en esta área incluyen a LISP, que está construido sobre el modelo de listas enlazadas; APL, que está construido sobre el modelo de arreglos; y Smalltalk, que está construido sobre el modelo de objetos que se comunican.

## Organización

Una metáfora uniforme provee el marco en el cual se pueden construir sistemas complejos. Algunos principios de organización relacionados entre sí contribuyen a la administración exitosa de la complejidad. Para empezar

Al incrementarse la cantidad de componentes de un sistema, la probabilidad de interacción no deseada crece rápidamente. Por esto, un lenguaje de computadora debería ser diseñado para minimizar las posibilidades de esa interdependencia.

> **Modularidad:** Ningún componente en un sistema complejo debería depender de los detalles internos de ningún otro componente.

Si los sistemas de computación son para alguna vez asistir a las tareas humanas complejas, deben ser diseñados para minimizar esta interdependencia. La metáfora de envío de mensajes provee modularidad al desacoplar la intención del mensaje (incorporado en el nombre) del método usado por el receptor para realizar la intención. La información estructural es similarmente protegida porque todo acceso al estado interno de un objeto es a través de esta misma interfaz de mensajes.

La complejidad de un sistema puede muchas veces ser reducida agrupando componentes similares. Este agrupamiento es conseguido a través del tipado de datos en los lenguajes de programación convencionales, y a través de clases en Smalltalk. Una clase describe otros objetos -su estado interno, el protocolo de mensajes que reconocen, y los métodos internos para responder a esos mensajes. Los objetos así descriptos se llaman instancias de la clase. Incluso las propias clases entran en este esquema; simplemente son instancias de la clase Class, que describe el protocolo y la implementación apropiados para la descripción de los objetos:

> **Clasificación:** Un lenguaje debe proveer un medio para clasificar objetos similares, y para agregar nuevas clases de objetos en pie de igualdad con las clases centrales del sistema.

La clasificación es la objetivación de la idadidad.

Las clases son el principal mecanismo de extensión en Smalltalk. La cláusula "en pie de igualdad" es importante porque asegura que el sistema va a ser usado como fue diseñado. En cada etapa del diseño, un humano va a elegir en forma natural la representación más efectiva si el sistema la provee.

> **Polimorfismo:** Un programa sólo debería especificar el comportamiento esperado de los objetos, no su representación.

Un afirmación inferida de este principio es que un programa nunca debería declarar que cierto objeto es un SmallInteger (entero chico) o un LargeInteger (entero grande), sino sólo que responde al protocolo de los enteros. Esta descripción genérica es crucial para los modelos del mundo real.

Considera una simulación de tránsito automotor. Muchos procedimientos en este sistema se referirán a los diversos vehículos involucrados. Supón que uno quisiera agregar, por ejemplo, un camión barrecalles. Una cantidad substancial de computación (por recompilación) y posibles errores estarían involucrados para hacer esta simple extensión si el código dependiera de los objetos que manipula. La interfaz de mensajes establece un marco ideal para esta extensión. Dado que los camiones barrecalles soportan el mismo protocolo que los demás vehículos, no hacen falta cambios para incluirlos en la simulación.

> **Factorización:** Cada componente independiente de un sistema sólo debería aparecer en un sólo lugar.

Hay muchas razones para este principio:

1. Ahorra tiempo, esfuerzo y espacio si los agregados al sistema sólo necesitan hacerse en un lugar.
2. Los usuarios pueden encontrar más fácilmente un componente que satisfaga una dada necesidad.
3. En la ausencia de una factorización apropiada, aparecen problemas para sincronizar cambios y para asegurar que todos los componentes interdependientes son consistentes. Puedes ver que una falla en la factorización implica una violación a la modularidad.

Smalltalk promueve diseños bien factorizados a través de la herencia. Todas las clases heredan comportamiento de su superclase. Esta herencia se desarrolla a través de clases cada vez más generales, terminando finalmente con la clase Object que describe el comportamiento mínimo de todos los objetos del sistema.La herencia ilustra una forma más pragmática de factorización:

> **Reaprovechamiento:** Cuando un sistema está bien factorizado, un gran reaprovechamiento está disponible tanto para los usuarios como para los implementadores.

Los beneficios de la estructuración para los implementadores son obvios. Para empezar, habrá menos primitivas para implementar. Por ejemplo, todos los gráficos en Smalltalk se hacen con una sola operación primitiva. Con sólo una tarea para hacer, un implementador puede aplicar su máxima atención a cada instrucción, sabiendo que cada pequeña mejora en eficiencia será amplificada en todo el sistema. Es natural preguntar qué conjunto de operaciones primitivas serán suficientes para soportar un sistema de computación entero. La respuesta a esta pregunta se llama especificación de una máquina virtual.

> **Máquina Virtual:** Una especificación de máquina virtual establece un marco para la aplicación de tecnología.

La máquina virtual de Smalltalk establece un modelo orientado a objetos para el almacenamiento, un modelo orientado a mensajes para el procesamiento, y un modelo de bitmap (mapa de bits) para el despliegue visual de información. A través del uso de microcódigo, y eventualmente hardware, la performance del sistema puede ser mejorada dramáticamente sin ningún compromiso de las otras virtudes del sistema.

## Interfaz al Usuario

Una interfaz al usuario es simplemente un lenguaje en el que la mayor parte de la comunicación es visual. Dado que la presentación visual se asimila mucho a la cultura humana establecida, la estética juega un rol muy importante en esta área. Como toda la capacidad de un sistema de computación finalmente es entregada a través de la interfaz al usuario, la flexibilidad es esencial también acá. Una condición habilitante para la flexibilidad adecuada de una interfaz al usuario puede ser enunciada como un principio orientado a objetos:

> **Principio Reactivo:** Cada componente accesible al usuario debería ser capaz de presentarse de una manera entendible para ser observado y manipulado.

Este criterio está bien soportado por el modelo de objetos que se comunican. Por definición, cada objeto provee un protocolo de mensajes apropiado para la interacción. Este protocolo es esencialmente un microlenguaje particular para sólo ese tipo de objeto. Al nivel de la interfaz al usuario, el lenguaje apropiado para cada objeto en la pantalla es presentado visualmente (como texto, menúes, imágenes) y percibido a través de la actividad del teclado y el uso de un dispositivo apuntador.

Debería notarse que los sistemas operativos parecen violar este principio. Aquí el programador debe alejarse de un marco de descripción que de otra manera es consistente, dejar cualquier contexto ya construido, y enfrentarse con un entorno completamente distinto y usualmente muy primitivo. Esto no tiene por qué ser así:

> **Sistema Operativo:** Un sistema operativo es una colección de cosas que no encajan dentro de un lenguaje. No debería existir.

Aquí hay algunos ejemplos de componentes de sistemas operativos convencionales que han sido incorporados naturalmente al lenguaje Smalltalk:

- Administración del Almacenamiento - Enteramente automático. Los objetos son creados por un mensaje a su clase y destruidos cuando no nadie los referencie.
- Sistema de Archivos - Está incorporado al esquema usual a través de objetos como Files y Directories con protocolos de mensajes que soportan el acceso a archivos.
- Manejo de la Pantalla - La pantalla es simplemente una instancia de la clase Form (figura), que es continuamente visible, y los mensajes de manipulación gráfica definidos en esa clase se usan para cambiar la imagen visible.
- Entrada del Teclado - Los dispositivos de entrada del usuario se modelan similarmente como objetos con mensajes apropiados para determinar su estado o leer la su historia como una secuencia de eventos.
- Acceso a Subsistemas - Los subsistemas se incorporan naturalmente como objetos independientes dentro de Smalltalk: aquí pueden usar el amplio universo de descripción existente, y aquellos que involucran interacción con el usuario pueden participar como componentes de la interfaz al usuario.
- Debugger - El estado del procesador de Smalltalk es accesible como una instancia de la clase Process que es dueña de una cadena de stacks. El debugger es sólo un subsistema de Smalltalk que tiene acceso a manipular el estado de un proceso suspendido. Es de notar que casi el único error de tiempo de ejecución que puede ocurrir en Smalltalk es que un mensaje no sea entendido por su receptor.

## Trabajo futuro

> **Selección Natural:** Los lenguajes y sistemas que son de buen diseño persistirán, sólo para ser reemplazados por otros mejores.
