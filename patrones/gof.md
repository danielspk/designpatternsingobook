# 23 Patrones de Diseño GoF

### ¿Qué es Gof?

**Contenido en desarrollo.**

### ¿Es posible implementar los patrones de diseño en Go?

En el libro "Patrones de Diseño" [\[29\]](recursos.md) Gamma hace la siguiente aclaración respecto de los lenguajes utilizados para documentar los 23 patrones: "Aunque los patrones describen diseños orientados a objetos, están basados en soluciones prácticas que han sido implementadas en los lenguajes de programación orientados a objetos más usuales, como _Smalltalk_ y _C++_, en vez de mediante lenguajes procedimentales (_Pascal_, _C_, _Ada_) u otros lenguajes orientados a objetos más dinámicos (_CLOS_, _Dylan_, _Self_). Nosotros hemos elegido _Smalltalk_ y _C++_ por una cuestión pragmática: nuestra experiencia diaria ha sido con estos lenguajes, y éstos cada vez son más populares". "La elección del lenguaje de programación es importante, ya que influye en el punto de vista. Nuestros patrones presuponen características de _Smalltalk_ y _C++_, y esa elección determina lo que puede implementarse o no fácilmente. si hubieramos supuesto lenguajes procedimentales, tal vez, hubieramos incluido patrones llamados 'Herencia', 'Encapsulación' y 'Polimorfismo'. De manera similar, algunos de nuestros patrones están incluidos directamente en lenguajes orientados a objetos menos corrientes. _CLOS_, por ejemplo, tiene multi-métodos que reducen la necesidad de patrones como _Visitor_. De hecho, hay suficientes diferencias entre _Smalltalk_ y _C++_ como para que algunos patrones puedan expresarse más facilmente en un lenguaje que en otro (por ejemplo, el _Iterator_)"

> Es importante entender que el libro de Gamma fue publicado en 1994 - (Java 1 recién se publicó en 1996)

También es importante entender que este trabajo intenta demostrar cómo pueden aplicarse los patrones de diseño en _Go_, aunque no es necesariamente imperativo su uso ni se lo promueve. Tal como expone Gamma, cada lenguaje tiene sus particularidades y en necesario entender el real problema a resolver, y no intentar adaptar formas de trabajo de un lenguaje a otro, sino entender esas particularidades que hacen diferente a un lenguaje respecto del otro, para potenciar sus características.

A pesar de que parezca desalentador lo anteriormente dicho es importante remarcarlo. Un error muy común cuando aprendemos algo nuevo es a querer utilizarlo en todos lados, sin analizar realmente la conveniencia de su uso. Cuando uno aprende un patrón de diseño nuevo se ve tentado a utilizarlo. **Los patrones de diseño resuelven problemas conocidos, y sólo deben usarse si se esta en precencia de dicho problema**.

Un error que veo muy seguido es la adaptación de un patrón de un lenguaje a otro (como si se tratase de una traducción literal) cuando en realidad no se tienen en cuenta estás características, que hacen a cada lenguaje de programación único, ni el objetivo que intenta resolver el patrón de diseño. **Intentaré no caer yo mismo en este error**.

> _Go_ por sus características particulares puede implementar también otros tipos de patrones distintos a los del libro de Gamma. Por ejemplo hay una gran cantidad de patrones de concurrencia.

### ¿Cómo se documenta un patrón?

Los autores del libro "Patrones de Diseño" [\[29\]](recursos.md) utilizan la siguiente plantilla para especificar un Patrón.

| Sección | Detalle |
| -- | -- |
| **Nombre del patrón y clasificación** | El nombre del patrón transmite su esencia. El nombre es vital porque pasa a formar parte de nuestro vocabulario de diseño. Por ejemplo al decir _Singleton_ todos entenderán de que se habla, sin necesidad de explicar el objetivo y los participantes del patrón por ejemplo |
| **Propósito** | Es una frase breve que responde a las siguientes cuestiones: ¿Qué hace este patrón de diseño?, ¿En que se basa? ¿Cuál es el problema concreto de diseño que resuelve? |
| **También conocido como** | Son otros nombres, si existen, por los que tambiñen se conoce al patrón |
| **Motivación** | Un escenario que ilustra un problema de diseño y cómo las estructuras de clases y objetos del patrón resuelven el problema |
| **Aplicabilidad** | ¿En qué situaciones se puede aplicar el patrón de diseño? ¿Qué ejemplos hay de malos diseños que el patrón puede resolver? ¿Cómo se puede reconocer dichas situaciones? |
| **Estructura** | Una representación gráfica de las clases del patrón usando una notación basada en la Técnica de Modelado de Objetos (OMT) |
| **Participantes** | Las clases y objetos participantes en el patrón de diseño, junto con sus responsabilidades |
| **Colaboradores** | Cómo colaboran los participantes para llevar a cabo sus responsabilidades |
| **Consecuencias** | ¿Cómo consigue el patrón sus objetivos? ¿Cuáles son las ventajas e inconvenientes y los resultados de usar el patrón? |
| **Implementación** | ¿Cúales son las dificultades, trucos o técnicas que deberíamos tener en cuenta a la hora de aplicar el patrón? ¿Hay cuestiones específicas del lenguaje? |
| **Código de ejemplo** | Fragmentos de código que muestran cómo se puede implementar el patrón |
| **Usos conocidos** | Ejemplos del patrón en sistemas reales |
| **Patrones relacionados** | ¿Qué patrones de diseño están estrechamente relacionados con éste? ¿Cuáles son las principales diferencias? ¿con qué otros patrones debería usarse? |

En esta publicación utilizaremos la misma estructura.

**Contenido en desarrollo.**
