# Patrón Observer

## Propósito

Define una dependencia de uno-a-muchos entre estructuras con estado, de forma que cuando una estructura con estado cambie de estado se notifique y se actualicen automáticamente todas las estructuras con estado que dependan de ellá.

## También conocido como

_Dependents_ (Dependientes), _Publish-subscribe_ (Publicar-Suscribir)

## Aplicabilidad

Úsese el patrón Onserver en cualquiera de las siguientes situaciones:
* Cuando una abstracción tiene dos aspectos y uno depende del otro. Encapsular estos aspectos en estructuras con estado separadas permite modificarlas y reutilizarlos de forma independiente.
* cuando un cambio en una estructura con estado requiere cambiar otras, y no sabemos cuántas estructuras con estado necesitan cambiarse.
* cuando una estructura con estado debería ser capaz de notificar a otras sin hacer suposiciones sobre quiénes son dichas estructuras con estado. En otras palabras, cuando no queremos que estas estructuras con estado estén fuertemente acopladas.

## Estructura

![](/assets/uml/observer.png)

## Participantes

* **Sujeto:**
  * conoce a sus observadores. Un sujeto puede ser observado por cualquier número de estructuras con estado Observador.
  * proporciona una interfaz para asignar y quitar estructuras con estado Observador.
* **Observador:**
  * define una interfaz para actualizar las estructuras con estado que deben ser notificadas ante cambios en un sujeto.
* **SujetoConcreto:**
  * almacena el estado de interés para las estructuras con estado ObservadorConcreto.
  * envía una notificación a sus observadores cuando cambia su estado.
* **ObservadorConcreto:**
  * mantiene una referencia a una estructura con estado SujetoConcreto.
  * guarda un estado que debería ser consistente con el del sujeto.
  * implementa la interfaz de actualización del Observador para mantener su estado consistente.

## Colaboradores

* SujetoConcreto notifica a sus observadores cada vez que se produce un cambio que pudiera hacer que el estado de éstos fuera inconsistente con el suyo.
* Después de ser informado de un cambio en el sujeto concreto, una estructura con estado ObservadorConcreto puede pedirle al sujeto más información. ObservadorConcreto usa esta información para sincronizar su estado con el del sujeto.

## Implementación

**Contenido en desarrollo.** a) analizar otras alternativas, b) implicancias con concurrencia.

## Código de ejemplo

**Contenido en desarrollo.**

## Patrones relacionados

[Mediator](/patrones/comportamiento/mediator.md): encapsulando semánticas de actualización complejas, se puede implementar un gestor de cambios que actue como mediador entre sujetos y observadores.
[Singleton](/patrones/creacionales/singleton.md): este gestor de cambios puede usar el patrón Singleton para que sea único y globalmente accesible.

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Observer_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
