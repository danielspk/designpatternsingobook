# Patrón Builder

## Propósito

Separa la construcción de una variable compleja de su representación, de forma que el mismo proceso de construcción pueda crear diferentes representaciones.

## Aplicabilidad

Úsese el patrón Builder cuando:
* el algoritmo para crear una variable compleja debiera ser independiente de las partes de que se compone dicha variable y de cómo se ensamblan.
* el proceso de construcción debe permitir diferentes representaciones de la variable que está siendo construida.

## Estructura

![](/assets/uml/builder.png)

## Participantes

* **Constructor:**
  * especifica una interfaz abstracta para crear las partes de una variable Producto.
* **ConstructorConcreto:**
  * implementa la interfaz de Constructor para construir y ensamblar las partes del producto.
  * proporciona una interfaz para devolver el producto.
* **Director:**
  * construye una variable usando la interfaz Constructor.
* **Producto:**
  * representa una variable compleja en construcción. El ConstructorConcreto construye la representación interna del producto y define el proceso de ensamble.
  * incluye los tipos de datos que definen sus partes constituyentes, incluyendo interfaces para ensamblar las partes en el resultado final.

## Colaboradores

* El cliente crea la variable Director y la configura con la variable Constructor deseada.
* El Director notifica al constructor cada vez que hay que construir una parte de un producto.
* El Constructor maneja las peticiones del director y las añade al producto.
* El cliente obtiene el producto del constructor.

## Implementación

- No se observan impedimentos y/o modificaciones de la estructura original del patrón para su implementación en _Go_.
- El _Constructor_ se define como interface por simplificación.

## Código de ejemplo

En este ejemplo queremos que un local de comida pueda entregar distintos tipos de hamburguesas (simples y dobles) para lo que será necesario generar distintos constructores de hamburguesas.

Implementación:

```go
// Interface Constructor
type Constructor interface {
    EstablecerTamanio()
    Construir() *Hamburguesa
}

// Constructor Concreto
type ConstructorHamburguesaSimple struct {
    tamanio string
}

func (chs *ConstructorHamburguesaSimple) EstablecerTamanio() {
    chs.tamanio = "Simple"
}

func (chs *ConstructorHamburguesaSimple) Construir() *Hamburguesa {
    return &Hamburguesa{chs.tamanio}
}

// Constructor Concreto
type ConstructorHamburguesaDoble struct {
    tamanio string
}

func (chd *ConstructorHamburguesaDoble) EstablecerTamanio() {
    chd.tamanio = "Doble"
}

func (chd *ConstructorHamburguesaDoble) Construir() *Hamburguesa {
    return &Hamburguesa{chd.tamanio}
}

// Producto
type Hamburguesa struct {
    Tamanio string
}

// Director
type LocalComida struct{}

func (lc *LocalComida) ConstruirHamburguesa(constructor Constructor) *Hamburguesa {
    constructor.EstablecerTamanio()

    return constructor.Construir()
}
```

Se puede probar la implementación del patrón de la siguiente forma:

```go
localComida := &LocalComida{}

hamburguesaA := localComida.ConstruirHamburguesa(&ConstructorHamburguesaSimple{})
hamburguesaB := localComida.ConstruirHamburguesa(&ConstructorHamburguesaDoble{})

fmt.Printf("Se solicito una hamburguesa: %s\n", hamburguesaA.Tamanio)
fmt.Printf("Se solicito una hamburguesa: %s\n", hamburguesaB.Tamanio)
```

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/creacionales/builder) | [Ejecutar código](https://play.golang.org/p/5dPp1a1Yaw_F)

## Patrones relacionados

El patrón [Abstract Factory](/patrones/creacionales/abstractfactory.md) se parece a un Builder en que también puede construir variables complejas. La principal diferencia es que el patrón Builder se centra en construir una variable compleja paso a paso. El Abstract Factory hace hincapié en familias de variables producto (simples o complejas). El Builder devuelve el producto como paso final, mientras que el Abstract Factory lo devuelve inmediatamente.
Muchas veces lo que construye el constructor es un [Composite](/patrones/estructurales/composite.md).

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Builder_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
