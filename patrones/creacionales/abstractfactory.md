# Patrón Abstract Factory

## Propósito

Proporciona una interfaz para crear familias de estructuras con estado relacionadas o que dependan entre sí, sin especificar sus estructuras concretas.

## También conocido como

_Kit_

## Aplicabilidad

Úsese el patrón Abstract Factory cuando:
* un sistema debe ser independiente de cómo se crean, componen y representan sus productos.
* un sistema debe ser configurado con una familia de productos de entre varias.
* una familia de estructuras con estado relacionadas esta diseñada para ser usada conjuntamente, y es necesario hacer cumplir esta restricción.
* quiere proporcionar una biblioteca de estructuras de productos, y sólo quiere revelar sus interfaces, no sus implementaciones.

## Estructura

![](/assets/uml/abstractfactory.png)

## Participantes

* **FabricaAbstracta:**
  * declara una interfaz para operaciones que crean estructuras con estado producto abstractas.
* **FabricaConcreta:**
  * implementa las operaciones para crear estructuras con estado producto concretos.
* **ProductoAbstracto:**
  * declara una interfaz para un tipo de estructura con estado producto.
* **ProductoConcreto:**
  * define una estructura con estado producto para que sea creado por la fábrica correspondiente.
  * implementa la interfaz ProductoAbstracto.
* **Cliente:**
  * sólo usa interfaces declaradas por las estructuras FabricaAbstracta y ProductoAbstracto.

## Colaboradores

* Normalmente sólo se crea una única instancia de una estructura FabricaConcreta en tiempo de ejecución. Esta fábrica concreta crea estructuras con estado producto que tienen una determinada implementación.
* FabricaAbstracta delega la creación de estructuras con estado producto en su sub estructura FabricaConcreta.

## Implementación

**Contenido en desarrollo.** a) analizar otras alternativas, b) implicancias con concurrencia.

## Código de ejemplo

**Contenido en desarrollo.**

## Patrones relacionados

Las estructuras FabricaAbstracta suelen implementarse con métodos de fabricación (patrón [Factory Method](/patrones/creacionales/factorymethod.md)), pero también se pueden implementar usando [Prototype](/patrones/creacionales/prototype.md).
Una fábrica concreta suele ser un [Singleton](/patrones/creacionales/singleton.md).

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Abstract Factory_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
