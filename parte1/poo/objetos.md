# Objetos

A diferencia de lenguajes explícitamente orientados a objetos como _C++_, _Java_, _Smalltalk_, y _Python_ entre otros, en _Go_ no existen las clases, ni los objetos, ni las excepciones, ni la herencia de clases.

Algunos, rápidamente podrían inferir que _Go_ no es un lenguaje orientado a objetos. ¿Cómo puede existir un lenguaje orientado a objetos que no disponga de clases?. La pregunta que realmente debemos hacernos es: _**¿Qué es la programación orientada a objetos?**_.

Los desarrolladores tenemos una tendencia natural a comparar las cosas. Entonces, por ejemplo, algunos podrían decir que dado que _Java_ es académicamente reconocido como un lenguaje estrictamente orientado a objetos, y dado que ese lenguaje tiene entre otras características clases, objetos y herencia; como _Go_ no las tiene, entonces no podría ser un lenguaje orientado a objetos.

_¿Alguien alguna vez escuchó decir que Javascript es un lenguaje orientado a objetos?_. Existe una gran discusión sobre si lo es o no lo es - a fin de cuentas en _Javascript_ tampoco hay clases ni herencia de la forma como la que la hay en _Java_. No obstante _Javascript_ suele ser considerado un lenguaje orientado a objetos. _¿Porqué?_. Porque permite implementar ciertas características de la programación orientada a objetos.

> En ES6 se incorporan las clases en Javascript aunque con un soporte muy limitado en comparación con otros lenguajes orientados a objetos clásicos.

Limitar el análisis a si un lenguaje es o no orientado a objetos por la sola existencia de la palabra reservada _"class"_ sería absolutamente simplista e incorrecto. A modo de ejemplo, _Objective-C_ define sus clases sin hacer uso de una palabra _"class"_ y el propio lenguaje se define a sí mismo como proveedor de características orientadas a objetos.

Las _clases_ no caracterizan a los lenguajes orientados a objetos. Un lenguaje soporta el paradigma orientado a objetos si respeta los pilares propios de la programación orientada a objetos. - _se verán más adelante_ -.

Cada lenguaje es único y permite implementar el paradigma orientado a objetos de diversas maneras. Algunas comparaciones de ejemplo:

* Herencia de clase
  * Simple
    * _Scala_
    * _Smalltalk_
  * Múltiple
    * _Eifell_
    * _C++_
* Herencia de Interfaces
  * Explícitas
    * _C++_ _\(mediante clases abstractas y métodos virtuales\)_
    * _Scala_ _\(mediante herencia simple de clase y/o traits\)_
    * _Eifell_ _\(mediante herencia simple/múltiple de clase\)_
  * Implícitas
    * _Smalltalk_
* Rasgos _\(Traits\)_
  * Permite
    * _Scala_
    * _Smalltalk_
    * _C++_ _\(mediante templates\)_
  * No Permite
    * _Eiffel_
* Sobrecarga de Métodos
  * Permite
    * _Scala_
    * _C++_
  * No Permite
    * _Smalltalk_
    * _Eiffel_

Como se puede apreciar lenguajes como _Scala_, _Eiffel_, _C++_ y _Smalltalk_ son muy distintos entre sí, pero todos ellos respetan el paradigma orientado a objetos.

Al analizar a _Go_, debemos comparar qué características propias de la programación orientada a objetos se pueden implementar y no simplemente hacer una comparación de un lenguaje respecto de otro sólamente por la falta o no de ciertos atributos o características individuales.

## Cómo es la POO en Go

### Clases y Objetos

En _Go_ no existen clases ni objetos. Existen tipos de datos definidos por el usuario a los cuales se les pueden incorporar comportamientos. En una analogía con una clase, las propiedades pudieran ser los tipos de datos de una estructura, y los métodos las funciones o comportamientos asociados al tipo de dato.

Ejemplo sobre una estructura:

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

Ejemplo sobre un tipo de dato especializado:

```go
type Int int

func (n Int) EsMayorQue(n2 Int) bool {
   return n > n2;
}
```

