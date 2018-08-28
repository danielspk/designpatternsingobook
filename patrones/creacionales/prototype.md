# Patrón Prototype

## Propósito

Especifica los tipos de estructuras con estado a crear por medio de una instancia prototípica, y crea nuevas estructuras con estado copiando dicho prototipo.

## Aplicabilidad

Úsese el patrón Prototype cuando un sistema deba ser independiente de cómo se crean, se componen y se representan sus productos; y
* cuando las estructuras a instanciar sean especificas en tiempo de ejecución (por ejemplo, mediante carga dinámica); o
* para evitar construir una jerarquía de estructuras de fábricas paralela a la jerarquía de estructuras de los productos; o
* cuando las instancias de una estructura puedan tener uno de entre sólo unos pocos estados diferentes. Puede ser más adecuado tener un número equivalente de prototipos y clonarlos, en vez de crear manualmente instancias de la estructura cada vez con el estado apropiado.

## Estructura

![](/assets/uml/prototype.png)

## Participantes

* **Prototipo:**
  * declara la interfaz para clonarse.
* **PrototipoConcreto:**
  * implementa una operación para clonarse.
* **Cliente:**
  * crea una estructura con estado pidíendole a un prototipo que se clone.

## Colaboradores

Un cliente le pide a un prototipo que se clone.

## Implementación

**Contenido en desarrollo.** a) analizar otras alternativas, b) implicancias con concurrencia.

## Código de ejemplo

**Contenido en desarrollo.**

## Patrones relacionados

Prototype y [Abstract Factory](/patrones/creacionales/abstractfactory.md) son patrones rivales en algunos aspectos. No obstante, también pueden usarse juntos. Una fábrica abstracta puede almacenar un conjunto de prototipos a partir de los cuales clonar y devolver estructuras con estado producto.
Los diseños que hacen un uso instensivo de los patrones [Composite](/patrones/estructurales/composite.md) y [Decorator](/patrones/estructurales/decorator.md) suelen beneficiarse también del Protopype.

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Prototype_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
