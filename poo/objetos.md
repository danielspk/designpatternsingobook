# Objetos en Go

A diferencia de otros lenguajes orientados a objetos como _C++_, _Java_, _C\#_, _Python_ y _PHP_, entre otros, en _Go_ no hay clases, ni objetos, ni excepciones, ni herencia.

Rápidamente se podría inferir en que _Go_ no es un lenguaje orientado a objetos. ¿Cómo puede existir un lenguaje orientado a objetos que no disponga de clases?. La pregunta que realmente debemos hacernos es: _**¿Qué es la programación orientada a objetos?**_.

Los desarrolladores tenemos una tendencia natural a comprar las cosas. Entonces porque actualmente _Java_ es el rey indiscutido de la programación orientado a objetos, y éste lenguaje tiene entre otras características clases y herencia; si _Go_ no las tiene entonces no puede ser un lenguaje orientado a objetos.

_¿Alguien alguna vez escucho decir que _Javascript_ es un lenguaje orientado a objetos?_. Existe una gran discución sobre si lo es o no - a fin de cuentas en _Javascript_ tampoco hay clases ni herencia de la forma clásica como la que las hay en _Java_. _Javascript_ suele ser considerado un lenguaje orientado a objetos. _¿Porqué?_. Porque permite implementar ciertas características de la programación orientada a objetos.

> En ES6 se incorporan las clases en Javascript aunque con un soporte muy limitado en comparación con otros lenguajes orientados a objetos clásicos.

Al analizar a _Go_, debemos comparar que características de la programación orientada a objetos se pueden implementar y no simplemente hacer una comparación de un lenguaje respecto del otro.

## Cómo es la POO en Go:

### Objetos:

En _Go_ no existen clases ni objetos. Existen estructuras que son tipos de datos definidos por el usuario que pueden incorporar comportamientos. En una analogía con una clase, las propiedades pudieran ser los tipos de datos de la estructura, y los métodos las funciones asociadas a la estructura.

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

### Interfaces:

Las interfaces en _Go_ son una característica distintiva del lenguaje. A diferencia de otros lenguajes de programación las interfaces en _Go_ son implícitas. Cualquier estructura de datos que implemente todos los métodos de una interfaz, implícitamente la implementa.

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

Como se puede observar el método _SaltarYCaminar()_ espera como argumento a un tipo _Felino_ pero se le pasa un tipo _Leon_. Como la estructura _Leon_ implementar los métodos _Caminar()_ y _Saltar()_ implícitamente también es un _Felino_.

### Los tres pilares de la programación orientada a objetos:

Los tres pilares de la programación orientada a objetos son la _herencia_, el _encapsulamiento_ y el _polimorfismo_.

#### Herencia:

Como ya se dijo, en _Go_ no existe la herencia. Las estructuras permiten ampliar/modificar su comportamiento incrustrando otras estructuras - _más información en el siguiente apartado - [link](composicion.md)_

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

#### Encapsulación:

En _Go_ no existen identificadores de privacidad tales como _public_, _protected_ y _privated_ típicos de otros lenguajes de programación. _Go_ encapsula estructuras y funciones a nivel de paquete en base a convenciones de nombres.
Todos aquellos nombres que empiecen con mayúsculas serán accesibles (visibles) desde otros paquetes. Por el contrario, aquellos que comiencen con minúsculas serán _privados_.
Esta es la razón por la que en el código fuente de paquetes y bibliotecas de _Go_ hay estructuras y funciones que pueden comenzar con mayúsculas o minísculas.

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

#### Polimorfismo:

**Contenido en desarrollo.**

## Qué dicen otros autores:

Según Gigi Sayfan [\[4\]](recursos.md) "Go es una extraña mezcla de ideas antiguas y nuevas.", y "Muchas personas ni siquiera están seguras de si Go es un lenguaje orientado a objetos", sin embargo para el "Go es un lenguaje de programación orientado a objetos de buena fe. Permite el modelado basado en objetos y promueve las mejores prácticas de usar interfaces en lugar de tipos concretos de jerarquías. Go tiene algunas elecciones sintácticas inusuales, pero el trabajo general con tipos, métodos e interfaces parece simple, ligero y natural. La incrustración no es muy pura, pero aparentemente estaba en juego el pragmatismo, y se proporcionó una incrustración en lugar de sólo la composición por nombre".

Para Junade Ali [\[39\]](recursos.md) "La programación orientada a objetos es más que solo clases y objetos; es un paradigma de programación basado alrededor de objetos (estructuras de datos) que contienen campos de datos y métodos. Es esencial entender esto; el uso de clases para organizar un grupo de métodos no relacionados no es orientación a objetos". 

**Contenido en desarrollo.**

## Mi punto de vista:

Ya que existen otros lenguajes que permiten programar orientado a objetos sin ser realmente orientados a objetos puedo decir que **"**_**Go**_** es un lenguaje no orientado a objetos, que permite que permite la programación orientado a objetos - **_**aunque no de la forma tradicional**_**"**.

