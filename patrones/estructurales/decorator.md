# Patrón Decorator

## Propósito

Asigna responsabilidades adicionales a una estructura con estado dinámicamente, proporcionando una alternativa flexible a la herencia _(composición)_ para extender la funcionalidad.

## También conocido como

_Wrapper_ (Envoltorio)

## Aplicabilidad

Úsese el patrón Decorator cuando:
* desea añadir estructuras con estado individuales de forma dinámica y transparente, es decir, sin afectar a otras estructuras con estado.
* pueda requerir retirar responsabilidades.
* la extensión mediante la composición no es viable.

## Estructura

![](/assets/uml/decorator.png)

## Participantes

* **Componente:**
  * define la interfaz para estructuras con estado a las que se puede añadir responsabilidades dinámicamente.
* **ComponenteConcreto:**
  * define una estructura con estado a la que se pueden añadir responsabilidades adicionales.
* **Decorador:**
  * mantiene una referencia a una estructura con estado Componente y define una interfaz que se ajusta a la interfaz del Componente.
* **DecoradorConcreto:**
  * añade responsabilidades al componente.

## Colaboradores

El Decorador redirige peticiones a su estructura con estado Componente. Opcionalmente puede realizar operaciones adicionales antes y después de reenviar la petición.

## Implementación

**Contenido en desarrollo.** a) analizar otras alternativas, b) implicancias con concurrencia.

## Código de ejemplo

**Contenido en desarrollo.**

## Patrones relacionados

[Adapter](/patrones/estructurales/adapter.md): un decorador se diferencia de un adaptador en que el decorador sólo cambia las responsabilidades de una estructura con estado, no su interfaz, mientras que un adaptador le da a una estructura con estado una interfaz completamente nueva.
[Composite](/patrones/estructurales/composite.md): se puede ver a un decorador como un composite degenerado que sólo tiene un componente. No obstante, un decorador añade responsabilidades adicionales - no está pensado para la agregación de estructuras con estado -.
[Strategy](/patrones/comportamiento/strategy.md): un decorador permite cambiar el exterior de una estructura con estado; un strategy permite cambiar su interior. Son dos formas alternativas de modificar una estructura con estado.

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Decorator_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
