# Patrón Decorator

## Propósito

Asigna responsabilidades adicionales a una variable dinámicamente, proporcionando una alternativa flexible a la herencia _(composición)_ para extender la funcionalidad.

## También conocido como

_Wrapper_ (Envoltorio)

## Aplicabilidad

Úsese el patrón Decorator cuando:
* desea añadir variables individuales de forma dinámica y transparente, es decir, sin afectar a otras variables.
* pueda requerir retirar responsabilidades.
* la extensión mediante la composición no es viable.

## Estructura

![](/assets/uml/decorator.png)

## Participantes

* **Componente:**
  * define la interfaz para variables a las que se puede añadir responsabilidades dinámicamente.
* **ComponenteConcreto:**
  * define una variable a la que se pueden añadir responsabilidades adicionales.
* **Decorador:**
  * mantiene una referencia a una variable Componente y define una interfaz que se ajusta a la interfaz del Componente.
* **DecoradorConcreto:**
  * añade responsabilidades al componente.

## Colaboradores

El Decorador redirige peticiones a su variable Componente. Opcionalmente puede realizar operaciones adicionales antes y después de reenviar la petición.

## Implementación

No se observan impedimentos y/o modificaciones de la estructura original del patrón para su implementación en _Go_.

## Código de ejemplo

En este ejemplo queremos agregarle dinámicamente ingredientes adicionales a un un cafe que por defecto viene simple.

Implementación:

```go
// Componente Interface
type CafeInterface interface {
    GetCosto() int
    GetDetalle() string
}

// Componente Concreto
type Cafe struct{}

func (c *Cafe) GetCosto() int {
    return 30
}

func (c *Cafe) GetDetalle() string {
    return "Cafe"
}

// Decorador
type CafeDecorador struct {
    CafeInterface
}

func (cd *CafeDecorador) GetCosto() int {
    return cd.CafeInterface.GetCosto()
}

func (cd *CafeDecorador) GetDetalle() string {
    return cd.CafeInterface.GetDetalle()
}

// Decorador Concreto
type CafeConCrema struct {
    *CafeDecorador
}

func (ccc *CafeConCrema) GetCosto() int {
    return ccc.CafeDecorador.GetCosto() + 15
}

func (ccc *CafeConCrema) GetDetalle() string {
    return ccc.CafeDecorador.GetDetalle() + " con crema"
}

// Decorador Concreto
type CafeConCanela struct {
    *CafeDecorador
}

func (ccc *CafeConCanela) GetCosto() int {
    return ccc.CafeDecorador.GetCosto() + 10
}

func (ccc *CafeConCanela) GetDetalle() string {
    return ccc.CafeDecorador.GetDetalle() + " con canela"
}
```

Se puede probar la implementación del patrón de la siguiente forma:

```go
cafe := &Cafe{}
fmt.Printf("Detalle: %s - Importe $%d\n", cafe.GetDetalle(), cafe.GetCosto())

cafeConCrema := &CafeConCrema{&CafeDecorador{cafe}}
fmt.Printf("Detalle: %s - Importe $%d\n", cafeConCrema.GetDetalle(), cafeConCrema.GetCosto())

cafeConCremaConCanela := &CafeConCanela{&CafeDecorador{cafeConCrema}}
fmt.Printf("Detalle: %s - Importe $%d\n", cafeConCremaConCanela.GetDetalle(), cafeConCremaConCanela.GetCosto())
```

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/estructurales/decorator) | [Ejecutar código](https://play.golang.org/p/62xDpf7XUv_m)

## Patrones relacionados

[Adapter](/patrones/estructurales/adapter.md): un decorador se diferencia de un adaptador en que el decorador sólo cambia las responsabilidades de una variable, no su interfaz, mientras que un adaptador le da a una variable una interfaz completamente nueva.
[Composite](/patrones/estructurales/composite.md): se puede ver a un decorador como un composite degenerado que sólo tiene un componente. No obstante, un decorador añade responsabilidades adicionales - no está pensado para la agregación de variables -.
[Strategy](/patrones/comportamiento/strategy.md): un decorador permite cambiar el exterior de una variable; un strategy permite cambiar su interior. Son dos formas alternativas de modificar una vaariable.

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Decorator_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
