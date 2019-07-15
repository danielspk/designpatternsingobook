# Objetos en Go

A diferencia de lenguajes explícitamente orientados a objetos como _C++_, _Java_, _C\#_, _Python_ y _PHP_ entre otros, en _Go_ no hay clases, ni objetos, ni excepciones, ni herencia.

Rápidamente se podría inferir que _Go_ no es un lenguaje orientado a objetos. ¿Cómo puede existir un lenguaje orientado a objetos que no disponga de clases?. La pregunta que realmente debemos hacernos es: _**¿Qué es la programación orientada a objetos?**_.

Los desarrolladores tenemos una tendencia natural a comparar las cosas. Entonces, por ejemplo, se podría decir que dado que _Java_ es academicamente reconocido como un lenguaje puramente orientado a objetos, y éste lenguaje tiene entre otras características clases y herencia; como _Go_ no las tiene entonces no puede ser un lenguaje orientado a objetos.

_¿Alguien alguna vez escucho decir que Javascript es un lenguaje orientado a objetos?_. Existe una gran discución sobre si lo es o no - a fin de cuentas en _Javascript_ tampoco hay clases ni herencia de la forma clásica como la que las hay en _Java_. No obstante _Javascript_ suele ser considerado un lenguaje orientado a objetos. _¿Porqué?_. Porque permite implementar ciertas características de la programación orientada a objetos.

> En ES6 se incorporan las clases en Javascript aunque con un soporte muy limitado en comparación con otros lenguajes orientados a objetos clásicos.

Al analizar a _Go_, debemos comparar qué características de la programación orientada a objetos se pueden implementar y no simplemente hacer una comparación de un lenguaje respecto de otro.

## Cómo es la POO en Go

### Objetos

En _Go_ no existen clases ni objetos. Existen estructuras, que son tipos de datos definidos por el usuario, a las cuales se les pueden incorporar comportamientos. En una analogía con una clase, las propiedades pudieran ser los tipos de datos de la estructura, y los métodos las funciones o comportamientos asociados a la estructura.

Ejemplo:

```go
type Persona struct {
    Nombre   string
    Apellido string
    Edad     int
}

func (p *Persona) Saludar() {
   fmt.Printf("Nombre: %s, Apellido: %s, Edad: %d\n", p.Nombre, p.Apellido, p.Edad)
}
```

