# Patrón Bridge

## Propósito

Desacopla una abstracción de su implementación, de modo que ambas puedan variar de forma independiente.

## También conocido como

_Handle/Body_ (Manejador/Cuerpo)

## Aplicabilidad

Úsese el patrón Bridge cuando:
* quiera evitar un enlace permanente entre una abstracción y su implementación. Por ejemplo, cuando debe seleccionarse o cambiarse la implementación en tiempo de ejecución.
* tanto las abstracciones como sus implementaciones deberían ser extensibles mediante sub estructuras. En este caso, el patrón Bridge permite combinar las diferentes abstracciones y sus implementaciones, y extenderlas independientemente.
* los cambios en la implementación de una abstracción no deberían tener impacto en los clientes; es decir, su código no tendría que ser recompilado.
* quiera compartir una implementación entre varias estructuras con estado  y este hecho deba permanecer oculto al cliente.

## Estructura

![](/assets/uml/bridge.png)

## Participantes

* **Abstraccion:**
  * define la interfaz de la abstracción.
  * mantiene una referencia a una estructura con estado de tipo Implementador.
* **AbstraccionRefinada:**
  * extiende la interfaz definida por Abstraccion.
* **Implementador:**
  * define la interfaz de las estructuras de implemetación. Esta interfaz no tiene por qué corresponderse exactamente con la de Abstracción; de hecho, ambas interfaces pueden ser muy distintas. Normalmente la interfaz Implementador sólo proporciona operaciones primitivas, y Abstraccion define operaciones de más alto nivel basadas en dichas primitivas.
* **ImplementadorConcreto:**
  * implementa la interfaz Implementador y define su implementación concreta.

## Colaboradores

Abstracción redirige las peticiones del cliente a su estructura con estado Implementador.

## Implementación

**Contenido en desarrollo.** a) analizar otras alternativas, b) implicancias con concurrencia.

## Código de ejemplo

**Contenido en desarrollo.**

## Patrones relacionados

El patrón [Abstract Factory](/patrones/creacionales/abstractfactory.md) puede Bridge.
El patrón [Adapter](/patrones/estructurales/adapter.md) está orientado a conseguir que trabajen juntas estructuras que no están relacionadas. Normalmente se aplica a sistemas que ya han sido diseñados. El patrón Bridge, por otro lado, se usa al comenzar un diseño para permitir que abstracciones e implementaciones varíen independientemente unas de otras.

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Bridge_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
