# 23 Patrones de Diseño GoF

### ¿Qué es Gof?

En esta publicación se utilizarán los 23 patrones de diseño del libro "Patrones de Diseño: Elementos de software orientado a objetos reutilizable" [\[29\]](/recursos.md) escrito por Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides.  
El término _GoF_ proviene de los autores del libro que son conocidos por la comunidad como _Gang of Four_ \(_La Banda de los Cuatro_\).

### ¿Es posible implementar los patrones de diseño en Go?

En el libro "Patrones de Diseño" [\[29\]](/recursos.md) los autores hacen la siguiente aclaración respecto de los lenguajes utilizados para documentar los 23 patrones: "Aunque los patrones describen diseños orientados a objetos, están basados en soluciones prácticas que han sido implementadas en los lenguajes de programación orientados a objetos más usuales, como _Smalltalk_ y _C++_, en vez de mediante lenguajes procedimentales \(_Pascal_, _C_, _Ada_\) u otros lenguajes orientados a objetos más dinámicos \(_CLOS_, _Dylan_, _Self_\). Nosotros hemos elegido _Smalltalk_ y _C++_ por una cuestión pragmática: nuestra experiencia diaria ha sido con estos lenguajes, y éstos cada vez son más populares". "La elección del lenguaje de programación es importante, ya que influye en el punto de vista. Nuestros patrones presuponen características de _Smalltalk_ y _C++_, y esa elección determina lo que puede implementarse o no fácilmente. Si hubiéramos supuesto lenguajes procedimentales, tal vez, hubiéramos incluido patrones llamados 'Herencia', 'Encapsulación' y 'Polimorfismo'. De manera similar, algunos de nuestros patrones están incluidos directamente en lenguajes orientados a objetos menos corrientes. _CLOS_, por ejemplo, tiene multi-métodos que reducen la necesidad de patrones como _Visitor_. De hecho, hay suficientes diferencias entre _Smalltalk_ y _C++_ como para que algunos patrones puedan expresarse más facilmente en un lenguaje que en otro \(por ejemplo, el _Iterator_\)"

> Es importante remarcar que este libro fue publicado en 1994 - \(Java 1 recién se publicó en 1996\)

También es importante entender que este trabajo intenta demostrar cómo pueden aplicarse los patrones de diseño en _Go_, aunque no es necesariamente imperativo su uso ni se lo promueve. Tal como exponen los autores, cada lenguaje tiene sus particularidades y en necesario entender el real problema a resolver, y no intentar adaptar formas de trabajo de un lenguaje a otro, sino entender esas particularidades que hacen diferente a un lenguaje respecto del otro para potenciar sus características.

A pesar de que parezca desalentador lo anteriormente dicho es importante remarcarlo. Un error muy común cuando aprendemos algo nuevo es querer utilizarlo en cualquier contexto, sin analizar realmente la conveniencia de su uso. Cuando uno aprende un patrón de diseño nuevo se ve tentado a utilizarlo. **Los patrones de diseño resuelven problemas conocidos, y sólo deben usarse si se está en precencia de un problema apropiado**.

Un error que veo muy seguido es la adaptación de un patrón de un lenguaje a otro \(como si se tratase de una traducción literal\) cuando en realidad no se tienen en cuenta sus características específicas, que hacen a cada lenguaje de programación único, ni el objetivo que intenta resolver el patrón de diseño. **Intentaré no caer yo mismo en este error**.

> _En Go _pueden aprovecharse algunas de sus características particulares para implementar también otros tipos de patrones distintos a los del libro "Patrones de Diseño" [\[29\]](/recursos.md). Por ejemplo hay una gran cantidad de patrones de concurrencia

### ¿Cómo se clasifican los patrones?

Los patrones de diseño se organizan en tres familias de acuerdo a su propósito:

* **Creacionales:** tienen que ver con el proceso de creación de objetos.
* **Estructurales:** tratan con la composición de clases u objetos.
* **Comportamiento:** caracterizan el modo en el que las clases y objetos interactúan y se reparten responsabilidades.

Los autores del libro "Patrones de Diseño" [\[29\]](/recursos.md), también proponen otro criterio de clasificacion denominado _ambito_: "especifíca si el patrón se aplica principalmente a clases o a objetos. Los patrones de clases se ocupan de relaciones entre las clases y sus subclases. Esras relaciones se establecen a través de la herencia, de modo que son relaciones estáticas - fijadas en tiempo de compilación -. Los patrones de objetos tratan con las relaciones entre objetos, que pueden cambiarse en tiempo de ejecución y son más dinámicas".

> Al no existir en _Go_ ni clases, ni objetos, ni herencia, la implementación de los patrones se verán muy diferentes. El desafío de esta publicación es respetar el propósito de cada patrón y su posible implementación en _Go_ en base a las características particulares del lenguaje.

## Catálogo de patrones

![](/assets/gamma/tabla1-1.png)

> "Patrones de Diseño" - Tabla 1.1 - Patrones de diseño - [\[29\]](/recursos.md)

### ¿Cómo se documenta un patrón?

Los autores del libro "Patrones de Diseño" [\[29\]](/recursos.md) utilizan la siguiente plantilla para especificar un Patrón.