[Ejecutar código](https://play.golang.org/p/3uoR7qRs9eV)

### Interfaces

Las interfaces en _Go_ son una característica distintiva del lenguaje. A diferencia de otros lenguajes de programación como _Visual Basic .Net_ o _Kotlin_ donde la interfaces se implementan de forma explícita, en _Go_ la interfaces son implícitas ya que no existe ninguna palabra reservada o símbolo para tal fin (tal como _implements_ en _Groovy_ o _:_ en _C#_).

En _Go_ cualquier estructura de datos que implemente todos los métodos de una interfaz, implícitamente la implementa. Este comportamiento es análogo a otros lenguajes, como _Python_ o _Boo_, donde a esto se lo conoce como _Duck typing ("si camina como un pato y grazna como un pato, entonces debe ser un pato" [\[54\]](/recursos.md))_. En _Go_ el compilador chequea forzosamente que se si referencia un tipo de dato como una _interface_, este debe implementar todos sus comportamientos sin excepción.

Ejemplo:

```go
type Felino interface {
    Caminar()
    Saltar()
}

type Leon struct {
    Nombre string
}

func (t Leon) Caminar() {
   fmt.Println("CAMINAR")
}

func (t Leon) Saltar() {
   fmt.Println("SALTAR")
}

func SaltarYCaminar(felino Felino) {
    felino.Saltar()
    felino.Caminar()
}

leon := Leon{"Simba"}
SaltarYCaminar(leon)
```

[Ejecutar código](https://play.golang.org/p/MD6D893_1KB)

Como se puede observar el método _SaltarYCaminar\(\)_ espera una variable de tipo _Felino_ pero se le pasa una de tipo _Leon_. Como la estructura _Leon_ implementar los métodos _Caminar\(\)_ y _Saltar\(\)_ implícitamente también es un _Felino_.

### Los tres pilares de la programación orientada a objetos

Los tres pilares de la programación orientada a objetos son la _herencia_, el _encapsulamiento_ y el _polimorfismo_.

#### Herencia

Como ya se dijo, en _Go_ no existe la herencia. Las estructuras permiten ampliar/modificar su comportamiento incrustrando otras estructuras. - _más información en el siguiente apartado de ["Herencia / Composición"](composicion.md)_

Ejemplo:

```go
type Persona struct {
    Nombre   string
    Apellido string
    Edad     int
}

type Empleado struct {
    Persona
    Legajo string
}

func (p *Persona) DatosBase() {
   //...
}

func (e *Empleado) DatosAdicionales() {
   //...
}

empleado := Empleado{
    Persona{"Jose", "Sánchez", 33},
    "A1234",
}
empleado.DatosBase()
empleado.DatosAdicionales()
```

[Ejecutar código](https://play.golang.org/p/oW83TcMCzHp)

Cada estructura incorpora los tipos de datos y comportamientos de la/s estructura/s incrustrada/s.

#### Encapsulamiento

En _Go_ no existen identificadores de privacidad tales como _public_, _protected_ y _private_ típicos de otros lenguajes de programación. _Go_ encapsula estructuras y funciones a nivel de paquete en base a convenciones de nombres.  
Todos aquellos nombres que empiecen con mayúsculas serán accesibles \(visibles\) desde otros paquetes. Por el contrario, aquellos que comiencen con minúsculas serán _privados_.  
Esta es la razón por la que en el código fuente de paquetes y bibliotecas de _Go_ hay estructuras y funciones que pueden comenzar con mayúsculas o minúsculas.

```go
// estructura pública
type CuentaCorriente struct {
    //...
}

// método privado
func (cc CuentaCorriente) calcularIntereses() double {
    //...
}
```

#### Polimorfismo

En _Go_ el polimorfismo se comporta tal como se esperaría. Dado que las estructuras pueden componerse de otras estructuras, tan sólo se debe reescribir el o los comportamientos deseados. - _más información en el siguiente apartado de ["Herencia / Composición"](composicion.md)_

Ejemplo:

```go
type Empleado struct {
   legajo string
   ingreso string
}

func (e *Empleado) InformarIngreso() {
   fmt.Printf("Mi legajo fue el %s.", e.ingreso)
}

func (e *Empleado) Presentarse() {
   fmt.Printf("Mi legajo es %s.", e.legajo)
}

type Gerente struct {
    Empleado
}

func (g *Gerente) Presentarse() {
   g.Empleado.Presentarse()

   fmt.Println(" Mi cargo es el de Gerente.")
}

gerente := Gerente{
    Empleado{"A0001", "01-01-2020"},
}
gerente.Presentarse()
gerente.InformarIngreso()
```

[Ejecutar código](https://play.golang.org/p/rBBwVyj9sjQ)

#### Método Estáticos

Esta característica no es posible de replicar en _Go_ dado que cada comportamiento asociado a una estructura, sólo puede ser invocado cuando exista un referencia a dicha estructura.
Se puede emular esta característica usando el paradigma procedimental del lenguaje. Si bien no es un comportamiento puramente orientado a objetos, se pueden lograr similares resultados.

Ejemplo:

```go
package Modelos

// estructura
type CuentaCorriente struct {
    //...
}

// emular propiedad estática
// utilizando variable de paquete
var banco = "Banco S.A."

// emular método estático de CuentaCorriente 
// utilizando una función de paquete
func CuentaCorrienteGetBanco() string {
    return banco
}
```

## Qué dicen otros autores

Según Gigi Sayfan [\[4\]](/recursos.md) "Go es una extraña mezcla de ideas antiguas y nuevas.", y "Muchas personas ni siquiera están seguras de si Go es un lenguaje orientado a objetos", sin embargo para el "Go es un lenguaje de programación orientado a objetos de buena fe. Permite el modelado basado en objetos y promueve las mejores prácticas de usar interfaces en lugar de tipos concretos de jerarquías. Go tiene algunas elecciones sintácticas inusuales, pero el trabajo general con tipos, métodos e interfaces parece simple, ligero y natural. La incrustración no es muy pura, pero aparentemente estaba en juego el pragmatismo, y se proporcionó una incrustración en lugar de sólo la composición por nombre".

Para Junade Ali [\[30\]](/recursos.md) "La programación orientada a objetos es más que solo clases y objetos; es un paradigma de programación basado alrededor de objetos \(estructuras de datos\) que contienen campos de datos y métodos. Es esencial entender esto; el uso de clases para organizar un grupo de métodos no relacionados no es orientación a objetos".

Incluso la propia gente que desarrolla _Go_ responde a esta pregunta [\[44\]](/recursos.md) como "Si y no."

## Mi punto de vista

Ya que existen otros lenguajes que permiten programar orientado a objetos, sin ser realmente orientados a objetos, puedo decir que **"**_**Go**_** es un lenguaje no orientado a objetos que permite la programación orientada a objetos - **_**aunque no de la forma tradicional**_**"**.

