# Patrón Strategy

## Propósito

Define una familia de algoritmos, encapsula cada uno de ellos y los hace intercambiables. Permite que un algoritmo varíe independientemente de los clientes que lo usan.

## También conocido como

_Policy_

## Aplicabilidad

El patrón Strategy se debe usar cuando:

* muchos tipos de datos relacionados difieren sólo en su comportamiento. Las estrategias permiten configurar un tipo de dato con un determinado comportamiento de entre muchos posibles.
* se necesitan distintas variantes de un algoritmo.
* un algoritmo usa datos que los clientes no deberían conocer.
* un tipo de dato define muchos comportamientos, y éstos se representan como múltiples sentencias condicionales en sus operaciones.

## Estructura

![](/assets/uml/strategy.png)

## Participantes

* **Estrategia:**
  * declara la interfaz común a todos los algoritmos permitidos. El _Contexto_ usa esta interfaz para llamar al algoritmo definido por una _EstrategiaConcreta_.
* **EstrategiaConcreta:**
  * implementa el algoritmo usando la interfaz _Estrategia_.
* **Contexto:**
  * se configura con una variable _EstrategiaConcreta_.
  * mantiene una referencia a una variable _Estrategia_.
  * puede definir una interfaz que permita a la _Estrategia_ acceder a sus datos.

## Colaboradores

* _Estrategia_ y _Contexto_ interactúan para implementar el algoritmo elegido. Un _Contexto_ puede pasar a la _Estrategia_ todos los datos requeridos por el algoritmo cada vez que se llama a éste. Otra alternativa es que el _Contexto_ se pase a sí mismo como argumento de las operaciones de _Estrategia_. Eso permite a la _Estrategia_ hacer llamadas al _Contexto_ cuando sea necesario.
* Un _Contexto_ redirige peticiones de los clientes a su _Estrategia_. Los clientes normalmente crean una variable _EstrategiaConcreta_, la cual pasan al _Contexto_. Suele haber una familia de tipos de datos _EstrategiaConcreta_ a elegir  por el cliente.

## Implementación

No se observan impedimentos y/o modificaciones de la estructura original del patrón para su implementación en _Go_.

## Código de ejemplo

En este ejemplo queremos definir tres estrategias concretas que pueden realizar distintas operaciones matemáticas. Cuando se crea el contexto se establece que estrategia deberá utilizar.

Implementación:

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

Se puede probar la implementación del patrón de la siguiente forma:

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

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/comportamiento/strategy) \| [Ejecutar código](https://play.golang.org/p/OoMEcPgef7e)

## Patrones relacionados

[Flyweight](/patrones/estructurales/flyweight.md): las variables Estrategia suelen ser buenos pesos ligeros.

##### Nota:

> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Strategy_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).



