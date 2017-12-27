# Patrón Strategy

## Propósito

Define una familia de algoritmos, encapsula cada uno de ellos y los hace intercambiables. Permite que un algoritmo varíe independientemente de los clientes que lo usan.

## También conocido como

_Policy_

## Motivación

**Contenido en desarrollo.**

![](/assets/uml/ejemplos/strategy.png)

## Aplicabilidad

**Contenido en desarrollo.**

## Estructura

![](/assets/uml/strategy.png)

## Participantes

**Contenido en desarrollo.**

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

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/comportamiento/strategy) | [Ejecutar código](https://play.golang.org/p/OoMEcPgef7e)

## Usos conocidos

**Contenido en desarrollo.**

## Patrones relacionados

[Flyweight](/patrones/estructurales/flyweight.md): los objetos Estrategia suelen ser buenos pesos ligeros.
