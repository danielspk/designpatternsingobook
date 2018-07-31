# Patrón Visitor

## Propósito

Representa una operación sobre los elementos de una organización de estructuras con estado. Permite definir una nueva operación sin cambiar las estructuras de los elementos sobre los que opera.

## Aplicabilidad

Úsese el patrón Visitor cuando

* una organización de estructuras con estado contiene muchas clases de estructuras con estado con diferentes interfaces, y queremos realizar operaciones sobre esos elementos que dependen de su estructura concreta.
* se necesitan realizar muchas operaciones distintas y no relacionadas sobre estructuras con estado de una organización de estructuras con estado, y queremos evitar "contaminar" sus estructuras con dichas operaciones. El patrón Visitor permite mantener juntas operaciones relacionadas definiéndolas en una estructura. Cuando la organización de estructuras con estado es compartida por varias aplicaciones, el patrón Visitor permite poner operaciones sólo en aquellas aplicaciones que las necesiten.
* las estructuras que definen la organización de estructuras con estado rara vez cambian, pero muchas veces queremos definir nuevas operaciones sobre la organización. Cambiar las estructuras de la organización de estructuras con estado requiere redefinir la interfaz para todos los visitantes, lo que es potencialmente costoso. Si las estructuras de la organización cambian con frecuencia, probablemente sea mejor definir las operaciones en las propias estructuras.

##### Nota:
> "Estructura de Objeto" es sinónimo de "organización de estructuras con estado" para ésta publicación.

## Estructura

![](/assets/uml/visitor.png)

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
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Visitor_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
