# Patrón Abstract Factory

## Propósito

Proporciona una interfaz para crear familias de variables relacionadas o que dependan entre sí, sin especificar sus tipos de datos concretos.

## También conocido como

_Kit_

## Aplicabilidad

Úsese el patrón Abstract Factory cuando:
* un sistema debe ser independiente de cómo se crean, componen y representan sus productos.
* un sistema debe ser configurado con una familia de productos de entre varias.
* una familia de variables relacionadas esta diseñada para ser usada conjuntamente, y es necesario hacer cumplir esta restricción.
* quiere proporcionar una biblioteca de tipos de datos de productos, y sólo quiere revelar sus interfaces, no sus implementaciones.

## Estructura

![](/assets/uml/abstractfactory.png)

## Participantes

* **FabricaAbstracta:**
  * declara una interfaz para operaciones que crean variables producto abstractas.
* **FabricaConcreta:**
  * implementa las operaciones para crear variables producto concretos.
* **ProductoAbstracto:**
  * declara una interfaz para un tipo de variable producto.
* **ProductoConcreto:**
  * define una variable producto para que sea creado por la fábrica correspondiente.
  * implementa la interfaz ProductoAbstracto.
* **Cliente:**
  * sólo usa interfaces declaradas por los tipos de datos FabricaAbstracta y ProductoAbstracto.

## Colaboradores

* Normalmente sólo se crea una única variable de un tipo de dato FabricaConcreta en tiempo de ejecución. Esta fábrica concreta crea variables producto que tienen una determinada implementación.
* FabricaAbstracta delega la creación de variables producto en su subtipo de dato FabricaConcreta.

## Implementación

- No se observan impedimentos y/o modificaciones de la estructura original del patrón para su implementación en _Go_.
- La _FabricaAbstracta_ y _ProductoAbstracto_ se definen como interfaces por simplificación.

## Código de ejemplo

En este ejemplo queremos comprar distintos tipos de puertas de madera (madera o metal).
Al realizar el pedido el local de venta debe encargar cada puerta a distintos fabricantes, ya que quien realiza la puerta de madera no la hace de metal y viceversa.

Implementación:

```go
// Producto Abstracto Interface
type Puerta interface {
    VerMaterial() string
}

// Producto Concreto
type PuertaMadera struct{}

func (pm *PuertaMadera) VerMaterial() string {
    return "Madera"
}

// Producto Concreto
type PuertaMetal struct{}

func (pm *PuertaMetal) VerMaterial() string {
    return "Metal"
}

// Fábrica Abstracta Interface
type FabricaPuerta interface {
    ConstruirPuerta() Puerta
}

// Fábrica Concreta
type FabricaPuertaMadera struct{}

func (fpm *FabricaPuertaMadera) ConstruirPuerta() Puerta {
    return &PuertaMadera{}
}

// Fábrica Concreta
type FabricaPuertaMetal struct{}

func (fpm *FabricaPuertaMetal) ConstruirPuerta() Puerta {
    return &PuertaMetal{}
}
```

Se puede probar la implementación del patrón de la siguiente forma:

```go
fabricaPuertaMadera := &FabricaPuertaMadera{}
puertaMadera := fabricaPuertaMadera.ConstruirPuerta()
fmt.Printf("Se construyo un puerta de: %s\n", puertaMadera.VerMaterial())

fabricaPuertaMetal := &FabricaPuertaMetal{}
puertaMetal := fabricaPuertaMetal.ConstruirPuerta()
fmt.Printf("Se construyo un puerta de: %s\n", puertaMetal.VerMaterial())
```

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/creacionales/abstractfactory) | [Ejecutar código](https://play.golang.org/p/8yy8vp4cDD5)

## Patrones relacionados

Los tipos de datos FabricaAbstracta suelen implementarse con métodos de fabricación (patrón [Factory Method](/patrones/creacionales/factorymethod.md)), pero también se pueden implementar usando [Prototype](/patrones/creacionales/prototype.md).
Una fábrica concreta suele ser un [Singleton](/patrones/creacionales/singleton.md).

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Abstract Factory_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