| Sección | Detalle |
| --- | --- |
| **Nombre del patrón y clasificación** | El nombre del patrón transmite su esencia. El nombre es vital porque pasa a formar parte de nuestro vocabulario de diseño. Por ejemplo al decir _Singleton_ todos entenderán de que se habla, sin necesidad de explicar el objetivo y los participantes del patrón |
| **Propósito** | Es una frase breve que responde a las siguientes cuestiones: ¿Qué hace este patrón de diseño?, ¿En que se basa? ¿Cuál es el problema concreto de diseño que resuelve? |
| **También conocido como** | Son otros nombres, si existen, por los que también se conoce al patrón |
| **Motivación** | Un escenario que ilustra un problema de diseño y cómo las estructuras de clases y objetos del patrón resuelven el problema |
| **Aplicabilidad** | ¿En qué situaciones se puede aplicar el patrón de diseño? ¿Qué ejemplos hay de malos diseños que el patrón puede resolver? ¿Cómo se puede reconocer dichas situaciones? |
| **Estructura** | Una representación gráfica de las clases del patrón |
| **Participantes** | Las clases y objetos participantes en el patrón de diseño, junto con sus responsabilidades |
| **Colaboradores** | Cómo colaboran los participantes para llevar a cabo sus responsabilidades |
| **Consecuencias** | ¿Cómo consigue el patrón sus objetivos? ¿Cuáles son las ventajas, desventajas y resultados de usar el patrón? |
| **Implementación** | ¿Cúales son las dificultades, trucos o técnicas que deberíamos tener en cuenta a la hora de aplicar el patrón? ¿Hay cuestiones específicas del lenguaje? |
| **Código de ejemplo** | Fragmentos de código que muestran cómo se puede implementar el patrón |
| **Usos conocidos** | Ejemplos del patrón en sistemas reales |
| **Patrones relacionados** | ¿Qué patrones de diseño están estrechamente relacionados con éste? ¿Cuáles son las principales diferencias? ¿Con qué otros patrones debería usarse? |

En esta publicación utilizaremos la misma estructura pero con las siguientes observaciones:

* Se reemplazarán los escenarios por ejemplos más simples ya que los del libro están basados en un caso de estudio complejo \(_creación de un editor de texto_\) y no pueden ser ejecutados para el aprendizaje del lector. Los escenarios serán triviales y muy simples, la idea es orientar al lector en cómo se implementa el patrón de diseño y no en como resolver un problema puntual. Se utilizarán escenarios de alguno de los siguientes links: [\[8\]](/recursos.md), [\[40\]](/recursos.md), [\[41\]](/recursos.md), [\[42\]](/recursos.md)
* Se omitirán los usos conocidos ya que son atemporales.
* Se unificará la motivación junto con el código de ejemplo.
* Se omitirán las consecuencias ya que no es el objetivo de esta publicación el analizar las ventajas y desventajas de utilizar cada patrón de diseño.
* Se analizarán adicionalmente , sólo si corresponden, las alternativas de implementación desde el punto de vista de la concurrencia que caracteriza al lenguaje _Go_.
* Se utilizarán códigos de ejemplo en el lenguaje _Go_.
* Se utilizará UML en reemplazo de OMT. 

> Paradojicamente se utilizarán diagramas de clases de UML cuando en _Go_ no existen clases. Sin embargo, al ser UML una de las notaciones más extendidas, considero que la traducción de las _clases_ a tipos de datos de _Go_ no presentará dificultades adicionales al lector.

### Implicancias

En las explicaciones de cada patrón de diseño del libro "Patrones de Diseño" [\[29\]](/recursos.md) utilizan constantemente las palabras _objeto_ y _clase_. Parte de la comunidad asume que en _Go_ la palabra _objeto_ es válida ya que se interpreta que es sinónimo de un tipo de dato con comportamiento. Sin embargo, a fines de esta publicación cuando se requiera hablar de un _objeto_ utilizare la frase _"variable"_ \(_considero que se ajusta más al lenguaje_\).  
Para la palabra _clase_ no existe una terminología comparable, por lo que utilizaré simplemente la frase _"tipo de dato"_ o la palabra _"tipo"_.  
En cuanto a la palabra _método,_ si bien es válida en _Go_ dado que en definitiva los métodos son funciones que reciben un argumento receptor, también utilizaré la frase _"comportamiento de un tipo"_.

Dado que el libro original "Patrones de Diseño" [\[29\]](/recursos.md) utiliza OMT en lugar de UML, se hará el mayor esfuerzo en respetar la estructura original de cada patrón dado que cada lenguaje permite implementaciones levemente distintas en base a sus características particulares.  
Dicho esto se han observado pequeñas alteraciones/concesiones en implementaciones donde se reemplazan clases abstractas por interfaces y viceversa. Este tema es justamente una de las principales diferencias que pueden encontrarse en las implementaciones de un patrón de diseño GoF en _Go_, por lo que será dificultoso al lector diferenciar si una clase abstracta fue implementada como interface por _a\)_ una necesidad exclusiva dada las limitaciones del lenguaje _Go_ en sus características orientadas a objetos; o _b\)_ simplemente por una concesión válida entre los desarrolladores de otros lenguajes. Lo invito en esos caso a buscar implementaciones de código en otros lenguajes como _Java_ o _C\#_.

