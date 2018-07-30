# Patrón Iterator

## Propósito

Proporciona un modo de acceder secuencialmente a los elementos de una estructura con estado agregada sin exponer su representación interna.

## También conocido como

_Cursor_

## Aplicabilidad

Úsese el patrón Iterator

* para acceder al contenido de una estructura con estado agregada sin exponer su representación interna.
* para permitir varios recorridos sobre estructuras con estado agregadas.
* para proporcionar una interfaz uniforme para recorrer diferentes estructuras agregadas (es decir, para permitir la iteración polimórfica).

## Estructura

![](/assets/uml/iterator.png)

## Participantes

* **Iterador:**
  * define una interfaz para recorrer los elementos y acceder a ellos.
* **IteradorConcreto:**
  * implementa la interfaz Iterador.
  * mantiene la posición actual en el recorrido del agregado.
* **Agregado:**
  * define una interfaz para crear una estructura con estado Iterador.
* **AgregadoConcreto:**
  * implementa la interfaz de creación de Iterador para devolver una instancia del IteradorConcreto apropiado.

## Colaboradores

Un IteradorConcreto sabe cúal es la estructura con estado del agregado y puede calcular la estructura con estado siguiente en el recorrido.

## Implementación

**Contenido en desarrollo.** a) analizar otras alternativas, b) implicancias con concurrencia.

## Código de ejemplo

**Contenido en desarrollo.**

## Patrones relacionados

[Composite](/patrones/estructurales/composite.md): los iteradores suelen aplicarse a estructuras recursivas como los Composite.
[Factory Method](/patrones/creacionales/factorymethod.md): los iteradores polimórficos se basan en funciones de fabricación para crear instancias de las subestructuras apropiadas de Iterator.
El patrón [Memento](/patrones/comportamiento/memento.md) suele usarse conjuntamente con el patrón Iterator. Un iterador puede usar un memento para representar el estado de una iteración. El iterador almacena el memento internamente.

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Iterator_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
