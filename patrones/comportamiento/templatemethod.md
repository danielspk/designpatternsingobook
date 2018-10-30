# Patrón Template Method

## Propósito

Define en una operación el esqueleto de un algoritmo, delegando en las subestructuras algunos de sus pasos. Permite que las subestructuras definan ciertos pasos de un algoritmo sin cambiar su esquema.

## Aplicabilidad

El patrón Template Method debería usarse

* para implementar las partes de un algoritmo que no cambian y dejar que sean las subestructuras quienes implementen el comportamiento que puede variar.
* cuando el comportamiento repetido de varias subestructuras debería factorizarse y ser localizado en una estructura común para evitar el código duplicado.Ésta en una buena idea de "refactorizar para generalizar". En primer lugar identificamos las diferencias en el código existente y a continuación separamos dichas diferencias en nuevas operaciones. Por último, sustituimos el código que cambia por una función (comportamiento)  que llama a una de estas nuevas operaciones.
* para controlar las extensiones de las subestructuras. Podemos definir una función plantilla que llame a operaciones "de enganche" en determinados puntos, permitiendo así las extensiones sólo en esos puntos.

## Estructura

![](/assets/uml/templatemethod.png)

## Participantes

* **ClaseAbstracta:**
  * define operaciones primitivas abstractas que son definidas por las subestructuras para implementar los pasos de un algoritmo.
  * implementa una función plantilla que define el esqueleto de un algoritmo. La función plantilla llama a las operaciones primitivas así como a operaciones definidas en ClaseAbstracta o a las de otras estructuras con estado.
* **ClaseConcreta:**
  * implementa las operaciones primitivas para realizar los pasos del algoritmo específicos de las subestructuras.

## Colaboradores

ClaseConcreta se basa en ClaseAbstracta para implementar los pasos de un algoritmo que no cambian.

## Implementación

**Contenido en desarrollo.** a) analizar otras alternativas, b) implicancias con concurrencia.

## Código de ejemplo

En este ejemplo queremos cumplir con una serie de pasos formales _(método plantilla)_ para deployar diferentes aplicaciones mobile.

**Contenido en desarrollo.**

## Patrones relacionados

Los [Factory Method](/patrones/creacionales/factorymethod.md) se llaman muchas veces desde Template Method.
[Strategy](/patrones/comportamiento/strategy.md): Template Method usa la composición para modificar una parte de un algoritmo. Las estrategias usan delegación para variar el algoritmo completo.

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Template Method_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
