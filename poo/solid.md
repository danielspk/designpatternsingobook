# Principios S.O.L.I.D. en Go

SOLID es un acrónimo introducido por Robert C. Martin en su libro "Agile Software Development, Principles, Patterns and Practices" [\[48\]](/recursos.md) y hace referencia a los siguientes cinco principios:

- **S**: *(SRP - Single responsibility principle)* Principio de responsabilidad única.
- **O**: *(OCP - Open closed principle)* Principio de abierto cerrado.
- **L**: *(LSP - Liskov substitution principle)* Principio de substitución de Liskov.
- **I**: *(ISP - Interface segregation principle)* Principio de segregación de la interfaz.
- **D**: *(DIP - Dependency inversion principle)* Principio de inversión de la dependencia.

El objetivo de aplicar estos principios es objtener sistemas orientados a objetos con código de mayor calidad, facilidad es su mantenimiento y buen rehuso de código.

### Principio de responsabilidad única

> Una clase debe tener una, y sólo una, razón para cambiar, lo que significa que una clase debe tener un solo trabajo.

La primera observación respecto de este principio es que en _Go_ no existen clases. Sin embargo, como vimos mediante la incorporación de comportamientos a estructuras de datos, podemos llegar a un concepto equivalente.

Este principio hace foco en que un objeto debe tener únicamente una responsabilidad encapsulada por la clase. Cuando se hace referencia a una responsabilidad es para referirse a una razón para cambiar.
Mantener una clase que tiene múltiples objetivos o responsabilidades es mucho más complejo que una clase enfocada en una única responsabilidad.

El siguiente ejemplo no cumple con éste principio ya que otorga a una estructura dos responsabilidades bien diferenciadas: *guardar en un archivo local* y *guardar en una base de datos*.

```go
package main

type Documento struct {
    Nombre  string
}

func (d *Documento) GuardarEnArchivo() {
   // ...
}

func (d *Documento) GuardarEnBaseDatos() {
   // ...
}
```

[Ejecutar código](https://play.golang.org/p/1d5JvLzQTEH)

Un *Documento* debería saber cómo acceder al sistema de archivos local y a la vez como conectarse y operar contra una base de datos. Implementar ambas acciones en una misma estructura genera un alto acoplamiento.

Creando estructuras con responsabilidades bien definidas se puede mejorar el código de la siguiente manera:

```go
package model

type Documento struct {
    Nombre  string
}
```

```go
package store

import "model"

type GuardadorDocumento interface {
    Guardar(d model.Documento)
}

type GuardadorDocumentoArchivo struct {
    Path  string
}

func (gda GuardadorDocumentoArchivo) Guardar(d model.Documento) {
   // ...
}

type GuardadorDocumentoBaseDatos struct {
    StringConnection  string
}

func (gdbd GuardadorDocumentoBaseDatos) Guardar(d model.Documento) {
   // ...
}
```

[Ejecutar código](https://play.golang.org/p/nxRPMtLbWP2)

Gracias a la organización en paquetes que permite _Go_ es posible crear estructuras, tipos, funciones y métodos empaquetados con propositos claros y bien definidos.

### Principio de abierto cerrado

> Los objetos o entidades deberían estar abiertos para la extensión, pero cerrados para su modificación.

Este principio hace mención a que una entidad permita extender su comportamiento pero sin que se modifique su código fuente. De esta forma la entidad puede ser extendida pero nunca modificada.

Imaginemos que se requiere cambiar el comportamiento de la siguiente estructura únicamente en uno de sus métodos:

```go
type Animal struct {
    Nombre  string
}

func (a Animal) Caminar() {
    // ...
}

func (a Animal) Saltar() {
    // ...
}
```

[Ejecutar código](https://play.golang.org/p/FP80Iem9qqV)

Podemos hacerlo de la siguiente forma:

```go
type AnimalModificado struct {
    Animal
}

func (am AnimalModificado) Caminar() {
    // ...
}
```

[Ejecutar código](https://play.golang.org/p/Sf1WkRugRN3)

Gracias a la composición que permite _Go_ es posible componer tipos simples en más complejos.

### Principio de substitución de Liskov

> Las subclases deberían poder ser sustituidas por sus clases base.

Este principio aduce a que el contrato de una clase base debe ser honrado por sus clases derivadas.

**Contenido y ejemplo en desarrollo.**

Gracias al modo de intefaces que permite _Go_ es factible expresar las dependencias entre paquetes a traves de interfaces y no mediante tipos concretos.

### Principio de segregación de la interfaz

> Nunca se debe obligar a un cliente a implementar una interfaz que no utilice, o no se debe forzar a los clientes a depender de métodos que no usan.

Este principio hace foco en como deben definirse las interfaces. Las mismas deben ser pequeñas y específicas.
Grandes y complejas interfaces obligan al cliente a implementar métodos que no necesita.

**Contenido y ejemplo en desarrollo.**

En _Go_ puede aplicarse este concepto aislando el comportamiento requerido utilizando interfaces.

### Principio de inversión de la dependencia

> Los módulos de alto nivel no deben depender de módulos de bajo nivel. Ambos deberían depender de abstracciones.
Las abstracciones no deben depender de los detalles. Los detalles deben depender de las abstracciones. 

Este principio esta basado en reducir las dependencias entre los módulos del código para atacar el alto acoplamiento.

**Contenido y ejemplo en desarrollo.**

La forma en la que compila _Go_ valida que este principio se cumpla. Caso contrario el programa no podría compilar.

## Conclusión

Si bien el libro de Robert C. Martin [\[48\]](/recursos.md) tiene más de una decada y media y hace referencia a lenguajes propiamente orientados a objetos, vimos como también pueden aplicarse esos principios en _Go_.

Como se vio en el apartado anterior, el poder de la composición y de las interfaces implícitas le permiten a _Go_ implementar prácticas y conceptos propios de la programación orientada a objetos.
