# Abstract Factory

## Propósito

Proporciona una interfaz para crear familias de variables relacionadas o que dependan entre sí, sin especificar sus tipos de datos concretos.

## También conocido como

_Kit_

## Estructura

![](../../../.gitbook/assets/abstractfactory.png)

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

## Implementación

* No se observan impedimentos y/o modificaciones de la estructura original del patrón para su implementación en _Go_.
* La _FabricaAbstracta_ y _ProductoAbstracto_ se definen como interfaces por simplificación.

## Código de ejemplo

En este ejemplo queremos comprar distintos tipos de puertas de madera \(madera o metal\). Al realizar el pedido el local de venta debe encargar cada puerta a distintos fabricantes, ya que quien realiza la puerta de madera no la hace de metal y viceversa.

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

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/creacionales/abstractfactory) \| [Ejecutar código](https://play.golang.org/p/8yy8vp4cDD5)

