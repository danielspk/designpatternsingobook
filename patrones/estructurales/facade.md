# Patrón Facade

## Propósito

Proporciona una interfaz unificada para un conjunto de interfaces de un subsistema. Define una interfaz de alto nivel que hace que el subsistema sea más fácil de usar.

## Aplicabilidad

Úsese el patrón Facade cuando:
* se quiere proporcionar una interfaz simple para un subsistema complejo. Los subsistemas suelen volverse más complicados a medida que van evolucionando. La mayoría de los patrones, cuando se aplican, dan como resultados más estructuras y más pequeñas. Esto hace que el subsistema sea más reutilizable y fácil de personalizar, pero eso también lo hace más dificil de usar para aquellos clientes que no necesitan personalizarlo. Una fachada puede proporcionar, por omisión, una vista simple del subsistema que resulta adecuada para la mayoría de clientes. Sólo aquellos clientes que necesitan más personalización necesitarán ir más allá de la fachada.
* haya muchas dependencias entre los clientes y las estructuras que implementan una abstracción. Se introduce una fachada para desacoplar el subsistema de sus clientes y de otros subsistemas, promoviendo así la independencia entre subsistemas y la portabilidad.
* se requiere dividir en capas los subsistemas. Se usa una fachada para definir un punto de entrada en cada nivel del subsistema. Si éstos son dependientes, se pueden simplificar las dependencias entre ellos haciendo que se comuniquen entre sí únicamente a través de sus fachadas.

## Estructura

![](/assets/uml/facade.png)

## Participantes

* **Fachada:**
  * sabe qué estructuras del subsistema son las responsables ante una petición.
  * delega las peticiones de los clientes en las estructuras con estado apropiadas del subsistema.
* **Estructura del subsistema:**
  * implementa la funcionalidad del subsistema.
  * realizan las labores encomendadas por la estructura con estado Fachada.
  * no conocen a la fachada; es decir, no tienen referencias a ella.

## Colaboradores

* Los clientes se comunican con el subsistema enviando peticiones a la estructura con estado Fachada, la cual las reenvía a las estructuras con estado apropiadas del subsistema. Aunque son las estructuras con estado del subsistema las que realizan el trabajo real, la fachada puede tener que hacer algo de trabajo para pasar de su interfaz a las del subsistema.
* Los clientes que usan la fachada no tienen que acceder directamente a las estructuras con estado del subsistema.

## Implementación

**Contenido en desarrollo.** a) analizar otras alternativas, b) implicancias con concurrencia.

## Código de ejemplo

**Contenido en desarrollo.**

## Patrones relacionados

El patròn [Abstract Factory](/patrones/creacionales/abstractfactory.md) puede usarse para proporcionar una interfaz para crear el subsistema de estructuras con estado de forma independiente a otros subsistemas. Las fábricas abstractas también pueden ser una alternativa a las fachadas para ocultar estructuras específicas de la plataforma.
El patrón [Mediator](/patrones/comportamiento/mediator.md) es parecido al Facade en el sentido de que abstrae funcionalidad a partir de unas estructuras existentes. Sin embargo, el propósito del Mediator es abstraer cualquier comunicación entre estructuras con estado similares, a menudo centralizando la funcionalidad que no pertenece a ninguno de ellas. Los colegas del mediador sólo se preocupan de comunicarse con él y no entre ellos directamente. Por el contrario, una fachada simplemente abstrae una interfaz para las estructuras con estado del subsistema, hacíendolas más fácil de usar; no define nueva funcionalidad, y las estructuras del subsistema no saben de su existencia.
Normalmente sólo necesita una estructura con estado Fachada. Por tanto, éstas suelen implementarse como [Singlotons](/patrones/creacionales/singleton.md).

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Facade_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