[Ejecutar código](https://play.golang.org/p/5WXUHGRBfn4)

### Interfaces

"La interfaz de un objeto no dice nada acerca de su implementación - distintos objetos son libres de implementar las peticiones de forma diferente -. Eso significa que dos objetos con implementaciones completamente diferentes pueden tener interfaces idénticas". [\[29\]](../../recursos.md). _Go_ cumple con esta característica de interfaces sin implementación. Lenguajes de programación tales como _Visual Basic .Net_ o _Kotlin_ definen sus interfaces de forma explícita. En _Go_ las interfaces son implícitas ya que no existe ninguna palabra reservada o símbolo para tal fin \(tal como _implements_ en _Groovy_ o _:_ en _C\#_\). En _Go_ cualquier tipo de dato que implemente todos los métodos de una interfaz, implícitamente la implementa. Este comportamiento es análogo al de algunos lenguajes de tipado dinámico, como _Python_ o _Boo_, donde a esto se lo conoce como _Duck typing \("si camina como un pato y grazna como un pato, entonces debe ser un pato"_ [_\[54\]_](../../recursos.md)_\)_. En _Go_ el compilador chequea forzosamente que se si referencia a un tipo de dato como una _interface_, este debe implementar todos sus comportamientos sin excepción.

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

Como se puede observar la función _SaltarYCaminar\(\)_ espera una variable de tipo _Felino_ pero se le pasa una de tipo _Leon_. Como el tipo _Leon_ implementar los métodos _Caminar\(\)_ y _Saltar\(\)_ implícitamente también es un _Felino_.

### Los tres pilares de la programación orientada a objetos

Los tres pilares de la programación orientada a objetos son la _herencia_, el _encapsulamiento_ y el _polimorfismo_.

#### Herencia

Como ya se dijo, en _Go_ no existe la herencia, o al menos no la herencia de clases como se la conoce en otros lenguajes tales como _Scala_, _Swift_ o _Eiffel_ por ejemplo.

Los tipos de datos en _Go_ permiten ampliar/modificar su comportamiento incrustando otros tipos dentro de él.

Cada estructura incorpora los tipos de datos y comportamientos de la/s estructura/s incrustrada/s.

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

También es posible extender/reemplazar el comportamiento de la/s estructura/s incrustrada/s reescribiendo el/los comportamiento/s deseado/s.

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

En _Go_ entonces se manifiesta la herencia de interfaz. - _más información en el siguiente apartado de_ [_"Herencia / Composición"_](composicion.md)_._

#### Encapsulamiento

En _Go_ no existen identificadores de privacidad tales como _public_, _protected_ y _private_ típicos de otros lenguajes de programación. _Go_ encapsula tipos de datos y funciones a nivel de paquete en base a convenciones de nombres.  
Todos aquellos nombres que empiecen con mayúsculas serán accesibles \(visibles\) desde otros paquetes. Por el contrario, aquellos que comiencen con minúsculas serán _privados_.  
Esta es la razón por la que en el código fuente de paquetes y bibliotecas de _Go_ hay tipos de datos y funciones que pueden comenzar con mayúsculas o minúsculas.

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

_Go_ es polimórfico. Gracias a la herencia de interfaces se pueden asignar referencias en forma polimórfica. - _más información en el siguiente apartado de_ [_"Herencia / Composición"_](composicion.md)

Ejemplo:

```go
type Figura interface {
   Dibujar()
}

type Cuadrado struct {}

func (c *Cuadrado) Dibujar() {
   fmt.Println("Dibujando un Cuadrado.")
}

type Triangulo struct {}

func (t *Triangulo) Dibujar() {
    fmt.Println("Dibujando un Triángulo.")
}

func dibujarFigura(f Figura) {
    f.Dibujar()
}

cuadrado := Cuadrado{}
dibujarFigura(&cuadrado)

triangulo := Triangulo{}
dibujarFigura(&triangulo)
```

[Ejecutar código](https://play.golang.org/p/yWlSrH_aXZg)

En _Go_ el polimorfismo se logra con la ayuda de interfaces.

#### Método Estáticos

Esta característica no es posible de replicar en _Go_ dado que cada comportamiento asociado a un tipo de datos, sólo puede ser invocado cuando exista un referencia a dicho tipo. Se puede emular esta característica usando el paradigma procedimental del lenguaje. Si bien no es un comportamiento puramente orientado a objetos, se pueden lograr similares resultados.

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

Según Gigi Sayfan [\[4\]](../../recursos.md) "Go es una extraña mezcla de ideas antiguas y nuevas.", y "Muchas personas ni siquiera están seguras de si Go es un lenguaje orientado a objetos", sin embargo para el "Go es un lenguaje de programación orientado a objetos de buena fe. Permite el modelado basado en objetos y promueve las mejores prácticas de usar interfaces en lugar de tipos concretos de jerarquías. Go tiene algunas elecciones sintácticas inusuales, pero el trabajo general con tipos, métodos e interfaces parece simple, ligero y natural. La incrustración no es muy pura, pero aparentemente estaba en juego el pragmatismo, y se proporcionó una incrustración en lugar de sólo la composición por nombre".

Para Junade Ali [\[30\]](../../recursos.md) "La programación orientada a objetos es más que solo clases y objetos; es un paradigma de programación basado alrededor de objetos \(estructuras de datos\) que contienen campos de datos y métodos. Es esencial entender esto; el uso de clases para organizar un grupo de métodos no relacionados no es orientación a objetos".

Incluso la propia gente que desarrolla _Go_ responde a esta pregunta [\[44\]](../../recursos.md) como "Si y no."

## Mi punto de vista

Ya que existen otros lenguajes que permiten programar orientado a objetos, sin ser realmente orientados a objetos, puedo decir que **"**_**Go**_ **es un lenguaje no orientado a objetos que permite la programación orientada a objetos -** _**aunque no de la forma tradicional**_**"**.

