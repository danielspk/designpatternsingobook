# Patrón State

## Propósito

Permite que una estructura con estado modifique su comportamiento cada vez que cambie su estado interno. Parecerá que cambia la estructura de la estructura con estado.

## También conocido como

_Objects for states_ (Estados como Objetos)

## Aplicabilidad

Úsese el patrón State en cualquiera de los siguientes dos casos:
* El comportamiento de una estructura con estado depende de su estado, y debe cambiar en tiempo de ejecución dependiendo de ese estado.
* Las operaciones tienen largas sentencias condicionales con múltiples ramas que dependen del estado de la estructura con estado. Ese estado se suele representar por una o más constantes enumeradas. Muchas veces son varias las operaciones que contienen esta misma organización condicional. el patrón state pone cada rama de la condición en una estructura aparte. Esto nos permite tratar al estado de la estructura con estado como una estructura con estado de pleno derecho que puede variar independientemente de otras estructuras con estado.

## Estructura

![](/assets/uml/state.png)

## Participantes

* **Contexto:**
  * define la interfaz de interés para los clientes.
  * mantiene una instancia de una sub estructura de EstadoConcreto que define el estado actual.
* **Estado:**
  * define una interfaz para encapsular el comportamiento asociado con un determinado estado del Contexto.
* **Sub estructuras de EstadoConcreto:**
  * cada sub estructura implementa un comportamiento asociado con un estado del Contexto.

## Colaboradores

* Contexto delega las peticiones que dependen del estado en la estructura con estado EstadoConcreto actual.
* Un contexto puede pasarse a sí mismo como parámetro para que la estructura con estado Estado maneje la petición. Esto permite a la estructura con estado Estado acceder al contexto si fuera necesario.
* Contexto es la interfaz principal para los clientes. Los clientes pueden configurar un contexto con estructuras con estado Estado. Una vez que está configurado el contexto, sus clientes ya no tienen que tratar con las estructuras con estado Estado directamente.
* Cualquiera de las sub estructuras de Contexto o de EstadoConcreto pueden decidir qué estado sigue a otro y  bajo qué circunstancias.

## Implementación

**Contenido en desarrollo.** a) analizar otras alternativas, b) implicancias con concurrencia.

## Código de ejemplo

**Contenido en desarrollo.**

## Patrones relacionados

El patrón [Flyweight](/patrones/estructurales/flyweight.md) explica cuándo y cómo compartir estructuras con estado Estado.
Las estructuras con estado Estado muchas veces son [Singleton](/patrones/creacionales/singleton.md).

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _State_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
