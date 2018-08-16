# Patrón Singleton

## Propósito

Gerantiza que una estructura tenga una instancia, y proporciona un punto de acceso global a ella.

## Aplicabilidad

Úsese el patrón Singleton cuando:
* deba haber exactamente una instancia de una estructura, y ésta deba ser accesible a los clientes desde un punto de acceso conocido.
* la única instancia debería ser extensible mediante otra estructura que la componga, y los clientes deberían ser capaces de usar una instancia compuesta sin modificar su código.

## Estructura

![](/assets/uml/singleton.png)

## Participantes

* **Singleton:**
  * define una operación instancia que permite que los clientes accedan a su única instancia.
  * puede ser responsable de crear su única instancia.

## Colaboradores

Los clientes acceden a la instancia de un Singleton exclusivamente a través de la operación instancia.

## Implementación

**Contenido en desarrollo.** a) analizar otras alternativas, b) implicancias con concurrencia.

## Código de ejemplo

**Contenido en desarrollo.**

## Patrones relacionados

Hay muchos patrones que pueden implementarse usando el patrón singleton. Véase [Abstract Factory](/patrones/creacionales/abstractfactory.md), [Builder](/patrones/creacionales/builder.md) y [Prototype](/patrones/creacionales/prototype.md).

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Singleton_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
