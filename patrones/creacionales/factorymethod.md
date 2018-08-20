# Patrón Factory Method

## Propósito

Define una interfaz para crear una estructura con estado, pero deja que sean las sub estructuras quienes decidan qué estructura instanciar. Permite que una estructura delegue a sus sub estructuras la creación de estructuras con estado.

## También conocido como

_Virtual Constructor_ (Constructor Virtual)

## Aplicabilidad

Úsese el patrón Factory Method cuando:
* una estructura no puede prever la clase de estructuras con estado que debe crear.
* una estructura quiere que sean sus sub estructuras quienes especifiquen las estructuras con estado que ésta crea.
* las estructuras delegan la responsabilidad en una de entre varias estructuras auxiliares, y queremos localizar qué sub estructuras concreta es en la que se delega.

## Estructura

![](/assets/uml/factorymethod.png)

## Participantes

* **Producto:**
  * define la interfaz de las estructuras con estado que crea el método de fabricación.
* **ProductoConcreto:**
  * implementa la interfaz Producto.
* **Creador:**
  * declara el método de fabricación, el cual devuelve una estructura con estado de tipo Producto. También puede definir una implementación predeterminada del método de fabricación que devuelva una estructura con estado ProductoConcreto.
  * puede llamar al método de fabricación para crear una estructura con estado Producto.
* **CreadorConcreto:**
  * redefine el método de fabricación para devolver una instancia de un ProductoConcreto.

## Colaboradores

El Creador se apoya en sus sub estructuras para definir el método de fabricación de manera que éste devuelva una instancia del ProductoConcreto apropiado.

## Implementación

**Contenido en desarrollo.** a) analizar otras alternativas, b) implicancias con concurrencia.

## Código de ejemplo

**Contenido en desarrollo.**

## Patrones relacionados

El patrón [Abstract Factory](/patrones/creacionales/abstractfactory.md) suele implementarse como métodos de fabricación.
Los métodos de fabricación generalmente son llamados desde el interior de [Template Method](/patrones/comportamiento/templatemethod.md).
El [Prototype](/patrones/creacionales/prototype.md) no necesita implementar un Creador. Sin embargo, suele requerir una operación _inicializar_ en la estructura Producto. El Creador usa _inicializar_ para iniciliazar la estructura con estado, mientras que el Factory Method no requiere de dicha operación.

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Factory Method_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
