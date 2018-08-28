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
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Bridge_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
