# Patrón Prototype

## Propósito

Especifica los tipos de variables a crear por medio de una creación prototípica, y crea nuevas variables copiando dicho prototipo.

## Aplicabilidad

Úsese el patrón Prototype cuando un sistema deba ser independiente de cómo se crean, se componen y se representan sus productos; y
* cuando los tipos de datos a crear sean especificos en tiempo de ejecución (por ejemplo, mediante carga dinámica); o
* para evitar construir una jerarquía de tipos de datos de fábricas paralelo a la jerarquía de tipos de datos de los productos; o
* cuando las creaciones de un tipo de dato puedan tener uno de entre sólo unos pocos estados diferentes. Puede ser más adecuado tener un número equivalente de prototipos y clonarlos, en vez de crear manualmente variables del tipo de dato cada vez con el estado apropiado.

## Estructura

![](/assets/uml/prototype.png)

## Participantes

* **Prototipo:**
  * declara la interfaz para clonarse.
* **PrototipoConcreto:**
  * implementa una operación para clonarse.
* **Cliente:**
  * crea una variable pidíendole a un prototipo que se clone.

## Colaboradores

Un cliente le pide a un prototipo que se clone.

## Implementación

No se observan impedimentos y/o modificaciones de la estructura original del patrón para su implementación en _Go_.

## Código de ejemplo

En este ejemplo queremos que un elemento químico séa capaz de clonarse a sí mismo indicando cuantas veces fue clonado.

Implementación:

```go
// Prototipo Interface
type Prototipo interface {
    Clonar() *Elemento
}

// Prototipo Concreto
type Elemento struct {
    Material string
    Copias   int
}

func (e *Elemento) Clonar() *Elemento {
    return &Elemento{
        Material: e.Material,
        Copias:   e.Copias + 1,
    }
}
```

Se puede probar la implementación del patrón de la siguiente forma:

```go
elementoA := &Elemento{"Azufre", 1}

elementoB := elementoA.Clonar()
elementoB.Material = elementoB.Material + " (fortificado)"

elementoC := elementoB.Clonar()

fmt.Printf("El elemento A es de %s y se clono %d veces\n", elementoA.Material, elementoA.Copias)
fmt.Printf("El elemento B es de %s y se clono %d veces\n", elementoB.Material, elementoB.Copias)
fmt.Printf("El elemento C es de %s y se clono %d veces\n", elementoC.Material, elementoC.Copias)
```

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/creacionales/prototype) | [Ejecutar código](https://play.golang.org/p/3OAK3-IzcTT)

## Patrones relacionados

Prototype y [Abstract Factory](/patrones/creacionales/abstractfactory.md) son patrones rivales en algunos aspectos. No obstante, también pueden usarse juntos. Una fábrica abstracta puede almacenar un conjunto de prototipos a partir de los cuales clonar y devolver variables producto.
Los diseños que hacen un uso instensivo de los patrones [Composite](/patrones/estructurales/composite.md) y [Decorator](/patrones/estructurales/decorator.md) suelen beneficiarse también del Protopype.

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Prototype_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
