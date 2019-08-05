# Patrón Template Method

## Propósito

Define en una operación el esqueleto de un algoritmo, delegando en los subtipos de datos algunos de sus pasos. Permite que los subtipos de datos definan ciertos pasos de un algoritmo sin cambiar su esquema.

## Aplicabilidad

El patrón Template Method debería usarse

* para implementar las partes de un algoritmo que no cambian y dejar que sean los subtipos de datos quienes implementen el comportamiento que puede variar.
* cuando el comportamiento repetido de varios subtipos de datos debería factorizarse y ser localizado en un tipo de dato común para evitar el código duplicado.Ésta en una buena idea de "refactorizar para generalizar". En primer lugar identificamos las diferencias en el código existente y a continuación separamos dichas diferencias en nuevas operaciones. Por último, sustituimos el código que cambia por una función (comportamiento)  que llama a una de estas nuevas operaciones.
* para controlar las extensiones de los subtipos de datos. Podemos definir una función plantilla que llame a operaciones "de enganche" en determinados puntos, permitiendo así las extensiones sólo en esos puntos.

## Estructura

![](/assets/uml/templatemethod.png)

## Participantes

* **ClaseAbstracta:**
  * define operaciones primitivas abstractas que son definidas por los subtipos de datos para implementar los pasos de un algoritmo.
  * implementa una función plantilla que define el esqueleto de un algoritmo. La función plantilla llama a las operaciones primitivas así como a operaciones definidas en ClaseAbstracta o a las de otras variables.
* **ClaseConcreta:**
  * implementa las operaciones primitivas para realizar los pasos del algoritmo específicos de los subtipos de datos.

## Colaboradores

ClaseConcreta se basa en ClaseAbstracta para implementar los pasos de un algoritmo que no cambian.

## Implementación

- No se observan impedimentos para su implementación en _Go_.
- En este caso, dado que no existe la herencia de clase en _Go_, la _ClaseAbstracta_ sugerida por el patrón debe implementarse en dos partes: a) por un lado los comportamientos abstractos deben definirse en una _Interface_, y b) por otro lado los comportamientos concretos (_el método plantilla_) dentro del propio tipo _ClaseAbstracta_.
- Las _ClasesConcretas_ se componen (_en vez de heredar_) de una _ClaseConcreta_.
- Las _ClasesConcretas_ implementan los comportamientos de la _Interface_.
- La principal dificultad de implementar este patrón en _Go_ es que el comportamiento del método plantilla de la _ClaseAbstracta_ invoca a otros comportamientos que no están definidos dentro de la propia _ClaseAbstracta_ sino dentro de la _ClaseConcreta_. Esto obliga a que cuando se invoca el método plantilla desde una _ClaseConcreta_ se deba pasar una referencia de si misma para que el método plantilla pueda invocar los comportamientos definidos en la _Interface_.

> Dada esta complejidad adicional léase esta forma de implementación junto al código de ejemplo del patrón.

## Código de ejemplo

En este ejemplo queremos cumplir con una serie de pasos formales _(método plantilla)_ para deployar diferentes aplicaciones mobile.

Implementación:

```go
// Clase Abstracta - Interface
type DeployInterface interface {
    Testear()
    Compilar()
    Publicar()
}

// Clase Abstracta
type Deploy struct{}

// Método Plantilla
func (d Deploy) Construir(di DeployInterface) {
    fmt.Println("Ejecutando las siguientes acciones:")

    di.Testear()
    di.Compilar()
    di.Publicar()
}

// Clase Concreta - Android
type DeployAndroid struct {
    Deploy
}

func (d DeployAndroid) Testear() {
    fmt.Println("Android: Testeando")
}

func (d DeployAndroid) Compilar() {
    fmt.Println("Android: Compilando")
}

func (d DeployAndroid) Publicar() {
    fmt.Println("Android: Publicando")
}

// Clase Concreta - iOS
type DeployiOS struct {
    Deploy
}

func (d DeployiOS) Testear() {
    fmt.Println("iOS: Testeando")
}

func (d DeployiOS) Compilar() {
    fmt.Println("iOS: Compilando")
}

func (d DeployiOS) Publicar() {
    fmt.Println("iOS: Publicando")
}
```

Se puede probar la implementación del patrón de la siguiente forma:

```go
deployAndroid := DeployAndroid{Deploy{}}
deployAndroid.Construir(&deployAndroid)

deployiOS := DeployiOS{Deploy{}}
deployiOS.Construir(&deployiOS)
```

[Código de ejemplo](https://github.com/danielspk/designpatternsingo/tree/master/patrones/comportamiento/templatemethod) | [Ejecutar código](https://play.golang.org/p/1J-MIDMaXi5)

## Patrones relacionados

Los [Factory Method](/patrones/creacionales/factorymethod.md) se llaman muchas veces desde Template Method.
[Strategy](/patrones/comportamiento/strategy.md): Template Method usa la composición para modificar una parte de un algoritmo. Las estrategias usan delegación para variar el algoritmo completo.

##### Nota:
> A excepción de los apartados "_Estructura_", "Implementación" y "_Código de Ejemplo_", los téxtos utilizados para redactar el patrón _Template Method_ son transcripciones - en algunos casos brevemente alteradas - del libro "Patrones de Diseño" de Erich Gamma, Richard Helm, Ralph Johnson y John Vlissides [\[29\]](/recursos.md).
