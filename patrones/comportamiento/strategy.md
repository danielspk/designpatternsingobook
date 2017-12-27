# Patrón Strategy

## Propósito

Define una familia de algoritmos, encapsula cada uno de ellos y los hace intercambiables. Permite que un algoritmo varíe independientemente de los clientes que lo usan.

## También conocido como

_Policy_

## Motivación

**Contenido en desarrollo.**

![](/assets/uml/ejemplos/strategy.png)

## Aplicabilidad

Use el patrón Strategy cuando:

* muchas estructuras relacionadas difieren sólo en su comportamiento. Las estrategias permiten configurar una estructura con un determinado comportamiento de entre muchos posibles.
* se necesitan distintas variantes de un algoritmo.
* un algoritmo usa datos que los clientes no deberían conocer.
* una estructura define muchos comportamientos, y éstos se representan como múltiples sentencias condicionales en sus operaciones.

## Estructura

![](/assets/uml/strategy.png)

## Participantes

* **Estrategia:**
  * declara la interfaz común a todos los algoritmos permitidos. El _Contexto_ usa esta interfaz para llamar al algoritmo definido por una _EstrategiaConcreta_.
* **EstrategiaConcreta:**
  * implementa el algoritmo usando la interfaz _Estrategia_.
* **Contexto:**
  * se configura con una estructura con estado _EstrategiaConcreta_.
  * mantiene una referencia a una estructura con estado _Estrategia_.
  * puede definir una interfaz que permita a la _Estrategia_ acceder a sus datos.

## Colaboradores

**Contenido en desarrollo.**

## Consecuencias

**Contenido en desarrollo.**

## Implementación

**Contenido en desarrollo.**

## Código de ejemplo

**Contenido en desarrollo.**

```go
// Interface
type Estrategia interface {
    RealizarOperacion(int, int) int
}

// Estrategia Suma
type EstrategiaSuma struct{}

func (e EstrategiaSuma) RealizarOperacion(num1 int, num2 int) int {
    return num1 + num2
}

// Estrategia Resta
type EstrategiaResta struct{}

func (e EstrategiaResta) RealizarOperacion(num1 int, num2 int) int {
    return num1 - num2
}

// Estrategia Multiplica
type EstrategiaMultiplica struct{}

func (e EstrategiaMultiplica) RealizarOperacion(num1 int, num2 int) int {
    return num1 * num2
}

// Contexto
type Contexto struct {
    estrategia Estrategia
}

func (c *Contexto) EjecutarOperacion(num1 int, num2 int) int {
    return c.estrategia.RealizarOperacion(num1, num2)
}
```

```go
var contexto Contexto
num1 := 10
num2 := 5

contexto = Contexto{EstrategiaSuma{}}
fmt.Printf("%d + %d = %d\n", num1, num2, contexto.EjecutarOperacion(num1, num2))

contexto = Contexto{EstrategiaResta{}}
fmt.Printf("%d - %d = %d\n", num1, num2, contexto.EjecutarOperacion(num1, num2))

contexto = Contexto{EstrategiaMultiplica{}}
fmt.Printf("%d * %d = %d\n", num1, num2, contexto.EjecutarOperacion(num1, num2))
```

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/comportamiento/strategy) | [Ejecutar código](https://play.golang.org/p/OoMEcPgef7e)

## Usos conocidos

**Contenido en desarrollo.**

## Patrones relacionados

[Flyweight](/patrones/estructurales/flyweight.md): las estructuras con estado Estrategia suelen ser buenos pesos ligeros.
