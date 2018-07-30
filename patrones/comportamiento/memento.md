# Patrón Memento

## Propósito

Representa y externaliza el estado interno de una estructura con estado sin violar la encapsulación, de forma que ésta pueda volver a dicho estado más tarde.

## También conocido como

_Token_

## Aplicabilidad

Úsese el patrón Memento cuando

* hay que guardar una instantánea del estado de una estructura con estado (o parte de ésta) para que pueda volver posteriormente a ese estado.
* o tenga una interfaz directa que para obtener el estado exponga detalles de implementación y rompa la encapsulación de la estructura con estado.

## Estructura

![](/assets/uml/memento.png)

## Participantes

* **Memento:**
  * guarda el estado interno de la estructura con estado Creador. El memento puede guardar tanta información del estado interno del creador como sea necesario a discreción del creador.
  * protege frente a accesos de otras estructuras con estado que no sean el creador. Los mementos tienen realmente dos interfaces. El Conserje va una interfaz _reducida_ del memento - sólo puede pasar el memento a otras estructuras con estado -. El Creador, por el contrario, ve una interfaz _amplia_, que le permite acceder a todos los datos necesarios para volver a su estado anterior. Idealmente, sólo el creador que produjo el memento estaría autorizado a acceder al estado interno de éste.
* **Creador:**
  * crea un memento que contiene una instantánea de su estado interno actual.
  * usa el memento para volver a su estado anterior.
* **Conserje:**
  * es responsable de guardar en lugar seguro el memento.
  * nunca examina los contenidos del memento, ni opera sobre ellos.

## Colaboradores

* Un conserje solicita un memento a un creador, lo almacena durante un tiempo y se lo devuelve a su creador. A veces el conserje no devolverá el memento a su creador, ya que el creador podría no necesitar nunca volver a su estado anterior.
* Los mementos son pasivos. Sólo el creador que creó el memento asignará o recuperará su estado.

## Implementación

**Contenido en desarrollo.** a) analizar otras alternativas, b) implicancias con concurrencia.

## Código de ejemplo

**Contenido en desarrollo.**

## Patrones relacionados

[Command](/patrones/comportamiento/command.md): las órdenes pueden usar mementos para guardar el estado de las operaciones que pueden deshacerse.
[Iterator](/patrones/comportamiento/iterator.md): puede usar mementos para la iteración.

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Memento_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
