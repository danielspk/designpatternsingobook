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

**Contenido en desarrollo.**

## Colaboradores

**Contenido en desarrollo.**

## Implementación

**Contenido en desarrollo.**

## Código de ejemplo

**Contenido en desarrollo.**

## Patrones relacionados

**Contenido en desarrollo.**

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Observer_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
